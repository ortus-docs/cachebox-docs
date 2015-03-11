# CacheFactory

**class** : `coldbox.system.cache.CacheFactory`


The `CacheFactory` object is the most important object as it represents CacheBox. The class path for this object is `coldbox.system.cache.CacheFactory` or in standalone mode `cachebox.system.cache.CacheFactory`. 

This is the aggregator or cache overseer that you will interact with to get caches, shutdown caches, perform global cache operations, and startup your CacheBox instance. If you are using CacheBox within a ColdBox application context, then ColdBox does all the configurations and creations for you. It even links your ColdBox context, [LogBox](http://wiki.coldbox.org/wiki/LogBox.cfm) and ColdBox [interceptor](http://www.coldbox.org/documents/api/ColdBoxDocs-3.0.0/) service for you.
