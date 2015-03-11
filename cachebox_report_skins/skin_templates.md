# Skin Templates

The first step of creating skin templates is to create its holding folder inside of the `skins` directory. So if we were starting a new skin called `goodness` then you would create a new folder in the following directory:

```javascript
/cachebox/system/cache/report/skins/goodness
```

The following templates are the ones you will be skinning and placing in this folder. In all reality you could potentially just have one, `CachePanel.cfm`. However, since you can bring in AJAX content to refresh certain parts of the panel, you break out its reporting functionality into various templates. The CFC in charge of rendering your skin templates is the `ReportHandler.cfc` located in the same report package, so we recommend also reading its API for more in depth information. So let's explore them:

|Template|Required|Description|
|--|--|--|
| cachebox.js | true | The JavaScript file that will be automatically loaded into the header content via a `cfhtmlhead` call. You can put any JavaScript you like here or load more JavaScript files via your skin templates.|
| cachebox.css | true | The css file that will be automatically loaded into the header content via a `cfhtmlhead` call.|
| CachePanel.cfm | true | The main template that displays the report monitor to the user. This skin could potentially hold action buttons and other parts of the cache report rendered in specific locations by using rendering methods (see ReportHandler section).|
| CacheReport.cfm | false | This template is usually rendered via the `renderCacheReport(cacheName)` method and it is supposed to render out a report of the cache provider using the incoming `cacheName` argument. This template usually has a call somewhere for the content report of such cache provider via the `renderCacheContentReport(cacheName)` method.|
| CacheContentReport.cfm | false | This template is usually rendered via the `renderCacheContentReport(cacheName)` method and it is supposed to render out a report of the contents of the cache provider using the incoming `cacheName` argument. This table of contents can also have action buttons assigned to them.|

> **Info** : All skins are rendered within the `ReportHandler` component. This means that you have access to this object's methods and local variables. We recommend you look at the default skin's templates for usage.

