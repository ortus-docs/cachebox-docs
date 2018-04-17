# Summary

## Intro

* [Introduction](README.md)
  * [What's New With 5.0.0](whats-new-with-500.md)
  * [What's New With 2.1.0](whats-new-with-2.1.0.md)
  * [What's New With 2.0.0](whats-new-with-2.0.0.md)
  * [About This Book](about-this-book.md)
  * [Author](author.md)

## Getting Started

* [Overview](overview/README.md)
  * [CacheBox RefCard](overview/cachebox-refcard.md)
  * [Useful Resources](overview/useful-resources.md)
  * [Features at a Glance](overview/features-at-a-glance.md)
  * [System Requirements](overview/system-requirements.md)
* [Installing CacheBox](installing-cachebox/README.md)
  * [Installation](installing-cachebox/installation.md)
* [Caching Concepts](caching-concepts/README.md)
  * [Caching Considerations](caching-concepts/caching-considerations.md)
  * [Cache Loading](caching-concepts/cache-loading.md)
  * [Definitions](caching-concepts/definitions.md)
  * [Java Soft References](caching-concepts/java-soft-references.md)
* [Cache Topologies](cache-topologies/README.md)
  * [Single Instance/In-Process](cache-topologies/single-instance-in-process.md)
  * [Single Instance/Out-Process](cache-topologies/single-instance-out-process.md)
  * [Replicated](cache-topologies/replicated.md)
  * [Distributed](cache-topologies/distributed.md)
* [CacheBox Architecture](cachebox-architecture/README.md)
  * [CacheFactory](cachebox-architecture/cachefactory.md)
  * [CacheBoxConfig](cachebox-architecture/cacheboxconfig.md)
  * [EventManager](cachebox-architecture/eventmanager.md)
  * [ColdBox](cachebox-architecture/coldbox.md)
  * [LogBox](cachebox-architecture/logbox.md)
  * [ICacheProvider](cachebox-architecture/icacheprovider.md)
  * [ICacheStats](cachebox-architecture/icachestats.md)
  * [IObjectStore](cachebox-architecture/iobjectstore.md)
  * [IEvictionPolicy](cachebox-architecture/ievictionpolicy.md)
  * [AbstractEvictionPolicy](cachebox-architecture/abstractevictionpolicy.md)
  * [IColdboxApplicationCache](cachebox-architecture/icoldboxapplicationcache.md)
* [Creating CacheBox](creating-cachebox/README.md)
  * [Common CacheFactory Methods](creating-cachebox/common-cachefactory-methods.md)
  * [Cache Cleanup/Reaping](creating-cachebox/cache-cleanup-reaping.md)

## Configuration

* [CacheBox Configuration](cachebox-configuration/README.md)
  * [CacheBox DSL](cachebox-configuration/cachebox-dsl/README.md)
    * [LogBoxConfig](cachebox-configuration/cachebox-dsl/logboxconfig.md)
    * [Scope Registration](cachebox-configuration/cachebox-dsl/scope-registration.md)
    * [Default Cache](cachebox-configuration/cachebox-dsl/default-cache.md)
    * [Caches](cachebox-configuration/cachebox-dsl/caches.md)
    * [Listeners](cachebox-configuration/cachebox-dsl/listeners.md)
  * [CacheBox Config Object](cachebox-configuration/cachebox-config-object.md)
  * [ColdBox Configuration](cachebox-configuration/coldbox-configuration.md)

## Usage

* [Cache Providers](cache-providers/README.md)
  * [Couchbase Providers](cache-providers/couchbase-providers.md)
  * [CF Providers](cache-providers/cf-providers.md)
  * [Railo Providers](cache-providers/railo-providers.md)
  * [Mock Provider](cache-providers/mock-provider.md)
  * [CacheBox Provider](cache-providers/cachebox-provider.md)
* [CacheBox Object Stores](cachebox-object-stores/README.md)
  * [ConcurrentStore](cachebox-object-stores/concurrentstore.md)
  * [ConcurrentSoftReferenceStore](cachebox-object-stores/concurrentsoftreferencestore.md)
  * [DiskStore](cachebox-object-stores/diskstore.md)
  * [JDBCStore](cachebox-object-stores/jdbcstore.md)
  * [BlackholeStore](cachebox-object-stores/blackholestore.md)

## Advanced Usage

* [CacheBox Eviction Policies](cachebox-eviction-policies/README.md)
  * [Using Your Own Policy](cachebox-eviction-policies/using-your-own-policy.md)
* [CacheBox Event Model](cachebox-event-model/README.md)
  * [CacheBox Events](cachebox-event-model/cachebox-events.md)
  * [Provider Events](cachebox-event-model/provider-events.md)
  * [Cache Listeners](cachebox-event-model/cache-listeners.md)
* [Cache Reporting](cache-reporting/README.md)
  * [Creating Your Own Skins](cache-reporting/creating-your-own-skins/README.md)
    * [Skin Templates](cache-reporting/creating-your-own-skins/skin-templates.md)
    * [ReportHandler](cache-reporting/creating-your-own-skins/reporthandler/README.md)
      * [Action Commands](cache-reporting/creating-your-own-skins/reporthandler/action-commands.md)

