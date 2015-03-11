# CacheBox Config Object

The previous CacheBox DSL is a great way to configure CacheBox as it is very portable. However, you can also configure CacheBox by calling methods on the CacheBoxConfig object, which is exactly what we do when we read the CacheBox DSL. 

Below are the main methods used for configuring CacheBox which match exactly to the DSL items, so please refer to the DSL items for definitions and settings. Also, for all the methods in this object, check out the [API Docs](http://apidocs.ortussolutions.com/cachebox/current)

* init([string XMLConfig=], [any CFCConfig], [string CFCConfigPath])

The constructor

* cache(string name, [string provider=], [struct properties={}])

Add a new cache configuration
* defaultCache([numeric objectDefaultTimeout=], [numeric objectDefaultLastAccessTimeout=], [numeric reapFrequency=], [numeric maxObjects=], [numeric freeMemoryPercentageThreshold=], [boolean useLastAccessTimeouts=], [string evictionPolicy=], [numeric evictCount=], [string objectStore=], [boolean coldboxEnabled=])

Add a default cache configuration
* listener(string class, [struct properties={}], [string name=])

Add a new listener configuration
* logBoxConfig(string config)

Set the logBox Configuration path to use
* reset()

Reset the entire configuration
* scopeRegistration([boolean enabled='false'], [string scope='application'], [string key='cachebox'])

Use to define cachebox factory scope registration

Code Examples:

```javascript
config = createObject("component","cacheBox.system.cache.config.CacheBoxConfig").init();

// logbox config & scope chained, yes you can chain any method
config.logBoxConfig("MyLogBox.xml").scopeRegistration(true,"application","cacheBox");

// default cache
config.default(maxObjects=500,evictCount=5,objectDefaultTimeout=30);

// Caches
config.cache("ehCache","caches.ehCacheProvider",{configFile="ehCache.xml"}).
    cache("template","cachebox.system.cache.providers.CacheBoxProvider");

// Listeners
config.listener("myapp.model.MyListener","FunkyListener",{});
```

