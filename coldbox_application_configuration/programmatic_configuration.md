# Programmatic Configuration

ColdBox 3.0.0 and above allows for a programmatic approach via the ColdBox configuration object. So let's look at how the framework loader looks at your configuration for CacheBox configuration details:

* Is there a CacheBox DSL variable defined in the configuration structure?
    * False:
        * Does a *CacheBox.cfc* exist in the application's config folder?
        * False: Configure CacheBox with default framework settings found in */coldbox/system/web/config/CacheBox.cfc*
    * True:
        * Have you defined a configFile key in the cacheBox DSL structure?
            * True: Then use that value to pass into the configuration object so it can load CacheBox using that configuration file (xml or CFC)
            * False: The configuration data (CacheBox DSL) is going to be defined inline here so use that structure for configuration

> **Info** Note: The configuration DSL is exactly the same as you have seen in before with the only distinction that you can add a configFile key that can point to an external configuration file (XML or CFC)

```javascript
cacheBox = {
    configFile = "mypath.config.CacheBoxConfig"
};
```

That's it folks! You can either write inline CacheBox DSL configuration, use by convention a *CacheBox.cfc* data CFC or use a configFile approach for external file loading. Pick your poison!
