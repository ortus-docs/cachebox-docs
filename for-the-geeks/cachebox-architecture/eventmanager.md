# EventManager

**class** : `cachebox.system.core.events.EventPoolManager or coldbox.system.web.services.InterceptorService`

If you are in standalone mode then CacheBox configures its own internal event manager that is very similar to the ColdBox [Interceptor Service]([http://coldbox.ortusbooks.com/content/interceptors/interceptors.html](https://coldbox.ortusbooks.com/the-basics/interceptors)). This event manager keeps track of the listeners for each of the interceptions points or events that are broadcasted by CacheBox and its providers.
