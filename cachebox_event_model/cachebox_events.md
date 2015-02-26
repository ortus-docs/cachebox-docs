# CacheBox Events

CacheBox's aggregation functionality offers a wide gamut of life cycle events that are announced at certain points in execution time. Below are the current events announced by the CacheBox *CacheFactory*. Remember, this is the *CacheFactory* and not a *CacheBox Cache Provider*.

|Event|Data|Description|
|--|--|--|
|afterCacheRegistration | cache: the registered reference||
|beforeCacheRemoval |cach: the cahce reference to remove|Called before a removeCache() operation is called on CacheBox|
|afterCacheRemoval |cache: the cache name|Called after the cache has been removed from CacheBox. You receive only the name of the cache removed.|
|beforeCacheReplacement | *oldCache*: the cache reference to replace<br><br>*newCache*: the new cache reference to replace with |Called right before a cache is replaced with another cache in CacheBox.|
|afterCacheFactoryConfiguration |cacheFactory: A reference to the CacheBox factory created|Called after a CacheBox instance has been created, configured and started up. This is a great interception point for creating cache loaders or on startup scripts.|
|beforeCacheFactoryShutdown |cacheFactory: A reference to the CacheBox factory created|Called right before the CacheBox instance is shutdown gracefully|
|afterCacheFactoryShutdown |cacheFactory: A reference to the CacheBox factory created|Called right after the CacheBox instance has been shutdown gracefully|
|beforeCacheShutdown |cache: A reference to the cache shutdown|Called right before a specific cache provider is shutdown by CacheBox Factory|
|afterCacheShutdown |cache: A reference to the cache that was shutdown|Called right after a specific cache provider has been shut down by CacheBox Factory and before its removed|
