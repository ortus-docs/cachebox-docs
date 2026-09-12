# Cache Providers

We have shipped CacheBox with several CacheBox providers that you can use in your applications. There are basically two modes of operation for a CacheBox provider and it is all determined by the interface they implement:

1. `ICacheProvider` : A standalone cache provider
2. `IColdboxApplicationCache` : A cache provider for usage by the ColdBox Framework

The following are the shipped providers:

| Provider                | ColdBox Enabled | Reporting Enabled | Description                                                               |
| ----------------------- | --------------- | ----------------- | ------------------------------------------------------------------------- |
| CacheBoxProvider        | false           | true              | Our very own CacheBox caching engine                                      |
| CacheBoxColdBoxProvider | true            | true              | Our CacheBox caching engine prepared for ColdBox application usage        |
| CFProvider              | false           | true              | A ColdFusion 9.0.1 and above implementation                               |
| CFColdBoxProvider       | true            | true              | A ColdBox enhanced version of our ColdFusion 9.0.1 cache provider         |
| LuceeProvider           | false           | true              | A ColdBox enhanced version of our Lucee cache provider                    |
| LuceeColdBoxProvider    | true            | true              | A ColdBox enhanced version of our Lucee cache provider                    |
| BoxLangProvider         | false           | true              | BoxLang native cache engine integration                                   |
| BoxLangColdBoxProvider  | true            | true              | BoxLang native cache engine for ColdBox applications                      |
| MockProvider            | true            | false             | A ColdBox enhanced cache provider that can be used for mocking or testing |

Each provider has the shared functionality provided by the ICacheProvider and IColdboxApplicationCache interfaces, so I encourage you to look at the class [API Docs](https://apidocs.ortussolutions.com/cachebox/5.0.0/index.html) for an in-depth view of their API. Also, please note that each cache provider implementation has also some extra methods and functionality according to their implementation, so please check out the API docs for each provider.

## BoxLang+ Premium Connectors

Beyond the built-in providers above, [BoxLang+](https://boxlang.ortusbooks.com/boxlang-+-++) - Ortus's premium module subscription - ships additional distributed caching and search connectors:

| Module            | Description                                                            | Install                     |
| ----------------- | ------------------------------------------------------------------------ | ---------------------------- |
| `bx-couchbase`    | Distributed caching and NoSQL document storage via Couchbase             | `box install bx-couchbase`   |
| `bx-redis`        | Redis-backed caching, data structures, and pub/sub messaging             | `box install bx-redis`       |
| `bx-meilisearch`  | Full-text search integration via Meilisearch                             | `box install bx-meilisearch` |

{% hint style="info" %}
These are part of the **BoxLang+** subscription tier and require `bx-plus` for license management - they are not part of the free/open-source CacheBox distribution. There is currently no OpenSearch/Elasticsearch connector; `bx-meilisearch` is the closest search-oriented option today.
{% endhint %}

See [BoxLang+ Modules](https://boxlang.ortusbooks.com/boxlang-+-++/modules) for the full, current list.
