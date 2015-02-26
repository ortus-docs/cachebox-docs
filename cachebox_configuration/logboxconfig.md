# LogBoxConfig

The LogBoxConfig element is used only in standalone mode of operation and tells CacheBox what configuration file to load into http://wiki.coldbox.org/wiki/LogBox.cfm[](http://wiki.coldbox.org/wiki/LogBox.cfm). [LogBox](http://wiki.coldbox.org/wiki/LogBox.cfm) is an enterprise ColdFusion logging library that is part of the ColdBox Platform. This way, you have granular control of how CacheBox and its registered caches will be producing logging and debugging data. If you do not specify a location for a custom [LogBox](http://wiki.coldbox.org/wiki/LogBox.cfm) configuration file, then CacheBox will instantiate [LogBox](http://wiki.coldbox.org/wiki/LogBox.cfm) with its own default configuration file located at:

```javascript
coldbox.system.cache.config.LogBox.cfc
OR
cachebox.system.cache.config.LogBox.cfc
```

Example

```javascript
// The CacheBox configuration structure DSL
cacheBox = {
    logBoxConfig = "myapp.config.MyLogBoxConfig",
};
```
