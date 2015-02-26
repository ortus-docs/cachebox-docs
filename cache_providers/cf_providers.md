# CF Providers

Our *CFColdboxProvider* is an implementation specifically written for Adobe ColdFusion 9.0.1 and beyond. This provider leverages the [EHCache](http://ehcache.org/) engine within ColdFusion 9 and extends the native ColdFusion capabilities by talking to the [EHCache](http://ehcache.org/) sessions natively via Java. In this manner we are able to do things like:

* Get extended cached object metadata
* Get overall cache statistics
* Talk to terracotta classes
* Do quiet operations on get, clear, and put
* Check if an element is expired
* Do reporting and content reporting
* Much more

