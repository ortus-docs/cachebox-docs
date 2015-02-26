# Using Your Own Policy

CacheBox is incredibly flexible and if you would like to create your own eviction policy, you can! Below are a set of easy steps on how to do this:

1. Create a simple CFC that implements the following class *coldbox.system.cache.policies.IEvictionPolicy* or use our convenience abstract class and inherit from *coldbox.system.cache.policies.AbstractEvictionPolicy*
2. Create your own execute() method that will evict items (We recommend looking at existing policies to get an insight on how to do this) 3. Use the policy instantiation path in your cachebox provider properties

Sample Policy

```javascript
<cfcomponent output="false"
             hint="FIFO Eviction Policy Command"
             extends="coldbox.system.cache.policies.AbstractEvictionPolicy">

<-------------------------------------------- CONSTRUCTOR ------------------------------------------->

    <---  init --->
    <cffunction name="init" output="false" access="public" returntype="FIFO" hint="Constructor">
        <cfargument name="cacheProvider" type="any" required="true" hint="The associated cache provider of type: coldbox.system.cache.ICacheProvider" colddoc:generic="coldbox.system.cache.ICacheProvider"/>
        <cfscript>
            super.init(arguments.cacheProvider);

            return this;
        </cfscript>
    </cffunction>

<-------------------------------------------- PUBLIC ------------------------------------------->

    <---  execute --->
    <cffunction name="execute" output="false" access="public" returntype="void" hint="Execute the policy">
        <cfscript>
            var index       = "";

            // Get searchable index
            try{
                index   = getAssociatedCache().getObjectStore().getIndexer().getSortedKeys("hits","numeric","asc");
                // process evictions via the abstract class
                processEvictions( index );
            }
            catch(Any e){
                getLogger().error("Error sorting via store indexer #e.message# #e.detail# #e.stackTrace#.");
            }
        </cfscript>
    </cffunction>

<-------------------------------------------- PRIVATE ------------------------------------------->

</cfcomponent>
```
Process Evictions: The below code is the code used to evict objects from cache

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

Configuration File

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
