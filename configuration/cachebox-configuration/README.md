# CacheBox Configuration

CacheBox comes pre-configured for operation for caching using a `default` cache.  However, you can customize CacheBox using different strategies by levarging the [CacheBox Configuration DSL](cachebox-dsl/).

When you are in a ColdBox application, you will have a `cachebox` structure in your `ColdBox.cfc` already that you can use, or you can create a portable CFC as well and place it in `config/CacheBox.cfc`

{% hint style="success" %}
The cool thing about this CacheBox DSL is that it is the same whether you are using CacheBox in ColdBox applications or any other framework or non-framework ColdFusion application.&#x20;
{% endhint %}

Configuration can be done in the following ways:

1. **No configuration:** Uses the _default configuration_ shown below
2. **Portable CFC:** Creating a portable data CFC using the CacheBox DSL in a `configure()` method
3. **Programmatic Config:** Creating the CacheBox`Config` object and interacting with its methods programmatically
4. **CacheBox DSL Struct:** Passing a struct literal into CacheBox, using the CacheBox DSL.

{% content-ref url="cachebox-dsl/" %}
[cachebox-dsl](cachebox-dsl/)
{% endcontent-ref %}

### 1. Default Configuration

This is the default configuration when CacheBox is created with no config.  CacheBox will

* Use a default LogBox configuration to the console
* Register CacheBox in the CFML `application` scope as `cachebox`
* Create a `defaultcache` using `ConcurrentSoftReferenceStore` storage

```cfscript
/**
 * Copyright Since 2005 ColdBox Framework by Luis Majano and Ortus Solutions, Corp
 * www.ortussolutions.com
 * ----
 * The default ColdBox CacheBox configuration object that is used when the cache factory is created by itself
 **/
component {

/**
 * Configure CacheBox, that's it!
 */
function configure(){
    // The CacheBox configuration structure DSL
    cacheBox = { 
	// LogBox Configuration file
	logBoxConfig      : "coldbox.system.cache.config.LogBox",
	// Scope registration, automatically register the cachebox factory instance on any CF scope
	// By default it registers itself on server scope
	scopeRegistration : {
		enabled : true,
		scope   : "application", // the cf scope you want
		key     : "cacheBox"
	},
	// The defaultCache has an implicit name of "default" which is a reserved cache name
	// It also has a default provider of cachebox which cannot be changed.
	// All timeouts are in minutes
	// Please note that each object store could have more configuration properties
	defaultCache : {
		objectDefaultTimeout           : 120,
		objectDefaultLastAccessTimeout : 30,
		useLastAccessTimeouts          : true,
		reapFrequency                  : 2,
		freeMemoryPercentageThreshold  : 0,
		evictionPolicy                 : "LRU",
		evictCount                     : 1,
		maxObjects                     : 300,
		objectStore                    : "ConcurrentSoftReferenceStore",
		// This switches the internal provider from normal cacheBox to coldbox enabled cachebox
		coldboxEnabled                 : false
	},
	// Register all the custom named caches you like here
	caches    : {},
	// Register all event listeners here, they are created in the specified order
	listeners : [
		 // { class="", name="", properties={} }
	]
    };
}

}
```



### 2. Portable CFC

You can create a CFC with a single `configure` method with the CacheBox configuration in a variable called `cachebox` using the CacheBox DSL.

```cfscript
component{
/**
 * Configure CacheBox for ColdBox Application Operation
 */
function configure(){
    // The CacheBox configuration structure DSL
    cacheBox = {
	// LogBox config already in coldbox app, not needed
	// logBoxConfig = "coldbox.system.web.config.LogBox",

	// The defaultCache has an implicit name "default" which is a reserved cache name
	// It also has a default provider of cachebox which cannot be changed.
	// All timeouts are in minutes
	defaultCache : {
		objectDefaultTimeout           : 120, // two hours default
		objectDefaultLastAccessTimeout : 30, // 30 minutes idle time
		useLastAccessTimeouts          : true,
		reapFrequency                  : 5,
		freeMemoryPercentageThreshold  : 0,
		evictionPolicy                 : "LRU",
		evictCount                     : 1,
		maxObjects                     : 300,
		objectStore                    : "ConcurrentStore", // guaranteed objects
		coldboxEnabled                 : true
	},
	// Register all the custom named caches you like here
	caches : {
		// Named cache for all coldbox event and view template caching
		template : {
			provider   : "coldbox.system.cache.providers.CacheBoxColdBoxProvider",
			properties : {
				objectDefaultTimeout           : 120,
				objectDefaultLastAccessTimeout : 30,
				useLastAccessTimeouts          : true,
				freeMemoryPercentageThreshold  : 0,
				reapFrequency                  : 5,
				evictionPolicy                 : "LRU",
				evictCount                     : 2,
				maxObjects                     : 300,
				objectStore                    : "ConcurrentSoftReferenceStore" // memory sensitive
			}
		}
	}
    };

    // Add caches per engine
    if ( listFindNoCase( "Lucee", server.coldfusion.productname ) ) {
	cachebox.caches.luceeCache = { provider : "coldbox.system.cache.providers.LuceeProvider" };
    } else {
	cachebox.caches.cfCache = { provider : "coldbox.system.cache.providers.CFColdBoxProvider" };
    }
}
}
```

### 3. Programmatic Config

You can create an instance of the `cachebox.system.cache.config.CacheBoxConfig` and calling methods on it.

```cfscript
config = new cachebox.system.cache.config.CacheBoxConfig()
    .scopeRegistration( true )
    .defaultCache( maxObjects : 200, objectStore : "ConcurrentStore" );
    
new cachebox.system.cache.CacheFactory( config );
```



### 4. Struct Literal Config

You can also use a struct literal to configure CacheBox

```cfscript
new cachebox.system.cache.CacheFactory( {
	// LogBox Configuration file
	logBoxConfig      : "coldbox.system.cache.config.LogBox",
	// Scope registration, automatically register the cachebox factory instance on any CF scope
	// By default it registers itself on server scope
	scopeRegistration : {
		enabled : true,
		scope   : "application", // the cf scope you want
		key     : "cacheBox"
	},
	// The defaultCache has an implicit name of "default" which is a reserved cache name
	// It also has a default provider of cachebox which cannot be changed.
	// All timeouts are in minutes
	// Please note that each object store could have more configuration properties
	defaultCache : {
		objectDefaultTimeout           : 120,
		objectDefaultLastAccessTimeout : 30,
		useLastAccessTimeouts          : true,
		reapFrequency                  : 2,
		freeMemoryPercentageThreshold  : 0,
		evictionPolicy                 : "LRU",
		evictCount                     : 1,
		maxObjects                     : 300,
		objectStore                    : "ConcurrentSoftReferenceStore",
		// This switches the internal provider from normal cacheBox to coldbox enabled cachebox
		coldboxEnabled                 : false
	}
} );
```
