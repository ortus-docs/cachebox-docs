# AbstractEvictionPolicy

**class** : `cachebox.system.cache.policies.AbstractEvictionPolicy`

This is the abstract class that gives the magic to eviction policies under the CacheBox cache provider. It communicates with the internal object stores and asks for specific metadata in specific sorter orders so the policy can execute its algorithm. Our current algorithms are: _LRU,LFU, and FIFO_. However, you can very easily implement your own.
