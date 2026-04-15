# Using Your Own Policy

CacheBox is incredibly flexible and if you would like to create your own eviction policy, you can! Below are a set of easy steps on how to do this:

1. Create a simple CFC that implements the following class `cachebox.system.cache.policies.IEvictionPolicy` or use our convenience abstract class and inherit from `cachebox.system.cache.policies.AbstractEvictionPolicy`
2. Create your own `execute()` method that will evict items (We recommend looking at existing policies to get an insight on how to do this)&#x20;
3. Use the policy instantiation path in your `cachebox` provider `properties`

## Sample Policy

```javascript
/**
* FIFO Eviction Policy Command
*/
component extends="cachebox.system.cache.policies.AbstractEvictionPolicy"{

    /**
    * Constructor
    * @cacheProvider The associated cache provider of type: cachebox.system.cache.ICacheProvider
    */
    FIFO function init( required cacheProvider ){
        super.init( arguments.cacheProvider );

        return this;
    }

    /**
    * Execute the policy
    */
    function execute(){
        var index       = "";

        // Get searchable index
        try{
            index = getAssociatedCache()
                .getObjectStore()
                .getIndexer()
                .getSortedKeys( "hits", "numeric", "asc" );

            // process evictions via the abstract class
            processEvictions( index );
        }
        catch(Any e){
            getLogger().error("Error sorting via store indexer #e.message# #e.detail# #e.stackTrace#.");
        }
    }

}
```

## Process Evictions

The `processEvictions()` method is provided by the `AbstractEvictionPolicy` base class and handles the actual object expiration loop. Call it from your `execute()` method after sorting the index.

{% tabs %}
{% tab title="BoxLang" %}
```bx
private void function processEvictions( required array index ) {
    var oCacheManager  = getAssociatedCache()
    var indexer        = oCacheManager.getObjectStore().getIndexer()
    var indexLength    = index.len()
    var evictCount     = oCacheManager.getConfiguration().evictCount
    var evictedCounter = 0

    for ( var x = 1; x <= indexLength; x++ ) {
        if ( !indexer.objectExists( index[ x ] ) ) { continue }
        var md = indexer.getObjectMetadata( index[ x ] )

        // Evict if not eternal and not already expired
        if ( md.timeout > 0 && !md.isExpired ) {
            oCacheManager.expireKey( index[ x ] )
            oCacheManager.getStats().evictionHit()
            if ( ++evictedCounter >= evictCount ) { break }
        }
    }
}
```
{% endtab %}
{% tab title="CFML" %}
```javascript
private void function processEvictions( required array index ) {
    var oCacheManager  = getAssociatedCache();
    var indexer        = oCacheManager.getObjectStore().getIndexer();
    var indexLength    = arrayLen( arguments.index );
    var evictCount     = oCacheManager.getConfiguration().evictCount;
    var evictedCounter = 0;

    for ( var x = 1; x <= indexLength; x++ ) {
        if ( !indexer.objectExists( arguments.index[ x ] ) ) { continue; }
        var md = indexer.getObjectMetadata( arguments.index[ x ] );

        // Evict if not eternal and not already expired
        if ( md.timeout > 0 && !md.isExpired ) {
            oCacheManager.expireKey( arguments.index[ x ] );
            oCacheManager.getStats().evictionHit();
            if ( ++evictedCounter >= evictCount ) { break; }
        }
    }
}
```
{% endtab %}
{% endtabs %}

## Configuration File

```javascript
defaultCache = {
    objectDefaultTimeout = 120,
    objectDefaultLastAccessTimeout = 30,
    useLastAccessTimeouts = true,
    reapFrequency = 2,
    freeMemoryPercentageThreshold = 0,

    evictionPolicy = "myPath.policies.MyPolicy",

    evictCount = 1,
    maxObjects = 300,
    objectStore = "ConcurrentSoftReferenceStore",
    coldboxEnabled = false
}
```

That's it folks! Very easily you can create your own eviction policies and use our built in indexers to just sort the elements in whatever way you like. If not, you can always do it yourself :)
