# Properties

Each CacheBox provider can have its own set of configuration properties it needs for operation. Our CF providers also have some. Please note, all properties other than "cacheName" are passed through to the underlying EHCache implementation in ColdFusion. The default values may differ if you have edited the ehcache.xml file on your server.

|Property|Type|Required|Default|Description|
|--|--|--|--|--|
|cacheName |string |false |*object*|The named cache to talk to via ColdFusion cache operations. By default we talk to the default ColdFusion object cache.|
|clearOnFlush |boolean|false|*true*|Sets whether the MemoryStore should be cleared when flush() is called on the cache|
|diskExpiryThreadIntervalSeconds |integer|false|*120 (2 minutes) * |The interval in seconds between runs of the disk expiry thread.|
|diskPersistent |boolean |false|*false*|Specifies whether to persist caches stored on disk through JVM restarts.|
|diskSpoolBufferSizeMB |integer|false|*30*|The size of the disk spool used to buffer writes|
|external|boolean|false|*false*|Specifies whether no timeout or idletime applies. A true value indicates that the object or page is cached without any timespan being specified.|
|maxElementsInMemory |integer|fasle|*10000*|The maximum number of objects that can be cached in memory. If the number is exceeded and overflowtodisk is false, the new objects entered replace old elements using algorithm specified in the memoryevictionpolicy entry.|
|maxElementsOnDisk |integer|false|*10000000*|The maximum number of objects that can be stored on disk if overfllowtodisk is true.|
|memoryEvictionPolicy |string|false|*LRU*|The algorithm to used to evict old entries when maximum limit is reached, such as LRU (least recently used) or LFU (least frequently used).|
|overflowToDisk |boolean|false|*false*|Specifies whether when the maximum number of elements allowed in memory is reached, objects can be moved to disk, as determined by the memoryevictionpolicy value.|
|timeToIdleSeconds |integer|false|*86400*|The idle time in seconds. Used if a cfcache tag does not specify an idleTime attribute.|
|timeToLiveSeconds |integer|false|*86400*|The timeout time in seconds. Used if a cfcache tag does not specify a timespan attribute.|

> **Info** Note: Please note that you can configure more than 1 CFColdboxProvider cache engine in your applications that c  talk to more than one referenced ColdFusion (EHCache) custom cache.
