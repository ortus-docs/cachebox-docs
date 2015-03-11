# ICacheProvider

**class** : `cachebox.system.cache.ICacheProvider`

This is the main interface that each caching engine implementation must implement in order for CacheBox to aggregate it and use it. Each implementation can add additional functionality and methods but this is the core contract that each provider must adhere to. CacheBox aggregates 1 or more instances of CacheProviders that implement this interface. You can find all of our CacheBox cache providers in the following location:

```javascript
/coldbox/system/cache/providers
or
/cachebox/system/cache/providers
```


