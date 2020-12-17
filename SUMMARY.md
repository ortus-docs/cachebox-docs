# Table of contents

* [Introduction](README.md)

## Intro

* [Introduction](intro/readme/README.md)
  * [What's New With 5.4.0](intro/readme/whats-new-with-5.4.0.md)
  * [What's New With 5.0.0](intro/readme/whats-new-with-500.md)
  * [About This Book](intro/readme/about-this-book.md)
  * [Author](intro/readme/author.md)

## Getting Started

* [Overview](getting-started/overview/README.md)
  * [CacheBox RefCard](getting-started/overview/cachebox-refcard.md)
  * [Useful Resources](getting-started/overview/useful-resources.md)
  * [Features at a Glance](getting-started/overview/features-at-a-glance.md)
* [Installing CacheBox](getting-started/installing-cachebox.md)
* [Creating CacheBox](getting-started/creating-cachebox/README.md)
  * [Common CacheFactory Methods](getting-started/creating-cachebox/common-cachefactory-methods.md)
  * [Cache Cleanup/Reaping](getting-started/creating-cachebox/cache-cleanup-reaping.md)

## For The Geeks

* [Caching Concepts](for-the-geeks/caching-concepts/README.md)
  * [Caching Considerations](for-the-geeks/caching-concepts/caching-considerations.md)
  * [Cache Loading](for-the-geeks/caching-concepts/cache-loading.md)
  * [Definitions](for-the-geeks/caching-concepts/definitions.md)
  * [Java Soft References](for-the-geeks/caching-concepts/java-soft-references.md)
* [Cache Topologies](for-the-geeks/cache-topologies/README.md)
  * [Single Instance/In-Process](for-the-geeks/cache-topologies/single-instance-in-process.md)
  * [Single Instance/Out-Process](for-the-geeks/cache-topologies/single-instance-out-process.md)
  * [Replicated](for-the-geeks/cache-topologies/replicated.md)
  * [Distributed](for-the-geeks/cache-topologies/distributed.md)
* [CacheBox Architecture](for-the-geeks/cachebox-architecture/README.md)
  * [CacheFactory](for-the-geeks/cachebox-architecture/cachefactory.md)
  * [CacheBoxConfig](for-the-geeks/cachebox-architecture/cacheboxconfig.md)
  * [EventManager](for-the-geeks/cachebox-architecture/eventmanager.md)
  * [ColdBox](for-the-geeks/cachebox-architecture/coldbox.md)
  * [LogBox](for-the-geeks/cachebox-architecture/logbox.md)
  * [ICacheProvider](for-the-geeks/cachebox-architecture/icacheprovider.md)
  * [ICacheStats](for-the-geeks/cachebox-architecture/icachestats.md)
  * [IObjectStore](for-the-geeks/cachebox-architecture/iobjectstore.md)
  * [IEvictionPolicy](for-the-geeks/cachebox-architecture/ievictionpolicy.md)
  * [AbstractEvictionPolicy](for-the-geeks/cachebox-architecture/abstractevictionpolicy.md)
  * [IColdboxApplicationCache](for-the-geeks/cachebox-architecture/icoldboxapplicationcache.md)

## Configuration

* [CacheBox Configuration](configuration/cachebox-configuration/README.md)
  * [CacheBox DSL](configuration/cachebox-configuration/cachebox-dsl/README.md)
    * [LogBoxConfig](configuration/cachebox-configuration/cachebox-dsl/logboxconfig.md)
    * [Scope Registration](configuration/cachebox-configuration/cachebox-dsl/scope-registration.md)
    * [Default Cache](configuration/cachebox-configuration/cachebox-dsl/default-cache.md)
    * [Caches](configuration/cachebox-configuration/cachebox-dsl/caches.md)
    * [Listeners](configuration/cachebox-configuration/cachebox-dsl/listeners.md)
  * [CacheBox Config Object](configuration/cachebox-configuration/cachebox-config-object.md)
  * [ColdBox Configuration](configuration/cachebox-configuration/coldbox-configuration.md)

## Usage

* [Cache Providers](usage/cache-providers/README.md)
  * [CF Providers](usage/cache-providers/cf-providers.md)
  * [Lucee Providers](usage/cache-providers/lucee-providers.md)
  * [Mock Provider](usage/cache-providers/mock-provider.md)
  * [CacheBox Provider](usage/cache-providers/cachebox-provider.md)
  * [Couchbase Providers](usage/cache-providers/couchbase-providers.md)
* [CacheBox Object Stores](usage/cachebox-object-stores/README.md)
  * [ConcurrentStore](usage/cachebox-object-stores/concurrentstore.md)
  * [ConcurrentSoftReferenceStore](usage/cachebox-object-stores/concurrentsoftreferencestore.md)
  * [DiskStore](usage/cachebox-object-stores/diskstore.md)
  * [JDBCStore](usage/cachebox-object-stores/jdbcstore.md)
  * [BlackholeStore](usage/cachebox-object-stores/blackholestore.md)

## Advanced Usage

* [CacheBox Eviction Policies](advanced-usage/cachebox-eviction-policies/README.md)
  * [Using Your Own Policy](advanced-usage/cachebox-eviction-policies/using-your-own-policy.md)
* [CacheBox Event Model](advanced-usage/cachebox-event-model/README.md)
  * [CacheBox Events](advanced-usage/cachebox-event-model/cachebox-events.md)
  * [Provider Events](advanced-usage/cachebox-event-model/provider-events.md)
  * [Cache Listeners](advanced-usage/cachebox-event-model/cache-listeners.md)
* [Cache Reporting](advanced-usage/cache-reporting/README.md)
  * [Creating Your Own Skins](advanced-usage/cache-reporting/creating-your-own-skins/README.md)
    * [Skin Templates](advanced-usage/cache-reporting/creating-your-own-skins/skin-templates.md)
    * [ReportHandler](advanced-usage/cache-reporting/creating-your-own-skins/reporthandler/README.md)
      * [Action Commands](advanced-usage/cache-reporting/creating-your-own-skins/reporthandler/action-commands.md)

