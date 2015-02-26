# ColdBox Caches

A typical ColdBox application is configured by default with two caches named: *default* and *template*. The *default* cache is used for data, objects, model objects, plugins, handlers, etc. The *template* cache is exclusively used for event caching and view fragment caching. This provides the developer a nice way to decide how each of these concerns are cached. So if you are in a multi-cluster environment and you wanted to share event and view fragment caching in the cluster, you could easily configure the *template* cache to use the JDBCStore or the DiskStore and store these elements in a central location shared by the cluster. Lots of possibilities here.

We recommend seeing our other guides to see how caching is leveraged internally in ColdboxEnabled

* [Event Handlers](http://wiki.coldbox.org/wiki/EventHandlers.cfm) : How event handlers are persisted and how event caching can accelerate your applications
* [Layouts-Views Guide](http://wiki.coldbox.org/wiki/Layouts-Views.cfm) : A great way to find out how to do view fragment caching
* [Plugins](http://wiki.coldbox.org/wiki/Plugins.cfm) : How plugins are persisted if you are a plugin author
* [Interceptors](http://wiki.coldbox.org/wiki/Interceptors.cfm) : Learn what are interceptors/listeners, how to use them and how to configure them
* [FlashRAM](http://wiki.coldbox.org/wiki/FlashRAM.cfm) : How the ColdBox Flash RAM can be configured to use CacheBox for distribution
