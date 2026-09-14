# CacheBox Provider

The CacheBox provider is our very own enterprise cache implementation that has been part of the core since its initial baby step versions. Our caching engine has matured over the years and it has been proven effective, fast, scalable and very user friendly. Here are the two implementations for our CacheBox provider:

1. `CacheBoxProvider` : Our base CacheBox provider caching engine
2. `CacheBoxColdBoxProvider` : A subclass of `CacheBoxProvider` that enables caching operations for ColdBox applications

## Properties

| Key                                | Type           | Required | Default           | Description                                                                                                                                                                                                                    |
| ---------------------------------- | -------------- | -------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **ObjectDefaultTimeout**           | numeric        | false    | 60                | The default lifespan of an object in minutes                                                                                                                                                                                   |
| **ObjectDefaultLastAccessTimeout** | numeric        | false    | 30                | The default last access or idle timeout in minutes                                                                                                                                                                             |
| **UseLastAccessTimeouts**          | Boolean        | false    | true              | Use or not idle timeouts                                                                                                                                                                                                       |
| **ReapFrequency**                  | numeric        | false    | 2                 | The delay in minutes to produce a cache reap (Not guaranteed)                                                                                                                                                                  |
| **FreeMemoryPercentageThreshold**  | numeric        | false    | 0                 | The numerical percentage threshold of free JVM memory to have available before caching. If the JVM free memory falls below this setting, the cache will run the eviction policies in order to cache new objects. (0=Unlimited) |
| **MaxObjects**                     | numeric        | false    | 200               | The maximum number of objects for the cache                                                                                                                                                                                    |
| **EvictionPolicy**                 | string or path | false    | LRU               | The eviction policy algorithm class to use.\*                                                                                                                                                                                  |
| **EvictCount**                     | numeric        | false    | 1                 | The number of objects to evict once an execution of the policy is requested. You can increase this to make your evictions more aggressive                                                                                      |
| **objectStore**                    | string         | false    | _ConcurrentStore_ | ConcurrentStore     The object store to use for caching objects.\*\*                                                                                                                                                           |
| **ColdboxEnabled**                 | Boolean        | false    | false             | A flag that switches on/off the usage of either a plain vanilla CacheBox provider or a ColdBox enhanced provider. This must be true when used within a ColdBox application and it applies for the default cache ONLY.          |
| **resetTimeoutOnAccess**           | Boolean        | false    | false             | If true, then when cached objects are retrieved their timeout will be reset to its original value and thus elongating the survival strategy of the items. Much how session storages work.                                      |

### Eviction Policies

Coldbox ships with the following eviction policies

* **LRU** (Least Recently Used)
* **LFU** (Least Frequently Used)
* **FIFO** (First In First Out)
* **LIFO** (Last In First Out)
* **Custom**: You can also build your own and pass the instantiation path in this setting

### Object Stores

ColdBox ships with the following object stores:

* **ConcurrentStore** - Uses concurrent hash maps for increased performance
* **ConcurrentSoftReferenceStore** - Concurrent hash maps plus java soft references for JVM memory sensitivity
* **DiskStore** - Uses a physical disk location for caching (Uses java serialization for complex objects)
* **JDBCStore** - Uses a JDBC datasource for caching (Uses java serialization for complex objects)
* **Custom** : You can also build your own and pass the instantiation path in this setting

{% hint style="warning" %}
Please also note that each of the object stores can have extra configuration properties that you will need to set. So for that, let's delve a little deeper into object stores.
{% endhint %}

## Provider API Methods

All CacheBox providers implement the `ICacheProvider` interface. The table below covers the core methods available on any provider instance.

| Method | Description |
| --- | --- |
| `get( required objectKey )` | Get an object from cache; returns an empty value if not found or expired |
| `getQuiet( required objectKey )` | Get an object without touching access statistics |
| `getOrSet( required objectKey, required produce, [timeout], [lastAccessTimeout], [extra] )` | Get an object from cache, or produce it via the `produce` closure/UDF, cache it and return it if missing. See [Basic Usage](../basic-usage.md) |
| `set( required objectKey, required object, [timeout], [lastAccessTimeout], [extra] )` | Store an object in cache with optional timeout (minutes) |
| `setQuiet( required objectKey, required object, [timeout], [lastAccessTimeout], [extra] )` | Store an object without updating statistics |
| `clear( required objectKey )` | Remove a specific object from cache |
| `clearQuiet( required objectKey )` | Remove a specific object silently without throwing errors |
| `clearAll()` | Remove all objects from the cache |
| `lookup( required objectKey )` | Returns `true` if the key exists and has not expired |
| `lookupQuiet( required objectKey )` | Returns `true` if the key exists without touching statistics |
| `isExpired( required objectKey )` | Returns `true` if the cached object has expired |
| `expireAll()` | Mark all cached objects as expired |
| `expireObject( required objectKey )` | Force-expire a specific cached object |
| `getKeys()` | Get an array of all keys currently in the cache |
| `getCachedObjectMetadata( required objectKey )` | Get the metadata struct for a cached object (timeout, hits, created, etc.) |
| `getSize()` | Get the current number of objects in the cache |
| `reap()` | Run the cache reap routine to remove expired objects |
| `getStats()` | Get the `IStats` statistics object for this provider |
| `clearStatistics()` | Reset all statistics counters to zero |
| `getMemento()` | Get a struct representation of the provider's internal state (excludes functions) |
| `inThread()` | Returns `true` if executing inside a spawned thread |

For the bulk `getMulti()`/`setMulti()`/`clearMulti()`/`lookupMulti()`/`getCachedObjectMetadataMulti()` methods, see the [ICacheProvider](../../for-the-geeks/cachebox-architecture/icacheprovider.md) reference.

### Usage Examples

```javascript
// Get the default cache
cache = cachebox.getDefaultCache();

// Store an object for 60 minutes
cache.set( "myKey", myObject, 60 );

// Retrieve an object
value = cache.get( "myKey" );

// Get it from cache, or produce, cache and return it if missing
value = cache.getOrSet( "myKey", () => myService.produceExpensiveObject(), 60 );

// Check existence without retrieval
if ( cache.lookup( "myKey" ) ) {
    // key exists and is not expired
}

// Get metadata for a cached object
md = cache.getCachedObjectMetadata( "myKey" );
writeOutput( "Hits: #md.hits#, Created: #md.created#" );

// Remove a single key
cache.clear( "myKey" );

// Get current stats
stats = cache.getStats();
writeOutput( "Hit ratio: #stats.getCachePerformanceRatio()#" );
```
