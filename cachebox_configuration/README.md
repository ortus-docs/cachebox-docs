# CacheBox Configuration

Let's delve deeper into the rabbit hole and explore how to configure this bad boy. Our preference is the programmatic approach via a simple data CFC that can encapsulate the CacheBox configuration in one single component. However, at the end of the day all configuration approaches will use the `CacheBoxConfig` object's methods in some manner. 

This is the CFC that you will use to configure CacheBox and its constructor can be called with the following optional arguments which determines your configuration approach:

* `none` - Means you will be using the CFCs methods for configuration
* `CFCConfig` - The object reference to the simple data CFC that contains the CacheBox DSL
* `CFCConfigPath` - The instantiation path of the simple data CFC that contains the CacheBox DSL

No matter what configuration you decide to use, you will always have to instantiate CacheBox with a `CacheBoxConfig` object of type: `cachebox.system.cache.config.CacheBoxConfig`. However, you have the option of either working with this CFC directly or creating a more portable configuration.

This portable configuration we denote as a simple data CFC that contains the CacheBox configuration data that represents our CacheBox DSL (Domain Specific Language). This DSL is exactly the same if you are using CacheBox standalone or in any ColdBox application, so it definitely has its benefits.

> **Tip**: Please note that you have full access to the running CacheBox's configuration object or even a specific cache's configuration structure. Therefore, you can easily change the configuration settings for a cache or CacheBox dynamically at runtime.
