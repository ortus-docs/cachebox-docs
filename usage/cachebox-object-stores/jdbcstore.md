# JDBCStore

The `JDBCStore` is a nice object storage that leverages a single database table to keep track of its objects. This is great for simple or small scale clusters that need centralized caching. It also follows suit that complex objects are serialized into the tables and simple objects are just saved. The object store can even create the database table for you if need be via its own object store custom properties.

## Properties

| Key                 | Type    | Required | Default | Description                                                                                   |
| ------------------- | ------- | -------- | ------- | --------------------------------------------------------------------------------------------- |
| **dsn**             | string  | true     | ---     | The datasource to connect to                                                                  |
| **table**           | string  | true     | ---     | The table we will be caching to                                                               |
| **dsnUsername**     | string  | false    |         | The DSN username if used                                                                      |
| **dsnPassword**     | string  | false    |         | The DSN password if used                                                                      |
| **tableAutoCreate** | Boolean | false    | true    | The object store can create the repository table for you if need be and if it does not exist. |

## Adobe ColdFusion + CFTransaction Notes

Adobe ColdFusion (ACF) engines require all `queryExecute()` statements running within a transaction to have identical `datasource`, `username`, and `password` options.  If your application uses the JDBCStore within a `<cftransaction>` block you may receive the following error message *"Usernames and Passwords for all the database tags within the cftransaction tag must be the same"*.  If your application sets the default DSN using `this.datasource` in your Application.cfc file, you may be able to work around the issue by omitting the `dsn`, `dsnUsername`, and `dsnPassword` properties from the JDBCStore.
