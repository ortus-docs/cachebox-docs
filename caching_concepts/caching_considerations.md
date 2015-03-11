# Caching Considerations

Whenever you are leveraging the power of caching, we recommend that you also take into consideration several key factors that need to be evaluated and put into practice in your applications. Below are some key factors that we recommend:

* **Thread Safety** : Take into consideration that when you cache data/objects or whatever, multiple threads will be trying to access it in your application. Make sure that you have the appropriate locking and synchronization techniques so multiple threads don't interfere with one another. This might be from simple testing procedures to make sure an element exists, to a more strict approach where you create a cache decorator that does hard blocks on cache access via named locks. Don't ever assume that what you ask from the cache actually exists.
* **Serialization** : If you will be caching to disk, database or using replication, distribution, most likely the caching engines will be serializing or converting your data and objects into byte or string format in order to persist them. Therefore, your objects must be able to support serialization and also be aware that if you are caching complex objects, those objects will be serialized alongside the target object. This is what's called an object graph. Where a serializer will go through the entire object graph (object/data relationships) of the target object and serialize everything. If you have circular references or references to tons of objects, serialization performance degrades and could potentially cause a heap overload and crash your application server as it will recurse forever. ColdFusion 9 introduced the component and property attribute called serializable, which is a boolean attribute you can add to the `cfcomponent` and `cfproperty` tags. We recommend using it and marking components and relationships that do NOT need serialization.

```javascript
<---  Marking a component as NOT serializable --->
<cfcomponent output="false" serializable="false">

</cfcomponent>

<---  Marking a property as NOT serializable --->
<cfproperty name="cacheEngine" serializable="false" />
```

> <b>Important</b> The default value for the serializable attribute is true.

* Data Format : Determine how you want to store data so it is easy to take that snapshot out of a cache and use. This can be from implementing object state/memento patterns, to leveraging serialization, to pre-defined data structures. Think ahead of HOW your data will be stored in the caches.
* Cache Layers : In our experience, we have seen greater improvement in performance and scalability by planning caching layers. Caching layers is what are the different layers of caching your application will provide from data to objects to event and view fragments. We recommend you analyze your cache layers and plan how they will behave. A perfect live example of caching layers can be seen in our open source ColdFusion wiki, CodexWiki, which you are actually using right now. CodexWiki leverages query caching, XML/Feed caching, object caching of DAO's, services, some business objects, plugins and event handlers, to view fragment caching and overall event output caching. We use it all baby!

<img src="../images/cachebox_cachelayers.png">

* Cache Limits : There are definite benefits of demarcating limits on your cache. This involves setting up default limits for timeouts, idle timeouts and maximum number of objects within a cache. Studies have shown that leverage memory sensitive data constructs with fixed limit caching parameters can increase performance and overall JVM stability. Look at our cache resources for these studies as they are very interesting.


