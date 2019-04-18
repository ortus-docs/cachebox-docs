# What's New With 5.4.0

## Release Notes

### Bugs

* \[[CACHEBOX-46](https://ortussolutions.atlassian.net/browse/CACHEBOX-46)\] - CacheboxProvider metadata and stores: use CFML functions on java hash maps breaks concurrency
* \[[CACHEBOX-50](https://ortussolutions.atlassian.net/browse/CACHEBOX-50)\] - getOrSet\(\) provider method doesn't work with full null support
* \[[CACHEBOX-52](https://ortussolutions.atlassian.net/browse/CACHEBOX-52)\] - getQuiet\(\), clearQuiet\(\), getSize\(\), clearAll\(\), expireAll\(\) broken in acf providers

### New Features

* \[[CACHEBOX-48](https://ortussolutions.atlassian.net/browse/CACHEBOX-48)\] - New setting: \`resetTimeoutOnAccess\` to allow the ability to reset timeout access for entries
* \[[CACHEBOX-49](https://ortussolutions.atlassian.net/browse/CACHEBOX-49)\] - Global script conversion and code optimizations
* \[[CACHEBOX-53](https://ortussolutions.atlassian.net/browse/CACHEBOX-53)\] - lookup operations on ACF providers updated to leverage cacheIdExists\(\) improves operation by over 50x
* \[[CACHEBOX-54](https://ortussolutions.atlassian.net/browse/CACHEBOX-54)\] - setMulti\(\), getMulti\(\), lookupMulti\(\), clearMulti\(\),getCachedObjectMetadataMulti\(\) is now available on all cache providers

### Improvements

* \[[CACHEBOX-47](https://ortussolutions.atlassian.net/browse/CACHEBOX-47)\] - Increased timeout on \`getOrSet\` lock
* \[[CACHEBOX-51](https://ortussolutions.atlassian.net/browse/CACHEBOX-51)\] - Consolidated usages of the abstract cache provider to all providers to avoid redundancy

