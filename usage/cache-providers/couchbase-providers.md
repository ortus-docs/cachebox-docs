# Couchbase Providers

{% hint style="danger" %}
**Legacy / No Longer Supported**: The commercial Railo/Lucee Couchbase extension described on this page has been discontinued and is no longer sold or maintained by Ortus Solutions. There is no corresponding Couchbase cache provider shipped in the current CacheBox source (`system/cache`). This page is kept for historical reference only — please do not use it as a guide for new projects. If you need a distributed/remote cache today, look at the shipped [Cache Providers](README.md) or build your own via `ICacheProvider`.
{% endhint %}

### Ortus Couchbase Extension

[Ortus Solutions](http://www.ortussolutions.com/products/couchbase-railo), the makers of CacheBox, have created a commercial extension for the open source CFML engines Railo and Lucee to support caching distribution features via Couchbase ([https://www.ortussolutions.com/products/couchbase-lucee](https://www.ortussolutions.com/products/couchbase-lucee)).

> The Ortus Couchbase Extension is a Railo Server Extension that allows your server to natively connect to a Couchbase NoSQL Server cluster and leverage it for built-in caching, session/client storage and distribution, and much more. With our extension you will be able to scale and extend your Railo CFML applications with ease.

The extension will enhance your Lucee server with some of the following [capabilities](https://www.ortussolutions.com/products/couchbase-lucee):

* Store session/client variables in a distributed Couchbase cluster
* Get rid of sticky session load balancers, come to the round-robin world!
* Session/client variable persistence even after Railo restarts
* Ability to leverage the RAM resource virtual file system as a cluster-wide file system
* Cache connection capabilities for providing distributed & highly scalable query, object, template, function caching
* [Much more](https://www.ortussolutions.com/products/couchbase-lucee)
