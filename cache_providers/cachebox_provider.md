# CacheBox Provider

The CacheBox provider is our very own enterprise cache implementation that has been part of the core since its initial baby step versions. Our caching engine has matured over the years and it has been proven effective, fast, scalable and very user friendly. Here are the two implementations for our CacheBox provider:

1. CacheBoxProvider : Our base CacheBox provider caching engine
2. CacheBoxColdBoxProvider : A subclass of *CacheBoxProvider* that enables caching operations for ColdBox applications

## Properties

|Key|Type|Required|Default|Description|
|--|--|--|--|--|
|ObjectDefaultTimeout |numeric|false|60 |The default lifespan of an object in minutes |
|ObjectDefaultLastAccessTimeout |numeric |false |30 |The default last access or idle timeout in minutes|
|UseLastAccessTimeouts |Boolean |false |true |Use or not idle timeouts|
|ReapFrequency |numeric |false |2|The delay in minutes to produce a cache reap (Not guaranteed) |
|FreeMemoryPercentageThreshold |numeric |false |0 |The numerical percentage threshold of free JVM memory to have available before caching. If the JVM free memory falls below this setting, the cache will run the eviction policies in order to cache new objects. (0=Unlimited) |
|MaxObjects |numeric |false|200|The maximum number of objects for the cache|
|EvictionPolicy |string or path |false|LRU|The eviction policy algorithm class to use.*|
|EvictCount |numeric|false|1|The number of objects to evict once an execution of the policy is requested. You can increase this to make your evictions more aggressive|
|objectStore |string |false|*ConcurrentStore*|ConcurrentStore 	The object store to use for caching objects.**|
|ColdboxEnabled |Boolean|false|false|A flag that switches on/off the usage of either a plain vanilla CacheBox provider or a ColdBox enhanced provider. This must be true when used within a ColdBox application and it applies for the default cache ONLY.|

> *Coldbox ships with the following object store:

* LFU (Least Frequently Used)
* LFU (Least Frequently Used)
* LFU (Least Frequently Used)
<br><br>
 You can also build your own and pass the instantiation path in this setting

> **ColdBox ships with the following object stores:

* ConcurrentStore - Uses concurrent hashmaps for increased performance
* ConcurrentSoftReferenceStore - Concurrent hashmaps plus java soft references for JVM memory sensitivity
* DiskStore - Uses a physical disk location for caching (Uses java serialization for complex objects)
* JDBCStore - Uses a JDBC datasource for caching (Uses java serialization for complex objects)
<br><br>
 You can also build your own and pass the instantiation path in this setting

Please also note that each of the object stores can have extra configuration properties that you will need to set. So for that, let's delve a little deeper into object stores.
