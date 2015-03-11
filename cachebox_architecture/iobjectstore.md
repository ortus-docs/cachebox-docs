# IObjectStore

**class** : `cachebox.system.cache.store.IObjectStore`

A CacheBox cache provider uses the concept of an object store in order to, well, store its cached objects. This can be anything as we have created an interface that anybody can implement and create their own object storages. Just be aware that the CacheBox provider's eviction policies use certain methods for reporting and evictions that MUST be implemented.

