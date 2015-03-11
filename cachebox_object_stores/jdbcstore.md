# JDBCStore

The `JDBCStore` is a nice object storage that leverages a single database table to keep track of its objects. This is great for simple or small scale clusters that need centralized caching. It also follows suit that complex objects are serialized into the tables and simple objects are just saved. The object store can even create the database table for you if need be via its own object store custom properties.

## Properties 

|Key|Type|Required|Default|Description|
|--|--|--|--|--|
|dsn|string|true|---|The datasource to connect to|
|table|string|true|---|The table we will be caching to|
|dsnUsername |string|false| |The DSN username if used|
|dsnPassword |string|false| |The DSN password if used|
|tableAutoCreate |Boolean|false|true|The object store can create the repository table for you if need be and if it does not exist.|



