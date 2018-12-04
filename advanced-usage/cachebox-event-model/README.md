# CacheBox Event Model

CacheBox also sports a very nice event model that can announce several cache life cycle events and factory life cycle events. You can listen to these events and interact with caches at runtime very easily, whether you are in standalone mode or within a ColdBox application.

Of course, if you are within a ColdBox application, you get the benefit of all the potential of ColdBox Interceptors and if you are in standalone mode, well, you just get the listener and that's it.

Each event execution also comes with a structure of name-value pairs called `interceptData` that can contain objects, variables and all kinds of data that can be useful for listeners to use. This data is sent by the event caller and each event caller decides what this data sent is.

