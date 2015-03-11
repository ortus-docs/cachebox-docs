# Default Cache

The `defaultCache` element is in itself a structure of configuration data for the default cache provider of type `cachebox.system.cache.providers.CacheBoxProvider`. This is a reserved cache name and it is MANDATORY to declare and its name or type cannot be changed. 

However, if you are using CacheBox within a ColdBox application, the provider will switch itself to `cachebox.system.cache.providers.CacheBoxColdBoxProvider` by using the `coldboxEnabled` key. So let's see the configuration keys for our default cache.

##Default Cache Properties:

|Key|Type|Required|Default|Description|
|--|--|--|--|--|
|ObjectDefaultTimeout|numeric |false |60 |The default lifespan of an object in minutes |
|ObjectDefaultLastAccessTimeout |numeric |false |30 |The default last access or idle timeout in minutes|
|UseLastAccessTimeouts |Boolean |false |true |Use or not idle timeouts|
|ReapFrequency |numeric |false|2|The delay in minutes to produce a cache reap (Not guaranteed) |
|FreeMemoryPercentageThreshold |numeric |false |0|The numerical percentage threshold of free JVM memory to have available before caching. If the JVM free memory falls below this setting, the cache will run the eviction policies in order to cache new objects. (0=Unlimited) |
|MaxObjects |numeric |false|200|The maximum number of objects for the cache|
|EvictionPolicy |string or path | false | LRU | The eviction policy algorithm class to use.|
|EvictCount |numeric |false|1|The number of objects to evict once an execution of the policy is requested. You can increase this to make your evictions more aggressive|
|objectStore |string |false |ConcurrentStore|The object store to use for caching objects. |
|ColdBoxEnabled| Boolean|false|false|A flag that switches on/off the usage of either a plain vanilla CacheBox provider or a ColdBox enhanced provider. This must be true when used within a ColdBox application and it applies for the default cache ONLY.|

## Eviction Policies
* LFU (Least Frequently Used)
* LRU (Least Recently Used)
* FIFO (First In First Out)
* Custom: You can also build your own and pass the instantiation path in this setting

## Object Stores
* **ConcurrentStore** - Uses concurrent hashmaps for increased performance
* **ConcurrentSoftReferenceStore** - Concurrent hashmaps plus java soft references for JVM memory sensitivity
* **DiskStore** - Uses a physical disk location for caching (Uses java serialization for complex objects)
* **JDBCStore** - Uses a JDBC datasource for caching (Uses java serialization for complex objects)
* **Custom** : You can also build your own and pass the instantiation path in this setting.

> **Caution** : Please note that each object store could have more configuration properties that you will need to add to the configuration structure. To find out about these extra configuration properties, please see the Object Store's section.

**Example:**

```javascript
// The CacheBox configuration structure DSL
cacheBox = {
    // Please note that each object store could have more configuration properties
    defaultCache = {
        objectDefaultTimeout = 60,
        objectDefaultLastAccessTimeout = 30,
        useLastAccessTimeouts = true,
        reapFrequency = 2,
        freeMemoryPercentageThreshold = 0,
        evictionPolicy = "LRU",
        evictCount = 1,
        maxObjects = 200,
        // Our default store is the concurrent soft reference
        objectStore = "ConcurrentSoftReferenceStore",
        // This switches the internal provider from normal cacheBox to coldbox enabled cachebox
        coldboxEnabled = false
    },
};
```
