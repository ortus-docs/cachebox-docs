# Cache Providers

We have shipped CacheBox with several CacheBox providers that you can use in your applications. There are basically two modes of operation for a CacheBox provider and it is all determined by the interface they implement:

1. `ICacheProvider` : A standalone cache provider
2. `IColdboxApplicationCache` : A cache provider for usage by the ColdBox Framework

The following are the shipped providers:

|Provider|ColdBox Enabled|Reporting Enabled|Description|
|--|--|--|--|
|CacheBoxProvider |false |true |Our very own CacheBox caching engine|
|CacheBoxColdBoxProvider |true|true |Our CacheBox caching engine prepared for ColdBox application usage|
|CouchbaseProvider |false |true|An awesome provider for Couchbase NoSQL server, see [CacheBox-Couchbase](http://wiki.coldbox.org/wiki/CacheBox-Couchbase.cfm)|
|CouchbaseColdboxProvider |true |true|An awesome provider with ColdBox application support for Couchbase NoSQL server, see [CacheBox-Couchbase](http://wiki.coldbox.org/wiki/CacheBox-Couchbase.cfm)|
|CFProvider |false|true|A ColdFusion 9.0.1 and above implementation|
|CFColdBoxProvider |true|true|A ColdBox enhanced version of our ColdFusion 9.0.1 cache provider|
|RailoProvider |false|true|A ColdBox enhanced version of our Railo cache provider |
|RailoColdBoxProvider |true|true|A ColdBox enhanced version of our Railo cache provider|
|MockProvider |true|false|A ColdBox enhanced cache provider that can be used for mocking or testing|

Each provider has the shared functionality provided by the ICacheProvider and IColdboxApplicationCache interfaces, so I encourage you to look at the CFC [API Docs](http://apidocs.ortussolutions.com/cachebox/2.0.0/index.html) for an in-depth view of their API. Also, please note that each cache provider implementation has also some extra methods and functionality according to their implementation, so please check out the API docs for each provider.
