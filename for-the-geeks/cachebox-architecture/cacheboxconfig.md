# CacheBoxConfig

**class** : `cachebox.system.cache.config.CacheBoxConfig`

This is the required configuration object the `CacheFactory` object needs in order to start itself up. This configuration object can be created and then used to configure all your caches, listeners, scope registrations and logging. We will investigate all the types of configurations available but they all translate down to methods in this configuration object. Ways to configure CacheBox:

* Programmatically via method calls
* Programmatically via a CacheBox DSL or a CacheBox DSL CFC

```javascript
config = new cachebox.system.cache.config.CacheBoxConfig();
cachebox = new cachebox.system.cache.CacheFactory( config );
```

## Configuration Methods

| Method | Description |
| --- | --- |
| `scopeRegistration( [boolean enabled=true], [string scope="server"], [string key="cachebox"] )` | Configure scope-based persistence for the factory instance |
| `defaultCache( objectDefaultTimeout, objectDefaultLastAccessTimeout, reapFrequency, maxObjects, freeMemoryPercentageThreshold, useLastAccessTimeouts, evictionPolicy, evictCount, objectStore, coldboxEnabled )` | Set properties for the default cache region |
| `cache( required string name, [string provider="cachebox.system.cache.providers.CacheBoxProvider"], [struct properties={}] )` | Register a named cache with an optional provider class and properties |
| `listener( required string class, [struct properties={}], [string name=""] )` | Register a CacheBox event listener class |
| `logBoxConfig( required string config )` | Set a custom LogBox configuration CFC path |
| `reset()` | Reset all configuration back to defaults |
| `validate()` | Validate the configuration object; throws a descriptive exception on error |
