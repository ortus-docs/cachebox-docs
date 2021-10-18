# What's New With 6.2.0

CacheBox 6.2.0 is a minor released under the main ColdBox 6.x umbrella.  Significant updates and release notes are below.  Please also note that LogBox is included with CacheBox, so all updates to the LogBox library are also updates of CacheBox 6.2.0.

## Release Notes

{% tabs %}
{% tab title="CacheBox" %}
### Improvements

* \[[COLDBOX-945](https://ortussolutions.atlassian.net/browse/COLDBOX-945)] - Event caching now bases off the multi host key from the event.getSESBaseURL() to improve consistencies and single responsibility
* \[[COLDBOX-953](https://ortussolutions.atlassian.net/browse/COLDBOX-953)] - Update `DateFormat` Mask to use lowercase "d" to be compatible with ACF2021
{% endtab %}

{% tab title="LogBox" %}
### Bugs

* \[[LOGBOX-56](https://ortussolutions.atlassian.net/browse/LOGBOX-56)] - Missing line break on file appender control string

### New Features

* \[[LOGBOX-57](https://ortussolutions.atlassian.net/browse/LOGBOX-57)] - new `shutdown() `method to process graceful shutdown of LogBox
* \[[LOGBOX-58](https://ortussolutions.atlassian.net/browse/LOGBOX-58)] - New logbox config `onShutdown()` callback, which is called when LogBox has been shutdown
* \[[LOGBOX-59](https://ortussolutions.atlassian.net/browse/LOGBOX-59)] - New `shutdown() `method can be now used in appenders that will be called when LogBox is shutdown
{% endtab %}
{% endtabs %}

