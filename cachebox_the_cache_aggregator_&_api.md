# CacheBox: The Cache Aggregator & API

CacheBox is a cache aggregator, in which you can aggregate different caching engines or types of the same engine into one single umbrella. It gives you built in logging (via [LogBox](http://wiki.coldbox.org/wiki/LogBox.cfm)), an event model, synchronization, shutdown/startup procedures, reporting, interaction consoles and best of all a cache agnostic API. You can then build your applications based on an abstract API and then be able to configure the caches for your applications at runtime. This gives you greater flexibility and scalability when planning and writing your applications as they can be targeted for ANY CFML engine or version.

<img src="./images/intro_cacheboxTriangle.png">

CacheBox gives you the ability to manage and create your own, what we call <i>Cache Providers</i> that talk to different caching engines that you would like to configure in your applications. By aggregating them within CacheBox you get the added benefit of a rich event model for all caches to share, reporting and debugging. We have a great cache debugger where you can visualize all your configured caches right from within your application. You can see the performance of the cache, the contents and even issue commands to the targeted cache provider.

These cache providers also share the same interaction API and thus gives you a nice level of abstraction, higher extensibility and flexibility when planning your applications or trying to scale them out.
