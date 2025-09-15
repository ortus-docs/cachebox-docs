# CacheBox DSL

As we have seen, the CacheBox DSL can be used in different contexts:

* Portable CFC with a `configure()` method in a `cachebox` variable
* ColdBox config inside the `configure()` method in a `cachebox` variable
* A struct literal is sent into the constructor of CacheBox

No matter how you dice it, it's the same CacheBox Config DSL:

```javascript
**
* A CacheBox configuration data object
*/
component{

    function configure(){
        cacheBox = {
        
            logBoxConfig : "",
            
            scopeRegistration : {},
            
            defaultCache : {},
            
            caches : {}
            
            listeners : {}

        };
    }
}
```

## Base Config

The `cacheBox` structure can be configured with the following keys:

<table data-header-hidden><thead><tr><th width="226">Key</th><th width="113">Required</th><th>Description</th></tr></thead><tbody><tr><td>Key</td><td>Required</td><td>Description</td></tr><tr><td><code>logBoxConfig</code></td><td>false</td><td>The instantiation or location of a LogBox configuration file. This is only for standalone operations.</td></tr><tr><td><code>scopeRegistration</code></td><td>false</td><td>A structure that enables scope registration of the CacheBox factory in either server, cluster, application, or session scope.</td></tr><tr><td><code>defaultCache</code></td><td>true</td><td>The configuration of the default cache which will have an implicit name of default which is a reserved cache name. It also has a default provider of CacheBox which cannot be changed.</td></tr><tr><td><code>caches</code></td><td>true</td><td>A structure where you can create more named caches for usage in your CacheBox factory.</td></tr><tr><td><code>listeners</code></td><td>false</td><td>An array that will hold all the listeners you want to configure at startup time for your CacheBox instance. If you are running CacheBox within a ColdBox application, this item is not necessary as you can register them via the main ColdBox interceptors section.</td></tr></tbody></table>



### LogBoxConfig

```javascript
// LogBox config path
logBoxConfig : "myapp.config.MyLogBoxConfig",
```

The LogBoxConfig element is used only in a standalone mode of operation and tells CacheBox what configuration file to load into LogBox.&#x20;

