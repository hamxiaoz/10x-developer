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
- [add index](https://kadira.io/academy/meteor-performance-101/content/make-your-app-faster#learn-indexing)

Publication
- limit [fields](http://docs.meteor.com/#/full/fieldspecifiers) on publication:
`Users.find({}, {fields: {password: 0, hash: 0}})`

Counting on the server side
- [Mongodb aggregation](https://kadira.io/academy/meteor-performance-101/content/make-your-app-faster#do-server-side-aggregations)

