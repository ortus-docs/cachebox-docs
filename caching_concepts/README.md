# Caching Concepts

> "A cache (pronounced /'kæ?/ kash) is a component that improves performance by transparently storing data such that future requests for that data can be served faster" <br> <small> Wikipedia</small>

Caching is everywhere around us these days in all shapes and forms: query caching, data caching, page fragment caching, event caching, etc. Much like how in [Forrest Gump you could do all kinds of shrimp dishes](https://www.youtube.com/watch?v=4rT5fYMfEUc) :)

In its most basic form, we use caching to accelerate and scale our processes. We might have a certain request that takes time to process due to let’s say in colloquial terms "a big ass query". We can leverage caching by slapping that query up and placing it in cache so we don't have to wait for it again. Our process now only at most take 1 big hit and then can be merrily on their way serving requests. Again, this is a very practical approach to caching. As you will see from this guide, caching can get very very complex and you need the right tools to be able to scale out, configure and tune your caching approaches.

When building enterprise class applications we are faced with many problems dealing with architecture, performance, scalability and so much more. One of these issues might be dealing with expensive queries, but there are also lots of other issues to consider like: expense of object creation/configuration, data retrieval, data/system availability, page output caching, etc. All of these issues can benefit from some kind of caching in order to optimize performance, availability and scalability.

Let's explore some benefits of caching:

* Reduce the amounts of data transfers between processes, network or applications
* Reduce processing time within a system or application
* Reduce I/O access operations
* Reduce database access operations
* Reduce expensive data transformations and live by a 1 hit motto
