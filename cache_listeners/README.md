# Cache Listeners

We have already seen in our previous section all the events that are announced by CacheBox and its providers, but how do we listen? 

There are two ways to build CacheBox listeners because there are two modes of operations, but the core is the same. Listeners are simple CFCs that must create methods that match the name of the event they want to listen in. If you are running CacheBox within a ColdBox application, listeners are Interceptors and you declare them and register them exactly the same way that you do with normal interceptors.

Also, these methods can take up to three parameters depending on your mode of operation (standalone or ColdBox). The one main difference between pure CacheBox listeners and ColdBox interceptors are that the configure method for the standalone CacheBox is different. Please see samples in this section.

## Examples
So let's say that we want to listen on the `beforeCacheFactoryShutdown` and on the `afterCacheElementRemoved` event in our listener.

**Coldbox Mode Listener**

```javascript
component{

    function configure(){}

    function beforeCacheFactoryShutdown(event, interceptData, buffer){
        // get factory reference.
        var cacheFactory = arguments.interceptData.cacheFactory;
        // Do my stuff here:

        // I can use a log object because ColdBox is cool and injects one for me already.
        log.info("DUDE, I am going down!!!");
    }

    function afterCacheElementRemoved(event, interceptData, buffer){
        var cache = arguments.interceptData.cache;
        var key = arguments.interceptData.cacheObjectKey;

        log.info("The cache #cache.getName()# just removed the key -> #key#");
    }
}
```

**Standalone Mode Listener**

```javascript
component{

    function configure(cacheBox,properties){
        variables.cacheBox = arguments.cacheBox;
        variables.properties = arguments.properties;

        log = variables.cacheBox.getLogBox().getLogger( this );
    }

    function beforeCacheFactoryShutdown(interceptData){
        // Do your stuff here.
    }

    function afterCacheElementRemoved(interceptData){
        var cache = arguments.interceptData.cache;
        var key = arguments.interceptData.cacheObjectKey;

        log.info("The cache #cache.getName()# just removed the key -> #key#");
    }
}
```

Please note the `configure()` method in the standalone listener. This is necessary when you are using CacheBox listeners outside of a ColdBox application. The `configure()` method receives two parameters:

* `cacheBox` : An instance reference to the CacheBox factory where this listener will be registered with.
* `properties` : A structure of properties that passes through from the configuration file.

As you can see from the examples above, each Listener component can listen to multiple events. Now you might be asking yourself, in what order are these listeners executed in? Well, they are executed in the order they are declared in either the ColdBox configuration file as interceptors or the CacheBox configuration file as listeners.

> **Important** Order is EXTREMELY important for interceptors/listeners. So please make sure you order them in the declaration file.




