# BlackholeStore

The `BlackholeStore` is not something you would actually deploy to a production site. The `BlackholeStore` is a development tool that simulates caching but never actually caches anything. This store can be useful to help tune an application as it can provide a solid baseline for how things would behave without caching. Anything set into a cache powered by the blackhole store will vanish into a blackhole. Anytime a lookup is performed it will appear is if that object has expired. Finally, if you actually try to get and object you will receive a `null`.

## Properties 
* *None*