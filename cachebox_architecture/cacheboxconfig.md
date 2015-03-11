# CacheBoxConfig

**class** : `cachebox.system.cache.config.CacheBoxConfig`

This is the required configuration object the `CacheFactory` object needs in order to start itself up. This configuration object can be created and then used to configure all your caches, listeners, scope registrations and logging. We will investigate all the types of configurations available but they all translate down to methods in this configuration object. Ways to configure CacheBox:

* Programmatically via method calls
* Programmatically via a CacheBox DSL or a CacheBox DSL CFC
* XML



```js
cacheBoxConfig = new cachebox.system.cache.config.CacheBoxConfig();
cachebox = new cachebox.system.cache.CacheFactory( cacheBoxConfig );
```