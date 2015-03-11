# Creating CacheBox

CacheBox is the core framework you need to instantiate in order to work with caching in your application. You can instantiate it with a `CacheBoxConfig` object that will hold all of your caching configurations. To configure the library you can either do it programmatically or via a struct/data DSL, the choice is yours. After the library is instantiated and configured you can ask from it a named cache provider, or interact with the caches. By default, CacheBox can be started with no configuration and it will configure itself with the default configuration that is shipped with CacheBox that can be found in the following location:

```javascript
/cachebox/system/cache/config/DefaultConfiguration.cfc
```

The default configuration is the following:

```javascript
function configure(){
    // The CacheBox configuration structure DSL
    cacheBox = {
        // LogBox Configuration file
        logBoxConfig = "cachebox.system.cache.config.LogBox",

        // Scope registration, automatically register the cachebox factory instance on any CF scope
        // By default it registers itself on application scope
        scopeRegistration = {
            enabled = true,
            scope   = "application", // valid CF scope
            key     = "cacheBox"
        },

        // The defaultCache has an implicit name of "default" which is a reserved cache name
        // It also has a default provider of cachebox which cannot be changed.
        // All timeouts are in minutes
        // Please note that each object store could have more configuration properties
        defaultCache = {
            objectDefaultTimeout = 120,
            objectDefaultLastAccessTimeout = 30,
            useLastAccessTimeouts = true,
            reapFrequency = 2,
            freeMemoryPercentageThreshold = 0,
            evictionPolicy = "LRU",
            evictCount = 1,
            maxObjects = 300,
            // Our default store is the concurrent soft reference
            objectStore = "ConcurrentSoftReferenceStore",
            // This switches the internal provider from normal cacheBox to coldbox enabled cachebox
            coldboxEnabled = false
        },

        // Register all the custom named caches you like here
        caches = {},
        // Register all event listeners here, they are created in the specified order
        listeners = []
    };
}
```

If you are using CacheBox within a ColdBox application you do not need to worry about creating or even configuring the framework, as ColdBox ships already with a default configuration for ColdBox applications. However, you also have full control of configuring CacheBox at your application level (Please see the [ColdBox application configuration section](../coldbox_application_enhancements/README.md)). The default configuration for a ColdBox application can be found in the following location:

```javascript
/coldbox/system/web/config/CacheBox.cfc
```
## Modes of Operation
In summary, CacheBox has two modes of operation:

* Standalone Framework
* ColdBox Application

If you have downloaded CacheBox as a standalone framework, then please make sure you use the correct namespace path (`cachebox.system`). Also, once you create CacheBox make sure that you persist it somewhere, either in Application scope or any other scope or a dependency injection context (WireBox). ColdBox application users already have an instance of CacheBox created for you in every application and it is stored in the main application controller and can be retrieved via the following function:

```javascript
// Get a reference to CacheBox
controller.getCacheBox();

// Get a reference to the default cache provider
controller.getCache() or getCache()

// Get a reference to a named cache provider
controller.getCache("template") or getCache("template")
```

> **Info** Note: Most of the examples shown in this documentation refer the default framework namespace of coldbox.system. However, if you are using CacheBox as a standalone framework, then the namespace to use is `cachebox.system`. Happy Coding!

Creating CacheBox Examples <br>
<br>
 Let's start with the simplest example of them all which is just creating CacheBox with the default configuration. The rest of the samples show different configuration options:

```javascript
import cachebox.system.cache.*;

// create cachebox
cachebox = new CacheFactory();
// get the default cache
cache = cachebox.getDefaultCache();
// set a value in cache, with 60 minute timeout and 20 minute idle timeout.
cache.set("MyValue", {name="Luis Majano", awesome=true, cacheWeirdo=true}, 60,20);
```

Here are some more configuration samples:

```javascript
// Create CacheBox with default configuration
cacheBox = createObject("component","cachebox.system.cache.CacheFactory").init();


// Create the config object with an XML configuration file
config = createObject("component","cachebox.system.cache.config.CacheBoxConfig").init(expandPath('cachebox.xml'));
// Create CacheBox instance
cacheBox = createObject("component","cachebox.system.cache.CacheFactory").init(config);

// Create the config object as a CacheBox DSL Simple CFC
dataCFC = createObject("component","MyCacheBoxConfig");
config = createObject("component","cachebox.system.cache.config.CacheBoxConfig").init(CFCConfig=dataCFC);
// Create CacheBox instance
cacheBox = createObject("component","cachebox.system.cache.CacheFactory").init(config);


// Create the config object as a CacheBox DSL Simple CFC path only
config = createObject("component","cachebox.system.cache.config.CacheBoxConfig").init(CFCConfigPath="MyCacheBoxConfig");
// Create CacheBox instance
cacheBox = createObject("component","cachebox.system.cache.CacheFactory").init(config);

// Create CacheBoxConfig, call configuration methods on it and then create the factory
config = createObject("component","cachebox.system.cache.config.CacheBoxConfig").init();
// Configure programmatically: You can chain methods, woot!
config.scopeRegistration(true,"application").default(objectStore="DiskStore",maxObject=200);
// Create CacheBox instance
cacheBox = createObject("component","cachebox.system.cache.CacheFactory").init(config);
```



