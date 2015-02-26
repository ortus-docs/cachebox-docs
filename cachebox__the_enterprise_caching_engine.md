# CacheBox : The Enterprise Caching Engine

Caching has been a central concern in the ColdBox Platform since its very first version. We have always been concerned with mission critical applications, scalability and the ability to provide granular caching aspects to ColdBox applications. With CacheBox we decided it was time to open up the library for usage to all ColdFusion applications, not even if they are built on ColdBox (Shame on you!).

<img src="./images/intro_OBjectStores.png">

Foremost, CacheBox behaves as an in-memory cache designed for handlers, plugins, events, views fragments and any other objects or data you so desire. It has various tuning parameters such as default object timeout, default last access timeout, maximum objects to have in cache, a JVM memory threshold, a reaping frequency, eviction policies, an event model and so much more.

We also make use of object stores (inspired by EHCache) for the CacheBox caching engine. This means that CacheBox can be configured to store its cached objects in different locations other than memory. This gives us great flexibility because we offer a wide gamut of storage options plus the concept of actually building your own storages. Currently we offer object stores based on concurrency classes, java soft references (memory sensitive), file storage, JDBC replication, and more coming soon.

<img src="./images/intro_cachemonitor.jpg">
