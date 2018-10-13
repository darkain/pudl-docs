## PUDL Constants


### PUDL_RECURSION
* Value: 32
* Usage: This defines the maximum recursion limit for internal methods that can be executed multiple times from a single API call. This prevents the internal PHP call stack from overflowing, and instead throws a [pudlRecursionException](../exceptions/pudlRecursionException.md).



### PUDL_NONE
* Value: 0x00
* Usage: Default "_do nothing_".



### PUDL_START
* Value: 0x01
* Usage: Used with "_LIKE_" queries to add a "_%_" wildcard before the string to search.



### PUDL_END
* Value: 0x02
* Usage: Used with "_LIKE_" queries to add a "_%_" wildcard after the string to search.


### PUDL_BOTH
* Value: 0x03
* Usage: Used with "_LIKE_" queries to add a "_%_" wildcard before and after the string to search.


### PUDL_CSV
* Value: 0x10
* Usage: Used with [pudlObject](../pudlObject) when importing data. This tells the new pudlObject that imported data is a CSV string that needs to be parsed.
