---
description: June 21, 2022
---

# What's New With 6.7.0

## Release Notes

{% tabs %}
{% tab title="CacheBox" %}
**Bug**

* [CACHEBOX-66](https://ortussolutions.atlassian.net/browse/CACHEBOX-66) Cachebox concurrent store meta index not thread safe during reaping

**Improvement**

* [CACHEBOX-82](https://ortussolutions.atlassian.net/browse/CACHEBOX-82) Remove the usage of identity hash codes, they are no longer relevant and can cause contention under load
{% endtab %}

{% tab title="LogBox" %}
**Improvement**

* [LOGBOX-68](https://ortussolutions.atlassian.net/browse/LOGBOX-68) Remove the usage of identity hash codes, they are no longer relevant and can cause contention under load
* [LOGBOX-65](https://ortussolutions.atlassian.net/browse/LOGBOX-65) File Appender missing text "ExtraInfo: "
{% endtab %}
{% endtabs %}
