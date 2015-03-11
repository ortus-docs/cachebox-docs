# ColdBox Application Configuration

The default configuration file for CacheBox within ColdBox applications can be found here

```javascript
/coldbox/system/web/config/CacheBox.cfc
```

This configuration file configures CacheBox with two caches: 
* `default`
* `template`

The `default` cache can be used for any type of data caching or object persistence. The `template` cache is used for event caching and view fragment caching. It is also important to note that the `template` cache uses the `ConcurrentSoftReferenceStore` for its objects and the `default` cache uses the `ConcurrentStore` for its objects. 

This means that event/view caching is subject to available memory via the JVM, a memory sensitive cache. This is essential as you could have lots of events being cached and you want to be considerate with memory concerns. It is also limited to 300 objects.

Now, this is all nice and dandy, but what if I want to configure CacheBox "MY WAY!!"? Well, don't shout, we are just getting there. There are several ways you can configure CacheBox from within your applications, so chose wisely.


