# Installing CacheBox

**CacheBox** can be installed as a standalone framework or included with the latest ColdBox Platform release, so it is unnecessary if you are within a ColdBox application.

## System Requirements

* Adobe ColdFusion 2018+
* Lucee 5+

## Standalone Installation

You can leverage [CommandBox](http://www.ortussolutions.com/products/commandbox) to install the standalone version of CacheBox with a simple command:

```bash
# Latest Version
box install cachebox

# Bleeding Edge
box install cachebox@be
```

This will install CacheBox as a dependency in your application into a folder called `cachebox`. You can then leverage the standalone namespace within your application: `cachebox.system.ioc`.

### Mappings

You will need the following mapping that points to the folder you installed `cachebox` into:

```cfscript
this.mappings[ "/cachebox" ] = "path.to.cachebox";
```

This will ensure that the appropriate libraries can find each other.

{% hint style="danger" %}
Remember that this only applies to the standalone approach.
{% endhint %}
