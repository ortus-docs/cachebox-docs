# CacheFactory

**class** : `cachebox.system.cache.CacheFactory`

The `CacheFactory` object is the most important object as it represents CacheBox. The class path for this object is `coldbox.system.cache.CacheFactory` or in standalone mode `cachebox.system.cache.CacheFactory`.

This is the aggregator or cache overseer that you will interact with to get caches, shutdown caches, perform global cache operations, and startup your CacheBox instance. If you are using CacheBox within a ColdBox application context, then ColdBox does all the configurations and creations for you. It even links your ColdBox context, [LogBox](http://logbox.ortusbooks.com) and ColdBox Intercepting service for you.

```javascript
cachebox = new cachebox.system.cache.CacheFactory();
```

## Public API

| Method | Description |
| --- | --- |
| `configure( required CacheBoxConfig config )` | Configure the factory for operation; called automatically by `init()` |
| `getCache( required string name )` | Get a reference to a registered cache by name |
| `getDefaultCache()` | Get the default cache provider |
| `addCache( required ICacheProvider cache )` | Register a new instantiated cache provider with the factory |
| `addDefaultCache( required string name )` | Create, configure, register, and return a new cache using the default settings |
| `createCache( required name, required provider, struct properties )` | Create a new cache from the given provider class path and properties, register it with the factory, and return it |
| `cacheExists( required name )` | Check if a cache with the given name is already registered |
| `getCacheNames()` | Get an array of the names of all currently registered caches |
| `isColdBoxLinked()` | Check if this factory instance is linked to a ColdBox application controller |
| `getScopeRegistration()` | Get the scope registration configuration struct for this factory |
| `removeCache( required string name )` | Remove a named cache from the factory and shut it down |
| `removeAll()` | Remove and shutdown all registered caches from the factory |
| `replaceCache( required ICacheProvider cache, required ICacheProvider decoratedCache )` | Replace a registered named cache with a decorated version of the same name |
| `registerListeners()` | Register all configured event listeners from the configuration with the ColdBox Interceptor Service |
| `shutdownCache( required string name )` | Shutdown a specific named cache provider and remove it from the factory |
| `removeFromScope()` | Remove the factory from scope registration if scope registration is enabled |
| `shutdown()` | Recursively send shutdown commands to all registered caches and clean up |
| `reapAll()` | Call `reap()` on all registered caches |
| `expireAll()` | Expire all objects in all registered caches without de-registration |
| `clearAll()` | Clear all objects in all registered caches without de-registration |

The factory is declared with `accessors=true`, so it also exposes standard getters for its internal properties: `getFactoryId()`, `getVersion()`, `getConfig()`, `getCaches()`, `getEventManager()`, `getAsyncManager()`, and `getTaskScheduler()`.
