# Common CacheFactory Methods

Here is a list of some of the most common methods you can use to interact with CacheBox. For full details, please view the online [API Docs](http://apidocs.ortussolutions.com/cachebox/current)

* `addCache(any<ICacheProvider> cache)`

Register a new instantiated cache with this cache factory

* `addDefaultCache(string name)`

Add a default named cache to our registry, create it, config it, register it and return it of type: `cachebox`

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

* `reapAll()`

A nice way to call reap on all registered caches

* `removeCache(string name)`

Try to remove a named cache from this factory

* `replaceCache(any<ICacheProvider> cache, any<ICacheProvider> decoratedCache)`

Replace a registered named cache with a new decorated cache of the same name

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
