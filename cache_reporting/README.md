# Cache Reporting

CacheBox comes with great reporting tools whether you are using it within a ColdBox application or standalone. This section deals with how to do a-la-carte reporting by using the custom tags that CacheBox ships with. Below is the simplest form of usage for the monitor reporting tags:

```javascript
<cfimport prefix="cachebox" taglib="/cachebox/system/cache/report">

<---  Create CacheBox with default configuration --->
<cfif structKeyExists(url,"reinit") OR NOT structKeyExists(application,"cacheBox")>
    <cfset application.cacheBox   = new cachebox.system.cache.CacheFactory()>
<cfelse>
    <cfset cachebox = application.cacheBox>
</cfif>

<cfoutput>
<html>

    <head>
        <title>CacheBox Monitor Tool</title>
    </head>
    <body>

    <---  Special ToolBar --->
    <div id="toolbar">
        <input type="button" value="Reinit" onclick="window.location='index.cfm?reinit'"/>
    </div>

    <---  Render Report Here --->
    <cachebox:monitor cacheFactory="#cacheBox#"/>

    </body>
</html>
</cfoutput>
```

<img src="../images/cachemonitor.jpg">

That's it! You basically import the tag library from */cachebox/system/cache/report* and then use the monitor tag to render out the monitor. What's cool about the monitor is that it is completely skinnable. Please see the CacheBox Report Skins for more information. 

## Attributes
Let's check out the attributes for this custom tag:

|Attribute|Type|Required|Default|Description|
|--|--|--|--|--|
|cacheFactory |*cachebox.system.cache.CacheFactory *|true|---|The reference to the CacheBox factory to report on.|
|baseURL |string|false|cgi.script_name |The location of the script so the tag can create links for Ajax calls and rendering calls.|
|sking|string|false|*default*|The name of the skin to use for rendering the report. The skins are found at /coldbox/system/cache/report/skins.|

> **Important** Each skin can implement its own attributes, so always check the skins documentation to see what extra attributes it implements.

Here are some examples of the tag usage:

```javascript
<cachebox:monitor cacheFactory="#cacheBox#"/>

<cachebox:monitor cacheFactory="#cacheBox#" baseURL="index.cfm?event=cacheMonitor"/>

<cachebox:monitor cacheFactory="#cacheBox#" skin="coolskin"/>

<---  Embedding report in a coldbox application's admin view --->
<cachebox:monitor cacheFactory="#controller.getCacheBox()#"
          baseURL="#event.buildLink(event.getCurrentEvent())#" />
```


