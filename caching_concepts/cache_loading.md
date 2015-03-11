# Cache Loading

When working with a cache engine you also have to consider how you will get data INTO the cache before you work with it. There are several approaches but I will talk about two methods of content loading:

* **Lazy Loading or Reactive Loading** : This type of loading is the most typical way to load data into a cache and it happens once data is requested from an external process. Below is a typical example using CacheBox in a service layer call:


```js
/**
* Get some blog categories from the database or cache
*/
function getCategories(){
    var cacheKey = "q-blog-categories";

    //Check if data exists
    local.data = cache.get( cacheKey );
    if( !isNull( local.data ) ){
        return local.data;
    }

    // Else query DB and cache
    var data = blogDAO.getCategories();
    cache.set(cacheKey, data, 120, 20);

    return data;
}
```

This is great for small content pieces and works well for applications. However, if you have large amounts of data that must be available at application startup or cache startup. Then we recommend looking at the next method.


* Proactive Loading : This approach focuses itself on the loading of resources before the application starts up so content can be loaded. EHCache for example offers cache loaders that you can create that will populate the cache on initializations. CacheBox offers the same capabilities through its event model, so you can tap into the necessary events and then carry your population and loading procedures. For example, you might tap into the afterCacheRegistration event in CacheBox so you might listen to when a cache engine get's created and configured so you can start populating it right at application/cache startup. In this loader you will then have the opportunity to load your data either asynchronously or synchronously. If you will be loading large amounts of data or processor intensive data, we recommend you leverage cfthread and do the loading asynchronously within your event interceptor.

```javascript
/**
* A cache listener for CacheBox
*/
component{

    /**
    * Listen for cache registrations and load data into the 'bigCache' cache ONLY!
    */
    function afterCacheRegistration(interceptData){
        // Get the registered cache reference from the incoming interception data
        var cache = arguments.interceptData.cache;

        // Only work on the BigCache cache
        if( cache.getName() eq "BigCache" ){

            // Talk to service, get some big data items
            dataItems = service.getBigDataItems();

            //Cache them forever as eternal objects
            cache.setMulti(mapping=dataItems,timeout=0);
        }

    }
}
```

