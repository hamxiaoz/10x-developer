# Meteor

see also https://gist.github.com/hamxiaoz

## Guide
_ [Kadira Academy](https://kadira.io/academy)
- routing (don't do data management and auth on route level)
- performance
- bulletproof

## DDP
[DDP Spec](https://github.com/meteor/meteor/blob/devel/packages/ddp/DDP.md)

[meteor-ddp-analyzer](https://github.com/arunoda/meteor-ddp-analyzer)

## Performance

DB
- When setup db, enable db oplog   
    - If your query has a limit but not a sort specifier, your query can't take advantage of oplog
`Posts.find({category: "meteor"}, {limit: 10});`
- _ [add index](https://kadira.io/academy/meteor-performance-101/content/make-your-app-faster#learn-indexing)

Publication
- limit [fields](http://docs.meteor.com/#/full/fieldspecifiers) on publication:
`Users.find({}, {fields: {password: 0, hash: 0}})`
- _ pagination: [1](http://www.meteorpedia.com/read/Infinite_Scrolling) [2](https://www.discovermeteor.com/blog/pagination-problems-meteor/)

Subscription
- Use [subscription manager](https://github.com/kadirahq/subs-manager) to avoid re-sub when route changes

Counting on the server side
- _ [Mongodb aggregation](https://kadira.io/academy/meteor-performance-101/content/make-your-app-faster#do-server-side-aggregations)
- _ https://kadira.io/academy/meteor-performance-101/content/reducing-pubsub-data-usage#counting-on-the-server-side

_ Observer
- https://kadira.io/academy/meteor-performance-101/content/improve-cpu-and-network-usage

Reduce wait time: `this.unblock()`
- `this.unblock` will allow the next available DDP message to process without waiting for the current method. 
- Use it when your **methods** and subscriptions (enabled via this package: `meteor add meteorhacks:unblock`) don't depend on others
- Do not use it when a method will cause side effects and subsequent methods will depend on those side effects.    
_For example you have a method to update name and another method to send notification emails about the updated name, if unblock is used, the email might contain the old name._
- This is all on a per client basis: there no blocking involved globally.


Try [CPU profiling](https://kadira.io/academy/meteor-performance-101/content/meteor-cpu-profiling)


