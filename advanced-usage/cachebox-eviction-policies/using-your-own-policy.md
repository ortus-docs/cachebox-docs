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

## Process Evictions:

The below code is the code used to evict objects from cache

```javascript
<---  processEvictions --->
<cffunction name="processEvictions" output="false" access="private" returntype="void" hint="Abstract processing of evictions">
    <cfargument name="index" type="array" required="true" hint="The array of metadata keys used for processing evictions"/>
    <cfscript>
        var oCacheManager   = getAssociatedCache();
        var indexer         = oCacheManager.getObjectStore().getIndexer();
        var indexLength     = arrayLen(arguments.index);
        var x               = 1;
        var md              = "";
        var evictCount      = oCacheManager.getConfiguration().evictCount;
        var evictedCounter  = 0;

        //Loop Through Metadata
        for (x=1; x lte indexLength; x=x+1){

            // verify object in indexer
            if( NOT indexer.objectExists( arguments.index[x] ) ){
                continue;
            }
            md = indexer.getObjectMetadata( arguments.index[x] );

            // Evict if not already marked for eviction or an eternal object.
            if( md.timeout gt 0 AND NOT md.isExpired ){

                // Expire Object
                oCacheManager.expireKey( arguments.index[x] );

                // Record Eviction
                oCacheManager.getStats().evictionHit();
                evictedCounter++;

                // Can we break or keep on evicting
                if( evictedCounter GTE evictCount ){
                    break;
                }
            }
        }//end for loop
    </cfscript>
</cffunction>
```

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
