# Manual Installation

If you are using CacheBox within a ColdBox application context, then CacheBox is part of the platform. Just install ColdBox normally. If you are using CacheBox standalone, just drop CacheBox in your application root or create a mapping called `CacheBox` that points to the installation folder. If you can run the following snippet, then CacheBox is installed correctly:

```
CacheBox = new wirebox.system.ioc.Injection();
```

> **Note** Please remember that if you use the standalone version the namespace is `cachebox.system.ioc` and if you use the ColdBox application version it is `coldbox.system.ioc`. From this point on, we will use the standalone namespace for simplicity.
<br>


# CommandBox Installation
You can leverage [CommandBox](http://www.ortussolutions.com/products/commandbox) to install the standalone version of CacheBox

```bash
box install cachebox
```
