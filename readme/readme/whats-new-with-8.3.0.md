---
description: October 13, 2026
---

# What's New With 8.3.0

You can read the complete ecosystem changes in the [ColdBox 8.3.0 release notes](https://coldbox.ortusbooks.com/readme/release-history/whats-new-with-8.3.0).

## Release Notes

{% tabs %}
{% tab title="CacheBox" %}

### Integration

WireBox's scope-wiring fix also affects CacheBox-scoped objects: other threads now wait until an object's dependencies are injected instead of receiving a partially wired instance ([COLDBOX-1455](https://ortussolutions.atlassian.net/browse/COLDBOX-1455)). See the [WireBox 8.3.0 release notes](https://wirebox.ortusbooks.com/readme/introduction/whats-new-with-8.3.0) for the complete scope changes.
{% endtab %}
{% endtabs %}
