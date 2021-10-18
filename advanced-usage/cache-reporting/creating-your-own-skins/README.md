# Creating Your Own Skins

## Creating Your Own Skins

CacheBox also allows for the creation of reporting skins so you can create gorgeous looking reports for its caches, configurations, content, etc. The location of such skins is in the following location:

```javascript
/cachebox/system/cache/report/skins
```

The name of the folder inside of the skins folder is the unique name used to specify the skin in the custom tag. You can look at the default skin to learn from it and see how you can build skins yourself.

### Skin Attributes

A skin receives attributes or configuration elements via the custom tag used for the report monitor. Basically any attribute you add to the custom tag will be available in the skin's pages in a structure called `attributes`, makes sense huh?

## Tag Caller

A skin also receives a reference to the `caller` scope via a variable called, drum roll please, `caller`. So you can also reference the `caller` variables via this scope.
