# Cache Providers

We have shipped CacheBox with several CacheBox providers that you can use in your applications. There are basically two modes of operation for a CacheBox provider and it is all determined by the interface they implement:

1. `ICacheProvider` : A standalone cache provider
2. `IColdboxApplicationCache` : A cache provider for usage by the ColdBox Framework

The following are the shipped providers:

| Provider | ColdBox Enabled | Reporting Enabled | Description |
| --- | --- | --- | --- |
| CacheBoxProvider | false | true | Our very own CacheBox caching engine |
| CacheBoxColdBoxProvider | true | true | Our CacheBox caching engine prepared for ColdBox application usage |
| CFProvider | false | true | A ColdFusion 9.0.1 and above implementation |
| CFColdBoxProvider | true | true | A ColdBox enhanced version of our ColdFusion 9.0.1 cache provider |
| LuceeProvider | false | true | A ColdBox enhanced version of our Lucee cache provider |
| LuceeColdBoxProvider | true | true | A ColdBox enhanced version of our Lucee cache provider |
| MockProvider | true | false | A ColdBox enhanced cache provider that can be used for mocking or testing |

Each provider has the shared functionality provided by the ICacheProvider and IColdboxApplicationCache interfaces, so I encourage you to look at the CFC [API Docs](https://apidocs.ortussolutions.com/cachebox/5.0.0/index.html) for an in-depth view of their API. Also, please note that each cache provider implementation has also some extra methods and functionality according to their implementation, so please check out the API docs for each provider.

