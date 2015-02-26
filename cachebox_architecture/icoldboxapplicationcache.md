# IColdboxApplicationCache

*class : coldbox.system.cache.IColdboxApplicationCache*

This interface extends from the original cache provider interface and adds certain methods that MUST be implemented so the cache can work for ColdBox applications. This includes functionality to do event/view caching, clearing/expiring by certain regular expressions and reporting. So if you want to create your own cache implementation for ColdBox applications, then it must adhere to this contract.
