# Scope Registration

CacheBox has a nifty little feature that enables itself to leech onto a specific scope in memory. It basically can auto-register itself in your environment with no further need for persistence or just to expand its location. By default CacheBox registers itself in application scope with a key of **cacheBox**, but you have complete control on how the scope registration should work.

Customizable Keys:

|Key|Type|Required|Default|Description|
|--|--|--|--|--|
|enabled|boolean|false|*true*|Enable scope registration|
|scope|string|false|*application*|The ColdFusion scope to persist on|
|key|string|false|*cachebox*|The name of the key in the ColdFusion scope to persist on|

Example:

```javascript
// The CacheBox configuration structure DSL
cacheBox = {
    scopeRegistration = {
        enabled = true,
        scope   = "application",
        key     = "cacheBox"
    },
};
```
