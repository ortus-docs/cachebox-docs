# CacheBox Eviction Policies

The CacheBox Provider offers several eviction policies that are used to evict objects from cache when certain situations occur within the cache environment. Again, these eviction policies are only for the CacheBox Cache provider. These eviction situations can include:

* Maximum objects reached
* JVM memory threshold reached
* Manual eviction executions

Below is a refresher on what an eviction policy means:

> Eviction Policy: The algorithm that decides what element(s) will be evicted from a cache when full or a certain criteria has been met in the cache. (Cache Algorithms)

Please note that when a cache element is evicted from the cache it usually is expired first so it can be gracefully collected when the CacheBox reaping procedures occur. Therefore, you might see sometimes that the cache actually goes above the maximum objects defined, this is normal.

> **Caution** Please note that no eternal objects are ever evicted from the CacheBox provider. Eternal objects live as long as the CacheBox instance lives for (most likely application scope timeout). So please take that into consideration.

ColdBox ships with the following eviction policies:

|Policy|Description|
|--|--|
|LRU (Least Recently Used) |With this eviction policy, the cache discards the least recently used items first. *This is the default policy*|
|LFU (Least Frequently Used) |This policy counts how often an item has been accessed and it will discard the items that have been used the least.|
|FIFO (First In First Out) |Just like it sounds, first one in, first one out. Great for implementing sized queues|
|FIFO (First In First Out) |Just like it sounds, first one in, first one out. Great for implementing sized queues|
|LIFO (Last In First Out) |Just like it sounds, last one in, first one out. Great for implementing sized stacks or timed stacks|
