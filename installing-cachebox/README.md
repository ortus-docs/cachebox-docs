# Installing CacheBox

CacheBox has been designed to work either as a standalone framework or within the ColdBox Platform. So if you are building ColdBox applications, you do not have to do anything; CacheBox is already part of the platform. The main difference between both versions is the instantiation and usage namespace, the rest is the same.

The best way to install LogBox is using **CommandBox CLI and package manager**.

* [Download CacheBox Standalone](https://www.coldbox.org/download)
* [Download API Docs](apidocs.ortussolutions.com/cachebox/5.0.0/index.html)

## System Requirements

CacheBox has been designed to work under the following CFML Engines:

* Adobe ColdFusion 11+
* Lucee 4.5+

## Manual Installation

If you are using CacheBox within a ColdBox application context, then CacheBox is part of the platform. Just install ColdBox normally. If you are using CacheBox standalone, just drop CacheBox in your application root or create a mapping called `cachebox` that points to the installation folder. If you can run the following snippet, then CacheBox is installed correctly:

```text
cachebox = new cachebox.system.cache.CacheFactory();
```

> **Note** Please remember that if you use the standalone version the namespace is `cachebox.system.cache` and if you use the ColdBox application version it is `coldbox.system.cache`. From this point on, we will use the standalone namespace for simplicity.

## CommandBox Installation

You can leverage [CommandBox](https://www.ortussolutions.com/products/commandbox) to install the standalone version of CacheBox

```bash
# Latest CacheBox
box install cachebox

# Bleeding Edge
box install cachebox@be
```

## Namespaces

### Standalone

`cachebox.system.cache`

### ColdBox

`coldbox.system.cache`

> **Note** All examples in this book are based on the standalone namespace.

