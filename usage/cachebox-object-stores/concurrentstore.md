# ConcurrentStore

The `ConcurrentStore` is an object store that uses concurrent hash maps provided by the [Sun JDK](http://docs.oracle.com/javase/tutorial/essential/concurrency/highlevel.html). Concurrent maps are better suited for caching algorithms as they do not lock the entire map in order to access elements. They work on the concept of row locking. Therefore, the increased performance and increase in throughput is observable by using concurrency maps. Here is a quote from the Java Docs:

> "However, even though all operations are thread-safe, retrieval operations do not entail locking, and there is not any support for locking the entire table in a way that prevents all access. Retrieval operations (including get) generally do not block, so may overlap with update operations (including put and remove). Retrievals reflect the results of the most recently completed update operations holding upon their onset." \
> [Java Docs](http://docs.oracle.com/javase/tutorial/essential/concurrency/highlevel.html)

## Properties

* _None_

You can also find some great research out there about concurrency maps:

* [http://www.ibm.com/developerworks/java/library/j-jtp07233.html](http://www.ibm.com/developerworks/java/library/j-jtp07233.html)
* [http://www.ehcache.org](http://www.ehcache.org)
