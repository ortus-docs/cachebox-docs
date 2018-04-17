# ColdBox Configuration

## Default Configuration

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

## Custom Configuration

ColdBox allows for a programmatic approach via the ColdBox configuration object: `Coldbox.cfc`. So let's look at how the framework loader looks at your configuration for CacheBox configuration details:

* Is there a `cachebox` DSL variable defined in the configuration structure?
* **False**:
  * Does a `CacheBox.cfc` exist in the application's `config` folder?
    * **True** : Use that for configuration
    * **False**: Configure CacheBox with default framework settings found in `/coldbox/system/web/config/CacheBox.cfc`
* **True**:
  * Have you defined a `configFile` key in the `cacheBox` DSL structure?
    * **True**: Then use that value to pass into the configuration object so it can load CacheBox using that configuration CFC
    * **False**: The configuration data \(CacheBox DSL\) is going to be defined inline here so use that structure for configuration

> **Info** The configuration DSL is exactly the same as you have seen in before with the only distinction that you can add a `configFile` key that can point to an external configuration CFC.

```javascript
cacheBox = {
    configFile = "mypath.config.CacheBoxConfig"
};
```

That's it folks! You can either write inline CacheBox DSL configuration, use by convention a `CacheBox.cfc` data CFC or use a configFile approach for external file loading. Pick your poison!

