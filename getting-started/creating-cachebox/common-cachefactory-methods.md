# Common CacheFactory Methods

Here is a list of some of the most common methods you can use to interact with CacheBox. For full details, please view the online [API Docs](http://apidocs.ortussolutions.com/cachebox/current)

* `addCache(any<ICacheProvider> cache)`

Register a new instantiated cache with this cache factory

* `addDefaultCache(string name)`

Add a default named cache to our registry, create it, config it, register it and return it of type: `cachebox`

* `cacheExists(string name)`

Check if a cache with the given name is already registered with this factory

* `createCache(string name, string provider, struct properties)`

Create a new cache using the given provider class path and configuration `properties`, register it with the factory, and return it of type `ICacheProvider`. This is a lower-level alternative to `addDefaultCache()` when you need a non-default provider

* `clearAll()`

Clears all the elements in all the registered caches without de-registrations

* `configure(CacheBoxConfig config)`

Configure the cache factory for operation, called by the init()

* `expireAll()`

Expires all the elements in all the registered caches without de-registrations

* `getCache(string name)`

Get a reference to a registered cache in this factory

* `getDefaultCache()`

Get the default cache provider of type cachebox

* `getCacheNames()`

Get an array of the names of all caches currently registered with this factory

* `isColdBoxLinked()`

Check if this CacheFactory instance is linked to a ColdBox application controller

* `getScopeRegistration()`

Get the scope registration configuration struct used to register this factory in a runtime scope (e.g. application/server scope)

* `reapAll()`

A nice way to call reap on all registered caches

* `removeCache(string name)`

Try to remove a named cache from this factory

* `removeAll()`

Remove and shutdown all registered caches from this factory

* `replaceCache(any<ICacheProvider> cache, any<ICacheProvider> decoratedCache)`

Replace a registered named cache with a new decorated cache of the same name

* `registerListeners()`

Register all configured event listeners found in the configuration file with the ColdBox Interceptor Service

* `shutdownCache(string name)`

Send a shutdown command to a specific named cache provider and remove it from the factory

* `removeFromScope()`

Remove the CacheBox factory from scope registration if scope registration is enabled

* `shutdown()`

Recursively sends shutdown commands to all registered caches and cleans up in preparation for shutdown

## Common Operation Examples

```javascript
// Add another default cache type but with the name FunkyCache
funkyCache = cachebox.addDefaultCache("FunkyCache");
// Add some elements to funky Cache
funkyCache.set("Myentry",now(),"20");

// Get a reference to a named cache
cfCache = cacheBox.getCache("CFCache");

// Get a reference to the default named cache
cache = cacheBox.getDefaultCache();

// Remove our funky cache no longer needed
cacheBox.removeCache("FunkyCache");

// Create a new cache a replace a cache, the MyFunkyFunkyCache implements ICacheProvider
newCache = new MyFunkyFunkyCache({maxObjects=200,timeout=30});
// replace the CFCache with this one
cacheBox.replaceCache( "CFCache", newCache );

// Add a new cache to cachebox programmatically
newCache = new MyFunkyFunkyCache("FunkynessCache", {maxObjects=200,timeout=30});
cacheBox.addCache( newCache );

// Send a shutdown command to cachebox
cachebox.shutdown();
```

> **Info** Remember that some of the CacheBox methods announce events. So please see our event model section to see what kind of events you can listen to when working with CacheBox.

## Property Accessors

The `CacheFactory` is declared with `accessors=true`, so it also exposes standard getters for its internal properties: `getFactoryId()`, `getVersion()`, `getConfig()`, `getCaches()`, `getEventManager()`, `getAsyncManager()`, and `getTaskScheduler()`.
