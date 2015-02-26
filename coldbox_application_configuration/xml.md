# XML

The XML approach uses exactly the same configuration elements as the normal XML configuration file but with one extra element: *&lt;ConfigFile&gt;*. This serves the same purpose as in the programmatic approach, where you have defined the CacheBox configuration somewhere and you are pointing to it via this setting:

```javascript
<CacheBox>
    <ConfigFile>shared.path.LogBoxConfig</ConfigFile>
</CacheBox>
```

Please also note that the application loader follows the same approach as in the programmatic configuration:

* Is there a *&lt;CacheBox&gt;* element defined in the configuration structure?
    * False:
        * Does a *CacheBox.cfc* exist in the application's config folder?
        * False: Configure CacheBox with default framework settings found in */coldbox/system/web/config/CacheBox.cfc*
    * True:
        * Have you defined a *&lt;configFile&gt;* key in the cacheBox DSL structure?
            * True: Then use that value to pass into the configuration object so it can load CacheBox using that configuration file (xml or CFC)
            * False: The configuration data (CacheBox DSL) is going to be defined inline here so use that structure for configuration
