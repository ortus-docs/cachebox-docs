# Distributed

Distributed caching is the big daddy of scalability and extensibility. The crux concept is of partitioning the cache data across the members of the cache cluster and creating a grid of cached data that can scale rather easily. There are several major players out there like [EHCache](http://ehcache.org/) with Terracotta, [Oracle](http://www.oracle.com/technetwork/middleware/coherence/overview/index.html) [Coherence](http://www.oracle.com/technetwork/middleware/coherence/overview/index.html), [Couchbase NoSQL](http://couchbase.com/), etc. I suggest looking at all three options, but using EHCache with Terracotta is definitely easy to setup, easy to use and their tools are great. They also offer professional services and support. Please note that each vendor has their own flavor of distributed caching and might not match our diagram. Our diagram is just a visual representation for knowledge purposes.

<img src="../images/cachebox_topology_distributed.png">

Benefits:
* Extreme scalability
* Cache data can survive server restarts if one goes down, better redundancy
* Better cache availability through redundancy
* Higher storage availability
* Higher flexibility
* Your storage increases as more cluster members are added

Cons:
* Harder to configure and setup (Maybe, terracotta and ColdFusion 9 is super easy)
* Not as much serialization and communication costs
* Could need load balancing


