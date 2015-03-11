# DiskStore

The `DiskStore` as its name implies, uses a disk to store cached objects under. This can be any location that can be accessible via `cffile and cfdirectory`. Therefore, you can use Railo/Lucee resources or virtual RAM locations or even Amazon S3. You can get funky my friends!

Anyways, this storage will look at the incoming target object to cache and if it is a complex object it will serialize to binary and store it on disk. If it is a simple value, it just saves it. This is a great way to provide a centralized template/view caching mechanisms as views are simple strings. You can even connect a farm of servers to talk to a centralized network drive that has centralized view/event template storage. Anyways, you can get funky!

## Properties 

|Key|Type|Required|Default|Description|
|--|--|--|--|--|
|autoExpandPath |Boolean |false |true |A flag that indicates if the store should use `expandPath()` to figure out the path to store objects in.|
|directoryPath |string |true |---|The directory path to use to store cached objects under. This can be relative or absolute. |


