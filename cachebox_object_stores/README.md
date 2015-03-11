# CacheBox Object Stores

CacheBox offers the capability of object stores that can be used to store cached objects. If you look at the following figure you will understand our object model for our object stores:

<img src="../images/cachebox_majorclasses.png">

Each object store is composed into a CacheBox provider for usage of storing and retrieving cached objects. The design principle behind each object store is that each object store implements its own locking, serialization, reading and writing mechanisms that are fronted by a nice API via the `CacheBoxProvider` object. Also, it is very important to note that the CacheBox eviction policies talk to the object stores in order to get ordered data structures for eviction purposes.

So if you will be creating your own object stores, make sure they implement the right data methods the eviction policies can use for evictions. Also, the CacheBox provider's reaping methods use the object stores in order to get metadata out of the object stores in order to take care of cleanup, expirations and evictions. We definitely encourage you to take a look at the written object store implementations in order to learn how this works. So let's start investigating each of the object stores that are shipped with CacheBox.

> **Important** Please note that each object store can have extra properties that need to be set in your cache configuration file.


