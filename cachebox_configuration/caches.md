# Caches

The caches element is in itself a structure of configuration data for aggregating named cache providers of ANY type. The key is the unique name of the cache to aggregate under this CacheBox instance. The value should be a structure with the following keys:

|Key|Type|Required|Default|Description|
|--|--|--|--|--|
|provider|string|true|---|The instantiation path of the cache that must implement our `ICacheProvider` interface.|
|properties|struct|false| `{}` |A structure of name-value pairs of configuration data for the cache to declare.|

Example:

```javascript
// Register all the custom named caches you like here
caches = {
    sampleCache1 = {
        provider="cachebox.system.cache.providers.CacheBoxProvider",
        properties = {
            objectDefaultTimeout="20",
            useLastAccessTimeouts="false",
            reapFrequency="1",
            evictionPolicy="LFU",
            evictCount="1",
            maxObjects="100",
            objectStore="ConcurrentSoftReferenceStore"
        }
    },
    sampleCache2 = {
        provider = "cachebox.system.cache.providers.CFColdboxProvider"
    }
},
```

