# XML Configuration

```javascript
config = createObject("component","coldbox.system.cache.config.CacheBoxConfig").init(expandPath("/config/cacheBox.xml"));
```

However, if you have your XML in a variable already, maybe you read it from a database or other location, you can still use it by calling the config object's parseAndLoad() method.

```javascript
//Get the xml document from somewhere.
xmlDoc = dbService().getCacheBoxConfig();
//create the CacheBox config object
config = createObject("component","coldbox.system.cache.config.CacheBoxConfig").init();
config.parseAndLoad(xmlDoc);
```

Sample *cacheBox.xml* file:

```javascript
<?xml version="1.0" encoding="UTF-8"?>
<CacheBox xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="http://www.coldbox.org/schema/CacheBoxConfig_1.0.xsd">

    <-- < The LogBox Configuration File to Use -->
    <LogBoxConfig>coldbox.system.cache.config.LogBoxConfig</LogBoxConfig>

    <-- <Scope Registration -->
    <ScopeRegistration enabled="true" scope="server" key="cachebox1" />

    <-- <The defaultCache has an implicit name "default" which is a reserved cache name
         It also has a default provider of cachebox which cannot be changed.
         All timeouts are in minutes -->
    <DefaultConfiguration
        objectDefaultTimeout="60"
        objectDefaultLastAccessTimeout="30"
        useLastAccessTimeouts="true"
        reapFrequency="2"
        freeMemoryPercentageThreshold="0"
        evictionPolicy="LRU"
        evictCount="1"
        maxObjects="100"
        objectStore="ConcurrentSoftReferenceStore"
        coldboxEnabled="true" />

    <-- < Register all the named caches below -->
    <Cache name="SampleCache1" provider="coldbox.system.cache.providers.CacheBoxProvider">
        <Properties
            objectDefaultTimeout="20"
            useLastAccessTimeouts="false"
            reapFrequency="1"
            evictionPolicy="LFU"
            evictCount="1"
            maxObjects="100"
            objectStore="ConcurrentSoftReferenceStore" />
    </Cache>
    <Cache name="sampleCache2" provider="coldbox.system.cache.providers.CacheBoxProvider">
        <Properties maxObjects="500"
                    evictionPolicy="FIFO" />
    </Cache>

    <-- < Register cache listeners -->
    <CacheListeners>
        <Listener class="test.path.Listner" name="SampleListner">
            <Property name=""></Property>
        </Listener>
    </CacheListeners>

</CacheBox>
```
As you can see the XML elements translate to the CacheBox DSL elements, so please refer to them for their meaning. The root element must be *&lt;CacheBox&gt;* with the following child elements:

* *&lt;LogBoxConfig&gt;*: The location of the LogBox configuration file.
* *&lt;ScopeRegistration&gt;* : The scope registration for the factory
    * *@scope* : The ColdFusion scope
    * *@key* : The key in the scope
    * *@enabled* : True/False to enable registration
* *&lt;DefaultConfiguration&gt;* : The default reserved cache configuration. All attributes match the CacheBox DSL default cache properties.
    * *@objectDefaultTimeout*
    * *@objectDefaultLastAccessTimeout*
    * *@useLastAccessTimeouts*
    * *@reapFrequency*
    * *@freeMemoryPercentageThreshold*
    * *@evictionPolicy*
    * *@evictCount*
    * *@maxObjects*
    * *@objectStore*
    * *@coldboxEnabled*
* *&lt;Cache&gt;* : A cache configuration, you can have as many as you like of these elements. They also match exactly to the caches element in the CacheBox DSL.
    * *@name* : Mandatory unique name for the cache.
    * *@provider* : The class of the provider
    * *&lt;Properties&gt;* : Optional child element that you can use to configure the name-value pairs of configuration properties for the cache. Each property is an attribute of this XML element.
* *&lt;CacheListeners&gt;* : A container element for all the cache listeners to register
    * *&lt;Listener&gt;* : A listener declaration
        * *@class* : The instantiation class
        * *@name* : The unique name of the listener, not mandatory, defaults to the filename in the class attribute
        * *&lt;Property&gt;* : 0 or more configuration properties for the listener
            * *@name* : Name of the property
            * *XMLValue* : The value of the XML element is the value of the property.

To make this XML configuration easier, CacheBox comes with its own XML Schema that can be found in the following location:

```javascript
/coldbox/system/cache/config/CacheBoxConfig.xsd
or
/cachebox/system/cache/config/CacheBoxConfig.xsd
or
http://www.coldbox.org/schema/CacheBoxConfig_1.0.xsd
```

You can also add the location to your XML header so your IDE can give you introspection and validation:

```javascript
<?xml version="1.0" encoding="UTF-8"?>
<CacheBox xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="http://www.coldbox.org/schema/CacheBoxConfig_1.0.xsd">

</CacheBox>
```

> **Info** Note: Please note the version identifier in the online schema, make sure you have the correct version when using within an IDE.



