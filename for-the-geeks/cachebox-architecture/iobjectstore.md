# IObjectStore

**class** : `cachebox.system.cache.store.IObjectStore`

A CacheBox cache provider uses the concept of an object store in order to, well, store its cached objects. This can be anything as we have created an interface that anybody can implement and create their own object storages. Just be aware that the CacheBox provider's eviction policies use certain methods for reporting and evictions that MUST be implemented.

## Interface Methods

| Method | Description |
| --- | --- |
| `flush()` | Flush the store to disk or finalize any pending write operations |
| `reap()` | Reap expired objects from the store |
| `clearAll()` | Remove all objects from the store |
| `getKeys()` | Get an array of all cached object keys |
| `lookup( required objectKey )` | Check whether an object key exists in the store |
| `get( required objectKey )` | Get an object from the store |
| `getQuiet( required objectKey )` | Get an object without touching access statistics |
| `expireObject( required objectKey )` | Force-expire an object in the store |
| `isExpired( required objectKey )` | Check whether a stored object has expired |
| `set( required objectKey, required object, [timeout], [lastAccessTimeout], [extra] )` | Store an object with optional timeout settings |
| `clear( required objectKey )` | Remove an object from the store |
| `getSize()` | Get the total number of objects in the store |
| `getSortedKeys( required string property, required string sortType, required string sortOrder )` | Get all object keys sorted by a metadata property; **required** by eviction policy implementations |
