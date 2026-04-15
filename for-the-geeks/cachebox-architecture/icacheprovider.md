# ICacheProvider

**class** : `cachebox.system.cache.ICacheProvider`

This is the main interface that each caching engine implementation must implement in order for CacheBox to aggregate it and use it. Each implementation can add additional functionality and methods but this is the core contract that each provider must adhere to. CacheBox aggregates 1 or more instances of CacheProviders that implement this interface. You can find all of our CacheBox cache providers in the following location:

```javascript
/cachebox/system/cache/providers
```

## Interface Methods

| Method | Description |
| --- | --- |
| `configure()` | Configure the cache provider for operation |
| `shutdown()` | Shutdown the cache provider and release resources |
| `get( required objectKey )` | Get an object from cache; returns an empty value if not found or expired |
| `getQuiet( required objectKey )` | Get an object without touching access statistics |
| `set( required objectKey, required object, [timeout], [lastAccessTimeout], [extra] )` | Store an object in cache with optional timeout settings |
| `setQuiet( required objectKey, required object, [timeout], [lastAccessTimeout], [extra] )` | Store an object without updating statistics |
| `clear( required objectKey )` | Remove a specific object from cache |
| `clearQuiet( required objectKey )` | Remove a specific object without throwing errors |
| `clearAll()` | Remove all objects from the cache |
| `lookup( required objectKey )` | Check whether a key exists in cache and has not expired |
| `lookupQuiet( required objectKey )` | Check for a key without touching access statistics |
| `isExpired( required objectKey )` | Check whether a specific cached object has expired |
| `expireAll()` | Mark all cached objects as expired |
| `expireObject( required objectKey )` | Force-expire a specific cached object |
| `getKeys()` | Get an array of all keys currently in the cache |
| `getCachedObjectMetadata( required objectKey )` | Get the metadata struct for a cached object (timeout, hits, created, etc.) |
| `getSize()` | Get the current number of objects in the cache |
| `reap()` | Run the cache reap routine to remove expired objects |
| `getStats()` | Get the `IStats` statistics object for this provider |
| `clearStatistics()` | Reset all statistics counters to zero |
