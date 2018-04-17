# Cache Cleanup/Reaping

If you are using CacheBox within a ColdBox application, ColdBox is in charge of emitting reaping or cleanup requests to the CacheBox factory. However, if you are using the standalone version of the cache, then you will need to emit this command yourself in the desired execution point. We would suggest to do this on every request. This does not mean that the request executes every time, it means that the trigger is made and if the reaping time has been elapsed, then the caches clean themselves \(**CacheBox Providers Only!**\):

```javascript
cachebox.reapAll();
```

That's it! Just call on the _reapAll\(\)_ method and this will make sure that your caches clean themselves according to the reaping frequency selected in your configuration file.

> **Info**: Reaping frequency and cleanup only applies to the CacheBox Provider.

