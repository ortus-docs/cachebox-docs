# LogBoxConfig

The LogBoxConfig element is used only in standalone mode of operation and tells CacheBox what configuration file to load into LogBox.  [LogBox](http://logbox.ortusbooks.com) is an enterprise ColdFusion (CFML) logging library. This way, you have granular control of how CacheBox and its registered caches will be producing logging and debugging data. If you do not specify a location for a custom LogBox configuration file, then CacheBox will instantiate LogBox with its own default configuration file located at:

```javascript
cachebox.system.cache.config.LogBox.cfc
```

Example

```javascript
// The CacheBox configuration structure DSL
cacheBox = {
    logBoxConfig = "myapp.config.MyLogBoxConfig",
};
```
