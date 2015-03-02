# CacheBox DSL
In order to create a simple data CFC, just create a new CFC with one required method on it called configure(). This is where you will define the caching configuration data structure in a structure called cacheBox in the variables scope:

```javascript
**
* A CacheBox configuration data object
*/
component{

    function configure(){
        cacheBox = {

        };
    }
}
```

The cacheBox structure can be configured with the following keys:

|Key|Type|Required|Default|Description|
|--|--|--|--|--|
|logBoxConfig |string |false |*coldbox.system.cache.config.LogBox* |The instantiation or location of a LogBox configuration file. This is only for standalone operation.|
|scopeRegistration |struct |false|*{enabled=true,scope=application,key=cacheBox} *|A structure that enables scope registration of the CacheBox factory in either server, cluster, application or session scope. |
|defaultCache |struct |true|---|The configuration of the default cache which will have an implicit name of default which is a reserved cache name. It also has a default provider of CacheBox which cannot be changed.|
|caches |struct|true|{}|A structure where you can create more named caches for usage in your CacheBox factory.|
|listeners |array|false|[]|An array that will hold all the listeners you want to configure at startup time for your CacheBox instance. If you are running CacheBox within a ColdBox application, this item is not necessary as you can register them via the main ColdBox interceptors section.|
