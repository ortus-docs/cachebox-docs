# ReportHandler

This object is in charge of rendering skin templates and also executing processing commands. The custom tag creates this object and prepares it for usage, so do not worry about it, just know how to use it. The following are the variable compositions this object has and therefore you can use them in your skin templates:

| Variable | Type | Description |
| :--- | :--- | :--- |
| cacheBox | `cachebox.system.cache.CacheFactory` | A reference to the running CacheBox cache factory |
| baseURL | string | The baseURL attribute passed via the tag configuration |
| sking | string | The skin attribute passed via the tag configuration |
| skinPath | string | The non-expanded path to the skin in use. e.g. `/cachebox/system/cache/report/skin/MyCoolSkin` |
| attributes | struct | A reference to the attributes structure passed via the tag |
| caller | template | A reference to the caller page of the custom tag. |

This tag also has the following methods that you might be interested in:

| Return Type | Method |
| :--- | :--- |
| void | `processCommands(*[command=],[cacheName=default],[cacheEntry=])`   Execute and process a cacheBox command |
| any | `renderCachePanel()`   Render the `CachePanel.cfm` template |
| any | `renderCacheReport(cacheName)`  Render the `CacheReport.cfm` template which renders typically the report information about a specific cache provider |
| any | `renderCacheContentReport(cacheName)`   Render the `CacheContentReport.cfm` template which typically renders the report of the content of the cache provider |
| any | `renderCacheDumper(cacheName,cacheEntry)`    Tries to retrieve the `cacheEntry` from the cacheName provider and dumps it |

For example, here is a snippet of the CachePanel.cfm template to designate where the cache report for a specific cache provider will be rendered by default:

```javascript
<---  Named Cache Report --->
<div id="fw_cacheReport">#renderCacheReport()#</div>
```

Since no _cacheName_ argument is provided, it will use the default value of _default_. Here is a snippet of the cache report template of where it designates the content report to be rendered. It also verifies that the cache provider has reporting enabled and uses a custom attribute called _contentReport_.

```javascript
<---  Content Report --->
<cfif cacheProvider.isReportingEnabled() AND attributes.contentReport>
    <h3>Cache Content Report</h3>

    <---  Reload Contents --->
    <input type="button" value="Reload Contents"
           name="cboxbutton_reloadContents"
           style="font-size:10px"
           title="Reload the contents"
           onClick="fw_cacheContentReport('#URLBase#','#arguments.cacheName#')" />

    <---  Expire All Keys --->
    <input type="button" value="Expire All Keys"
           name="cboxbutton_expirekeys" id="cboxbutton_expirekeys"
           style="font-size:10px"
           title="Expire all the keys in the cache"
           onclick="fw_cacheContentCommand('#URLBase#','expirecache', '#arguments.cacheName#')" />

    <---  ColdBox Application Commands --->
    <cfif cacheBox.isColdBoxLinked()>
        <---  Clear All Events --->
        <input type="button" value="Clear All Events"
               name="cboxbutton_clearallevents" id="cboxbutton_clearallevents"
               style="font-size:10px"
               title="Remove all the events in the cache"
               onclick="fw_cacheContentCommand('#URLBase#','clearallevents', '#arguments.cacheName#')" />
        <---  Clear All Views --->
        <input type="button" value="Clear All Views"
               name="cboxbutton_clearallviews" id="cboxbutton_clearallviews"
               style="font-size:10px"
               title="Remove all the views in the cache"
               onclick="fw_cacheContentCommand('#URLBase#','clearallviews', '#arguments.cacheName#')" />
    </cfif>

    <---  Loader --->
    <span class="fw_redText fw_debugContent" id="fw_cacheContentReport_loader">Please Wait, Processing...</span>

    <div class="fw_cacheContentReport" id="fw_cacheContentReport">
        #renderCacheContentReport(arguments.cacheName)#
    </div>
</cfif>
```

