# Meteor

see also [https://gist.github.com/hamxiaoz](https://gist.github.com/hamxiaoz)

## Guide

Kadira Academy

* \_ [routing guide: flow router](https://kadira.io/academy/meteor-routing-guide) \(don't do data management and auth on route level\)
* x [Meteor Performance 101](https://kadira.io/academy/meteor-performance-101)
* \_ [bulletproof](https://bulletproofmeteor.com/)

Little Projects

* [https://themeteorchef.com/snippets/importing-csvs/](https://themeteorchef.com/snippets/importing-csvs/)

Tools:

* admin for mongo db: [http://www.drmongo.com/](http://www.drmongo.com/)

### How to do logging via winston and loggly

Inspired from this guide: [https://meteorhacks.com/logging-support-for-meteor](https://meteorhacks.com/logging-support-for-meteor) 1. Sign up [loggly](https://github.com/hamxiaoz/notes/tree/9d65a28e8c0ebcdd1e2037fd60457da8edf05f03/loggly.com) 2. add 'winston' and 'winston-loggly' to package.json 3. code Don't forget Meteor.npmRequire is only available on **server side** 4. `LOGGER.info` will output on console and send events to loggly

```coffeescript
# Setup logging in server/config.js
@LOGGER = Meteor.npmRequire 'winston'
Meteor.npmRequire 'winston-loggly'
LOGGER.add(LOGGER.transports.Loggly, {
  token: "YOUR-TOKEN",
  subdomain: "YOUR-DOMAIN",
  tags: ["YOUR-TAG"],
  json:true,
  handleExceptions: true, # handle exception in logger
  humanReadableUnhandledException: true
});
LOGGER.existOnError = false # don't exit on error
LOGGER.info 'logger started'
```

### How to send email using SendGrid

Or see my [Medium post](https://medium.com/@hamxiaoz/meteor-how-to-send-email-using-sendgrid-25cba3b4bc7d#.c7dnzbf4h)

* regiter [sendgrid](https://sendgrid.com/)
* [create different user](https://app.sendgrid.com/settings/credentials) with \(Mail capability\): [https://app.sendgrid.com/settings/credentials](https://app.sendgrid.com/settings/credentials)
* `meter add email`
* Then you can use the mail package to send email: [https://gist.github.com/aaronthorp/8410571](https://gist.github.com/aaronthorp/8410571)
* Reference: [https://themeteorchef.com/snippets/using-the-email-package/](https://themeteorchef.com/snippets/using-the-email-package/)
* [Why not Mandrill?](https://news.ycombinator.com/item?id=11203056)
* [Why SendGrid?](https://www.inboxtrail.com/compare)

## DDP

[DDP Spec](https://github.com/meteor/meteor/blob/devel/packages/ddp/DDP.md)

[meteor-ddp-analyzer](https://github.com/arunoda/meteor-ddp-analyzer)

## Performance

DB

* When setup db, enable db oplog   
  * If your query has a limit but not a sort specifier, your query can't take advantage of oplog

    `Posts.find({category: "meteor"}, {limit: 10});`
* \_ [add index](https://kadira.io/academy/meteor-performance-101/content/make-your-app-faster#learn-indexing)

Counting on the server side

* \_ [Mongodb aggregation](https://kadira.io/academy/meteor-performance-101/content/make-your-app-faster#do-server-side-aggregations)
* \_ [https://kadira.io/academy/meteor-performance-101/content/reducing-pubsub-data-usage\#counting-on-the-server-side](https://kadira.io/academy/meteor-performance-101/content/reducing-pubsub-data-usage#counting-on-the-server-side)

Publication

* limit [fields](http://docs.meteor.com/#/full/fieldspecifiers) \(cannot do both inclusion/exclusion\) on publication:

  `Users.find({}, {fields: {password: 0, hash: 0}})` 

* [Infinite Scrolling using limit](http://www.meteorpedia.com/read/Infinite_Scrolling)
* [Pagination](https://www.discovermeteor.com/blog/pagination-problems-meteor/), problem demo on [MeteorPad](http://meteorpad.com/pad/ELf297D2uiTwdsuzQ/Template%20Subs%20v2%20-%20Flicker)

Subscription

* Use [subscription manager](https://github.com/kadirahq/subs-manager) to avoid re-sub when route changes

\_ Observer

* [https://kadira.io/academy/meteor-performance-101/content/improve-cpu-and-network-usage](https://kadira.io/academy/meteor-performance-101/content/improve-cpu-and-network-usage)
* [https://kadira.io/academy/meteor-performance-101/content/know-your-observers](https://kadira.io/academy/meteor-performance-101/content/know-your-observers)

Reduce wait time: `this.unblock()`

* `this.unblock` will allow the next available DDP message to process without waiting for the current method. 
* Use it when your **methods** and subscriptions \(enabled via this package: `meteor add meteorhacks:unblock`\) don't depend on others
* Do not use it when a method will cause side effects and subsequent methods will depend on those side effects.    

  _For example you have a method to update name and another method to send notification emails about the updated name, if unblock is used, the email might contain the old name._

* This is all on a per client basis: there no blocking involved globally.

Try [CPU profiling](https://kadira.io/academy/meteor-performance-101/content/meteor-cpu-profiling) [analysis](https://kadira.io/academy/meteor-performance-101/content/analyze-meteor-cpu-profile)

## Client Side

### Store data in template instance using ReactiveVar

You can store [ReactiveVar](http://docs.meteor.com/#/full/reactivevar) in the [template instance](http://docs.meteor.com/#/full/template_inst). A ReactiveVar is similar to a Session variable, with a few differences:

* ReactiveVars don't have global names, like the "foo" in Session.get\("foo"\). Instead, they may be created and used locally, for example attached to a template instance, as in: `this.foo.get(). // 'this' is the template instance`
* ReactiveVars are not automatically migrated across hot code pushes, whereas Session state is.
* ReactiveVars can hold any value, while Session variables are limited to JSON or EJSON.

```javascript
if (Meteor.isClient) {  
  Template.hello.created = function () {
    // counter starts at 0
    this.counter = new ReactiveVar(0);
  };

  Template.hello.helpers({
    counter: function () {
      return Template.instance().counter.get();
    }
  });

  Template.hello.events({
    'click button': function (event, template) {
      // increment the counter when button is clicked
      template.counter.set(template.counter.get() + 1);
    }
  });
}
```

## Packages

### fs

* collection-fs
  * tips: [http://blog.zipboard.co/2015/11/23/cfs-tips-and-tricks-for-meteorjs/](http://blog.zipboard.co/2015/11/23/cfs-tips-and-tricks-for-meteorjs/)
* slingshot: [https://atmospherejs.com/edgee/slingshot](https://atmospherejs.com/edgee/slingshot)
  * go directly to S3
  * Set ACL to 'private' so only your meteor app can download the file
  * Use S3 sdk to generate pre-signed url for public download
    * [https://github.com/peerlibrary/meteor-aws-sdk](https://github.com/peerlibrary/meteor-aws-sdk)
    * [http://docs.aws.amazon.com/AWSJavaScriptSDK/guide/node-services.html](http://docs.aws.amazon.com/AWSJavaScriptSDK/guide/node-services.html)
    * [http://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/S3.html\#getSignedUrl-property](http://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/S3.html#getSignedUrl-property)
* Upload and download in server [https://github.com/VeliovGroup/Meteor-Files/](https://github.com/VeliovGroup/Meteor-Files/)
* Upload to any path in server: [https://github.com/tomitrescak/meteor-uploads](https://github.com/tomitrescak/meteor-uploads)

