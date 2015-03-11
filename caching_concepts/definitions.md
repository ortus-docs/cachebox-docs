# Definitions

* **Cache Hit** : An event that occurs when an element requested from cache is found in the cache.
* **Cache Miss** : An event that occurs when an element requested form cache is NOT found in the cache.
* **Eviction** : The act of removing an element from the cache due to certain criteria algorithm that directly is connected to the state of the element.
* **Eviction Policy** : The algorithm that decides what element(s) will be evicted from a cache when full or a certain criteria has been met in the cache. (Cache Algorithms)
* **LRU** : An eviction policy that discards the least recently used items first.
* **LFU** : An eviction policy that counts how often an item has been accessed and it will discard the items that have been used the least.
* **FIFO** : An eviction policy that works as a queue, first object in will be the first object out of the cache. So older staler objects are purged.
* **Cache Provider** : A concrete implementation to a caching engine within CacheBox
* **Object Store** : An object that stores cached elements and indexes them
* **Idle or Last Access Timeout** : An expiration time an element receives if it is not accessed.
* **Reap** : Usually an asynchronous event that cleans a cache from dead elements or expired elements
* **Distributed/Partitioned Cache** : A form of caching that allows the cache to span multiple servers so that it can grow in size and in capacity. Each machine contains a unique partition of the dataset. Adding machines to the cluster will increase the capacity of the cache. Both read and write access involve network transfer and serialization/deserialization.
* **Near Cache** : Each cache server contains a small local cache which is synchronized with a larger distributed/partitioned cache, optimizing read performance. There is some overhead involved with synchronizing the caches.
* **Replicated** : Each cache server contains a full copy of the elements cached
* **In Process Cache** : A cache that lives inside of the same heap as the application using it.
* **Out of Process Cache** : A cache that lives as its own process and heap in the most likely the same server as the application using it.
* **Eternal Objects** : Eternal objects are objects that will never be purged or evicted by the caching engine automatically. The only way to remove them is to recreate the cache or clear them manually.
* **Cache Topology** : A concept that refers to where data physically resides and how it is accessed in a distributed environment

