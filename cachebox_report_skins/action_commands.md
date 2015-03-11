# Action Commands

Each skin template can execute action commands. We have several already constructed into the tag that can execute if it detects an incoming `URL` variable called `URL.cbox_command`. 
So if your report exists in a page called monitor.cfm then just call that same page (via AJAX preferably) with some `URL` variables attached (See default skin example). Now, below are the ones we implement, but you can build as many as you like and place them in the page where you use the monitor tag or in the skin templates themselves; wherever they make sense to you.

The following are the commands built in to the reporting tag and the incoming URL variables it expects. Please note that the command is taken from the `URL.cbox_command` variable:

|Command|URL Variables|Description|
|--|--|--|
| expireCache | `url.cbox_cacheName` |Executes a `expireAll()` in the cache provider specified by the incoming cache name.|
| reapCache |`url.cbox_cacheName`| Executes a `reap()` in the cache provider specified in the incoming cache name|
| delCacheEntry |`url.cbox_cacheName`<br>`url.cbox_cacheEntry`|Deletes the passed in cache entry from the named provider|
| clearAllEvents |`url.cbox_cacheName`|Executes a `clearAllEvents()` in the cache provider specified in the incoming cache name(Must be a ColdBox enabled cache)|
| clearAllViews |`url.cbox_cacheName`|Executes a `clearAllViews()` in the cache provider specified in the incoming cache name(Must be a ColdBox enabled cache)|
| cacheBoxReapAll|`none`|Executes a `reapAll()` via the CacheBox Cache Factory|
| cacheBoxExpireAll |`none`|Executes a `expireAll()` via the CacheBox Cache Factory|
| gc| `none` |Executes a suggestion to the JVM to produce a garbage collection|

> **Info** : If the tag detects an incoming command, it will execute it, reset the content and output a **true** to the response buffer.

**Sample Calls**

```javascript
GET monitor.cfm?cbox_command=gc
GET monitor.cfm?cbox_command=cacheBoxReapAll
GET monitor.cfm?cbox_command=delCacheEntry&cbox_cacheName=default&cbox_cacheEntry=testKey
```

