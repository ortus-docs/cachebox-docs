# CacheBox Provider Events

Each cache provider has the potential of announcing life cycle events as it implements it. If you are a cache provider author, then you can use the aggregated `EventManager` to register, process and announce events a-la-carte. So let's investigate each provider's life cycle events:

## CacheBoxProvider-CacheBoxColdBoxProvider Events

|Event|Data|Description|
|--|--|--|
| afterCacheElementUpdated | **cache**: the cache provider<br><br>**cacheNewObject**: the new object to cache<br><br>**cacheOldObject**: the object replaced | Called via a `set()` operation when there is already the same key in the cache. Called before the replacement occurs | 
| afterCacheElementInsert  | **cache**: the cache provider<br><br>**cacheObject**: the new object to cache<br><br>**cacheObjectKey**: the key used to store the object<br><br>**cacheObjectTimeout**: the timeout used<br><br>**cacheObjectLastAccessTimeout**:the last access timeout used | Called after a new cache element has been inserted into the cache|
| afterCacheElementRemoved | **cache**: the cache provdier<br><br>**cacheObjectKey**: the key of the removed object | Called after a cache element has been removed from the cache|
| afterCacheClearAll 	   | **cache**: the cache provider | Called after a `clearAll()` has been issued on the cache|
| afterCacheElementExpired | **cache**: the cache provider<br><br>**cacheObjectKey**: the key of the expired object | Called after a cache element has been expired from the cache|

## CFProvider-CFColdboxProvider Events

|Event|Data|Description|
|--|--|--|
| afterCacheElementInsert 	| **cache**: the cache provider<br><br> **cacheObject**: the new object to cache<br><br> **cacheObjectKey**: the key used to store the object<br><br>**cacheObjectTimeout**: the timeout used<br><br>**cacheObjectLastAccessTimeout**: the last access timeout used|Called after a new cache element has been inserted into the cache|
| afterCacheElementRemoved	| **cache**: the cache provider<br><br> **cacheObjectKey**: the key of the removed object|Called after a cache element has been removed from the cache|
| afterCacheClearAll		| **cache**: the cache provider|Called after a `clearAll()` has been issued on the cache|
