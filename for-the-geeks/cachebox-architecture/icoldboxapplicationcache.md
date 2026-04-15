# IColdboxApplicationCache

**class** : `cachebox.system.cache.IColdboxApplicationCache`

This interface extends from the original cache provider interface and adds certain methods that MUST be implemented so the cache can work for ColdBox applications. This includes functionality to do event/view caching, clearing/expiring by certain regular expressions and reporting. So if you want to create your own cache implementation for ColdBox applications, then it must adhere to this contract.

## Interface Methods

| Method | Description |
| --- | --- |
| `getViewCacheKeyPrefix()` | Get the string prefix used when building view cache keys |
| `getEventCacheKeyPrefix()` | Get the string prefix used when building event cache keys |
| `getColdbox()` | Get the linked ColdBox application controller |
| `setColdBox( required coldbox )` | Link a ColdBox application controller to this provider |
| `getEventURLFacade()` | Get the event URL facade helper object used for key generation |
| `clearAllEvents( [boolean async=false] )` | Clear all cached events; optionally run asynchronously |
| `clearEvent( required string eventSnippet, [string queryString=""] )` | Clear a cached event by snippet and optional query string |
| `clearEventMulti( required string eventsnippets, [string queryString=""] )` | Clear multiple cached events by a comma-delimited snippet list |
| `clearView( required string viewSnippet )` | Clear a specific cached view by snippet |
| `clearViewMulti( required string viewSnippets )` | Clear multiple cached views by a comma-delimited snippet list |
| `clearAllViews( [boolean async=false] )` | Clear all cached views; optionally run asynchronously |
