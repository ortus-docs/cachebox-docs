# CF Providers

Our `CFColdboxProvider` is an implementation specifically written for Adobe ColdFusion 9.0.1 and beyond. This provider leverages the [EHCache](http://ehcache.org/) engine within ColdFusion 9 and extends the native ColdFusion capabilities by talking to the [EHCache](http://ehcache.org/) sessions natively via Java. In this manner we are able to do things like:

* Get extended cached object metadata
* Get overall cache statistics
* Talk to terracotta classes
* Do quiet operations on get, clear, and put
* Check if an element is expired
* Do reporting and content reporting
* Much more

## Properties

Each CacheBox provider can have its own set of configuration properties it needs for operation. Our CF providers also have some. Please note, all properties other than "cacheName" are passed through to the underlying EHCache implementation in ColdFusion. The default values may differ if you have edited the `ehcache.xml` file on your server.

| Property | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| cacheName | string | false | _object_ | The named cache to talk to via ColdFusion cache operations. By default we talk to the default ColdFusion object cache. |
| clearOnFlush | boolean | false | _true_ | Sets whether the MemoryStore should be cleared when flush\(\) is called on the cache |
| diskExpiryThreadIntervalSeconds | integer | false | _120 \(2 minutes\)_  | The interval in seconds between runs of the disk expiry thread. |
| diskPersistent | boolean | false | _false_ | Specifies whether to persist caches stored on disk through JVM restarts. |
| diskSpoolBufferSizeMB | integer | false | _30_ | The size of the disk spool used to buffer writes |
| external | boolean | false | _false_ | Specifies whether no timeout or idletime applies. A true value indicates that the object or page is cached without any timespan being specified. |
| maxElementsInMemory | integer | fasle | _10000_ | The maximum number of objects that can be cached in memory. If the number is exceeded and overflowtodisk is false, the new objects entered replace old elements using algorithm specified in the memoryevictionpolicy entry. |
| maxElementsOnDisk | integer | false | _10000000_ | The maximum number of objects that can be stored on disk if overfllowtodisk is true. |
| memoryEvictionPolicy | string | false | _LRU_ | The algorithm to used to evict old entries when maximum limit is reached, such as LRU \(least recently used\) or LFU \(least frequently used\). |
| overflowToDisk | boolean | false | _false_ | Specifies whether when the maximum number of elements allowed in memory is reached, objects can be moved to disk, as determined by the memoryevictionpolicy value. |
| timeToIdleSeconds | integer | false | _86400_ | The idle time in seconds. Used if a cfcache tag does not specify an idleTime attribute. |
| timeToLiveSeconds | integer | false | _86400_ | The timeout time in seconds. Used if a cfcache tag does not specify a timespan attribute. |

> **Info** Please note that you can configure more than 1 `CFColdboxProvider` cache engine in your applications that can talk to more than one referenced ColdFusion \(EHCache\) custom cache.