{% hint style="info" %}
[LogBox](http://logbox.ortusbooks.com) is an enterprise ColdFusion (CFML) logging library
{% endhint %}

By default, CacheBox will instantiate LogBox with its default configuration file located at: `cachebox.system.cache.config.LogBox.cfc` which logs to the console.

###

### Scope Registration

```javascript
scopeRegistration = {
    enabled = true,
    scope   = "application",
    key     = "cacheBox"
},
```

This configuration allows CacheBox to be placed automatically upon construction in your specified scope.  By default, CacheBox registers itself in `application` scope with a key of `cachebox`



<table data-header-hidden><thead><tr><th width="135">Key</th><th width="102">Type</th><th width="107">Required</th><th width="125">Default</th><th>Description</th></tr></thead><tbody><tr><td>Key</td><td>Type</td><td>Required</td><td>Default</td><td>Description</td></tr><tr><td><code>enabled</code></td><td>boolean</td><td>false</td><td><em>true</em></td><td>Enable scope registration</td></tr><tr><td><code>scope</code></td><td>string</td><td>false</td><td><em>application</em></td><td>The ColdFusion scope to persist on</td></tr><tr><td><code>key</code></td><td>string</td><td>false</td><td><em>cachebox</em></td><td>The name of the key in the ColdFusion scope to persist on</td></tr></tbody></table>

###

### DefaultCache

```javascript
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
```

Every CacheBox instance has a `default` cache that can be configured as you like.  Above you can see the default configuration for the cache.

{% hint style="warning" %}
This is a reserved cache name, and it is MANDATORY to declare, and its name or provider type cannot be changed.
{% endhint %}

However, if you are using CacheBox within a ColdBox application, the provider will switch itself to `cachebox.system.cache.providers.CacheBoxColdBoxProvider` by using the `coldboxEnabled` key.

#### `objectDefaultTimeout` : numeric

The default lifespan of an object is in minutes.  This is how long an object lives within the cache.  If this value is `0` then all objects will be _eternal_, meaning they will live forever.

#### `objectDefaultLastAccessTimeout` : numeric

The default last access or idle timeout in minutes.  If an object has not been accessed within this time limit since the last access, then it will be marked for purging.

#### `useLastAccessTimeouts` : boolean

By default, the last access timeout is enabled.  You can disable this purging feature if you desire.

#### `resetTimeoutOnAccess` : boolean

If **true**, then when cached objects are retrieved their timeout will be reset to its original value thus elongating the survival strategy of the items. Much how session storages work on JEE.  The default is **false**, meaning the timeout will NOT be reset on each access.

#### `reapFrequency` : numeric

Every CacheBox provider has its own executor service with a reaping task executing under this frequency.  This is how often the cache is inspected to purge old/invalid keys.

#### `freeMemoryPercentageThreshold` : numeric

The numerical percentage threshold of free JVM memory to be available before caching. If the JVM free memory falls below this setting, the cache will run the eviction policies to cache new objects.  If you set this value to be `0` , there will be no free memory checks.

#### `evictionPolicy` : string

The eviction policy algorithm to use.  The available algorithms are:

* LFU
* **LRU - Default**
* LIFO
* FIFO
* Custom

#### `evictCount` : numeric

The number of objects to evict once an execution of the policy is requested. You can increase this to make your evictions more aggressive.  By default, one object is purged from the cache. However, you can increase it to purge more than one as needed.

#### `maxObjects` : numeric

The maximum number of objects the cache can have, give or take, expired objects. Once a limit is reached, the cache will start purging objects using the eviction policy and counts.  The default is 300.

#### `coldboxEnabled` : boolean

A flag that switches on/off the usage of either a plain vanilla CacheBox provider or a ColdBox enhanced provider. This must be **true** when used within a ColdBox application and applies to the default cache ONLY.  For standalone mode, ignore this or always set it to false.

#### `objectStore` : string

Each CacheBox provider can have a strategy of where to store the objects.  These are called object stores.  The value here is the name of the store.  By [default](../../../usage/cachebox-object-stores/concurrentsoftreferencestore.md), we use the `ConcurrentSoftReferenceStore`.

<table><thead><tr><th width="289">Store</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../../usage/cachebox-object-stores/blackholestore.md">BlackHoleStore</a></td><td>Used for mocking. Objects go nowhere!</td></tr><tr><td><a href="../../../usage/cachebox-object-stores/concurrentsoftreferencestore.md">ConcurrentSoftReferenceStore</a></td><td>Objects are kept in a <a href="https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html">concurrent hashmap</a> but wrapped in a Java <a href="https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/ref/SoftReference.html">SoftReference</a> object, which can sense the JVM's memory.  Meaning it can auto-reap if the JVM desires it.</td></tr><tr><td><a href="../../../usage/cachebox-object-stores/concurrentstore.md">ConcurrentStore</a></td><td>Objects are kept in a <a href="https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html">concurrent hashmap</a>.</td></tr><tr><td><a href="../../../usage/cachebox-object-stores/diskstore.md">DiskStore</a></td><td>Objects are stored on disk in a directory of choice</td></tr><tr><td><a href="../../../usage/cachebox-object-stores/jdbcstore.md">JDBCStore</a></td><td>Objects are stored in a database table of choice</td></tr><tr><td><a href="../../../for-the-geeks/cachebox-architecture/iobjectstore.md">Custom Stores</a></td><td>You can build your own storage</td></tr></tbody></table>

## Eviction Policies

* **,LFU** (Least Frequently Used)
* **LRU** (Least Recently Used)
* **FIFO** (First In First Out)
* **Custom**: You can also build your own and pass the instantiation path in this setting

## Object Stores

* **ConcurrentStore** - Uses concurrent hashmaps for increased performance
* **ConcurrentSoftReferenceStore** - Concurrent hashmaps plus java soft references for JVM memory sensitivity
* **DiskStore** - Uses a physical disk location for caching (Uses java serialization for complex objects)
* **JDBCStore** - Uses a JDBC datasource for caching (Uses java serialization for complex objects)
* **Custom** : You can also build your own and pass the instantiation path in this setting.

> **Caution** : Please note that each object store could have more configuration properties that you will need to add to the configuration structure. To find out about these extra configuration properties, please see the Object Store's section.

**Example:**



### Caches

```javascript
// Register all the custom-named caches you like here
caches = {
    sampleCache1 = {
        provider="cachebox.system.cache.providers.CacheBoxProvider",
        properties = {
            objectDefaultTimeout="20",
            useLastAccessTimeouts="false",
            reapFrequency="1",
            evictionPolicy="LFU",
            evictCount="1",
            maxObjects="100",
            objectStore="ConcurrentSoftReferenceStore"
        }
    },
    sampleCache2 = {
        provider = "cachebox.system.cache.providers.CFColdboxProvider"
    }
},
```

The `caches` element is a configuration data structure for aggregating named cache providers of ANY type. The key is the _unique name_ of the cache to aggregate under this CacheBox instance.  Each provider has unique [configuration properties](../../../usage/cache-providers/cachebox-provider.md), so explore them as well.

<table data-header-hidden><thead><tr><th width="165.33333333333331">Key</th><th width="100">Type</th><th>Description</th></tr></thead><tbody><tr><td>Key</td><td>Type</td><td>Description</td></tr><tr><td><code>provider</code></td><td>string</td><td>The path of the cache that must implement our <code>ICacheProvider</code> interface.</td></tr><tr><td><code>properties</code></td><td>struct</td><td>A structure of name-value pairs of configuration data for the cache to declare.</td></tr></tbody></table>

### Listeners

```javascript
{
    // The path to the listener
    class="path.to.CFC",
    // A unique name for the listener
    name="UniqueName",
    // A structure of name-value pairs for configuring this interceptor
    properties = {}
}
{ class="Timer", name="CoolTimer" }
```

CacheBox has an [event-driven model](../../../advanced-usage/cachebox-event-model/) where you can listen to cache operations and cache factory operations.  You do so with listener CFCs that you register in your config, mostly for standalone operation. In ColdBox, all interceptors have access to all events.

{% hint style="danger" %}
**Caution:** Please note that the order of declaration is the same as the order of execution, so it matters, just like ColdBox Interceptors. Using CacheBox within a ColdBox application, you can also register listeners as interceptors in your ColdBox configuration file.&#x20;
{% endhint %}



<table data-header-hidden><thead><tr><th width="152.33333333333331">Key</th><th width="93">Type</th><th>Description</th></tr></thead><tbody><tr><td>Key</td><td>Type</td><td>Description</td></tr><tr><td><code>class</code></td><td>path</td><td>The instantiation path of the listener object to register</td></tr><tr><td><code>name</code></td><td>string</td><td>The unique name is used for this listener for registration purposes. If no name is provided, we will use the last part of the instantiation path, usually the filename.</td></tr><tr><td><code>properties</code></td><td>struct</td><td>A structure of name-value pairs of configuration data for the listener declared.</td></tr></tbody></table>
