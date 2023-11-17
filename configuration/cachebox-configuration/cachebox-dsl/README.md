# CacheBox DSL

As we have seen, the CacheBox DSL can be used in different contexts:

* Portable CFC with a `configure()` method in a `cachebox` variable
* ColdBox config inside the `configure()` method in a `cachebox` variable
* A struct literal sent into the constructor of CacheBox

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

The LogBoxConfig element is used only in a standalone mode of operation and tells CacheBox what configuration file to load into LogBox.&#x20;

[LogBox](http://logbox.ortusbooks.com) is an enterprise ColdFusion (CFML) logging library

By default, CacheBox will instantiate LogBox with its default configuration file located at: `cachebox.system.cache.config.LogBox.cfc` which logs to the console.

```javascript
// The CacheBox configuration structure DSL
logBoxConfig : "myapp.config.MyLogBoxConfig",
```

### Scope Registration

This configuration allows for CacheBox to be placed automatically upon construction in your chosen specified scope.

By default, CacheBox registers itself in `application` scope with a key of `cachebox`

<table data-header-hidden><thead><tr><th width="135">Key</th><th width="102">Type</th><th width="107">Required</th><th width="125">Default</th><th>Description</th></tr></thead><tbody><tr><td>Key</td><td>Type</td><td>Required</td><td>Default</td><td>Description</td></tr><tr><td><code>enabled</code></td><td>boolean</td><td>false</td><td><em>true</em></td><td>Enable scope registration</td></tr><tr><td><code>scope</code></td><td>string</td><td>false</td><td><em>application</em></td><td>The ColdFusion scope to persist on</td></tr><tr><td><code>key</code></td><td>string</td><td>false</td><td><em>cachebox</em></td><td>The name of the key in the ColdFusion scope to persist on</td></tr></tbody></table>

Example:

```javascript
scopeRegistration = {
    enabled = true,
    scope   = "application",
    key     = "cacheBox"
},
```

