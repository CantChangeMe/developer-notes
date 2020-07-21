# Difference between Hashtable and Collections.synchronizedMap
|Collections.synchronizedMap| Hashtable|
|---------------------------|----------|
|Methods are synchronized at block level using mutex|synchronization is on method level|
|The developer is allowed to pass another object of the mutex as a second argument by which the lock on the Map methods would be only on that Object and hence less restrictive| More restrictive than synchronized map locking in Collections.synchronizedMap can be done at object level while constructing Map.If object is not provided then|

# Difference between Hashtable and HashMap
|Hashtable|HashMap  |
|---------|---------|
|Hashtable is synchronized|HashMap is not synchronized. This makes HashMap better for non-threaded applications, as unsynchronized Objects typically perform better than synchronized ones.|
|Hashtable does not allow null keys or values|HashMap allows one null key and any number of null values|
|This wouldn't be as easy if you were using Hashtable|One of HashMap's subclasses is LinkedHashMap, so in the event that you'd want predictable iteration order (which is insertion order by default), you could easily swap out the HashMap for a LinkedHashMap|

# Difference between HashTables/SynchronizedMaps and ConcurrentHashMap

|HashTables/SynchronizedMaps|ConcurrentHashMap  |
|---------|---------|
|Whole Map is locked in case of HashTables/SynchronizedMaps.|locking particular portion/ segment|
