# ColdBox Application Configuration

```javascript
/coldbox/system/web/config/CacheBox
```

The contents of this configuration CFC is the following:

```javascript
function configure(){
    // The CacheBox configuration structure DSL
    cacheBox = {
        // LogBox config already in coldbox app, not needed
        // logBoxConfig = "coldbox.system.web.config.LogBox",

        // The defaultCache has an implicit name "default" which is a reserved cache name
        // It also has a default provider of cachebox which cannot be changed.
        // All timeouts are in minutes
        defaultCache = {
            objectDefaultTimeout = 120, //two hours default
            objectDefaultLastAccessTimeout = 30, //30 minutes idle time
            useLastAccessTimeouts = true,
            reapFrequency = 2,
            freeMemoryPercentageThreshold = 0,
            evictionPolicy = "LRU",
            evictCount = 1,
            maxObjects = 300,
            objectStore = "ConcurrentStore", //guaranteed objects
            coldboxEnabled = true
        },

        // Register all the custom named caches you like here
        caches = {
            // Named cache for all coldbox event and view template caching
            template = {
                provider = "coldbox.system.cache.providers.CacheBoxColdBoxProvider",
                properties = {
                    objectDefaultTimeout = 120,
                    objectDefaultLastAccessTimeout = 30,
                    useLastAccessTimeouts = true,
                    reapFrequency = 2,
                    freeMemoryPercentageThreshold = 0,
                    evictionPolicy = "LRU",
                    evictCount = 2,
                    maxObjects = 300,
                    objectStore = "ConcurrentSoftReferenceStore" //memory sensitive
                }
            }
        }
    };
}
```

This configuration file configures CacheBox with two caches: *default* and *template*. The *default* cache is used for persistence for handlers, plugins, interceptors, and model objects. The template cache is used for event caching and view fragment caching. It is also important to note that the *template* cache uses the *ConcurrentSoftReferenceStore* for its objects. This means that even/view caching is subject to available memory via the JVM, a memory sensitive cache. This is essential as you could have lots of events being cached and you want to be considerate with memory concerns. It is also limited to 300 objects.

Now, this is all nice and dandy, but what if I want to configure CacheBox "MY WAY!!"? Well, don't shout, we are just getting there. There are several ways you can configure CacheBox from within your applications, so chose wisely.


