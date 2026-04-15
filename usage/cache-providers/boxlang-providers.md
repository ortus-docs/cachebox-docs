# BoxLang Providers

CacheBox ships two BoxLang-native cache providers that bridge the CacheBox API to the BoxLang runtime's built-in cache engine. Unlike the CF or Lucee providers, these providers do not depend on an external cache store — they delegate directly to BoxLang's own caching layer, which supports multiple named cache regions.

The two implementations follow the same pattern as other dual-mode providers:

1. `BoxLangProvider` — standalone provider, implements `ICacheProvider`
2. `BoxLangColdBoxProvider` — extends `BoxLangProvider` and implements `IColdBoxProvider` for ColdBox application usage (view/event caching)

## BoxLangProvider

**class**: `coldbox.system.cache.providers.BoxLangProvider`

### Properties

| Key | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| **cacheName** | string | false | `default` | The name of the BoxLang cache region to use. Multiple providers can map to different named regions. |

### Configuration Example

{% tabs %}
{% tab title="BoxLang" %}
```bx
// In your CacheBox configuration
cachebox = {
    defaultCache = {
        provider = "coldbox.system.cache.providers.BoxLangProvider",
        properties = {
            cacheName = "default"
        }
    },
    caches = {
        // A second provider pointing to a separate BoxLang cache region
        sessions : {
            provider   : "coldbox.system.cache.providers.BoxLangProvider",
            properties : { cacheName : "sessions" }
        }
    }
}
```
{% endtab %}
{% tab title="CFML" %}
```javascript
// In your CacheBox configuration
cachebox = {
    defaultCache = {
        provider = "coldbox.system.cache.providers.BoxLangProvider",
        properties = {
            cacheName = "default"
        }
    },
    caches = {
        // A second provider pointing to a separate BoxLang cache region
        sessions = {
            provider   = "coldbox.system.cache.providers.BoxLangProvider",
            properties = { cacheName = "sessions" }
        }
    }
};
```
{% endtab %}
{% endtabs %}

## BoxLangColdBoxProvider

**class**: `coldbox.system.cache.providers.BoxLangColdBoxProvider`

Extends `BoxLangProvider` and adds ColdBox-specific view and event caching support. It uses the following key prefixes when storing ColdBox-managed entries:

| Constant | Value | Purpose |
| --- | --- | --- |
| `VIEW_CACHEKEY_PREFIX` | `boxlang_view-` | Prefix for all view cache entries |
| `EVENT_CACHEKEY_PREFIX` | `boxlang_event-` | Prefix for all event cache entries |

### Configuration Example (ColdBox Application)

{% tabs %}
{% tab title="BoxLang" %}
```bx
// In config/CacheBox.bx or inside ColdBox.bx
cachebox = {
    defaultCache = {
        provider = "coldbox.system.cache.providers.BoxLangColdBoxProvider",
        properties = {
            cacheName = "default"
        }
    }
}
```
{% endtab %}
{% tab title="CFML" %}
```javascript
// In config/CacheBox.cfc or inside ColdBox.cfc
cachebox = {
    defaultCache = {
        provider = "coldbox.system.cache.providers.BoxLangColdBoxProvider",
        properties = {
            cacheName = "default"
        }
    }
};
```
{% endtab %}
{% endtabs %}

### ColdBox-Specific API Methods

In addition to the standard `ICacheProvider` methods, `BoxLangColdBoxProvider` exposes the full `IColdBoxProvider` interface:

| Method | Description |
| --- | --- |
| `clearAllEvents( [boolean async=false] )` | Clear all cached events |
| `clearEvent( required string eventSnippet, [string queryString=""] )` | Clear a specific cached event |
| `clearEventMulti( required string eventsnippets, [string queryString=""] )` | Clear multiple events by comma-delimited snippet list |
| `clearView( required string viewSnippet )` | Clear a specific cached view |
| `clearViewMulti( required string viewSnippets )` | Clear multiple views by comma-delimited snippet list |
| `clearAllViews( [boolean async=false] )` | Clear all cached views |

{% hint style="info" %}
BoxLang cache regions must be declared in the BoxLang runtime configuration (`boxlang.json`) before they can be referenced by `cacheName`. The `default` region is always available out of the box.
{% endhint %}
