- In order to **store a single data** instance on Redis 
``` lua
SET key_name key_value
``` 

- Instead to **collect**
	``` lua
GET key_name
```

- To check if **exists or not**
``` lua
EXISTS key_name
```
It return 1 if the field exists, 0 otherwise.

- To **delete** **something** we need only the key_name
``` lua
DEL key_name
```
- it's possible to **update** the **key-value pairs** using a series of operators
``` lua
INCR key_name
DECR key_name
INCRBY key_name value
DECRBY key_name value
``` 
- It's possible to execute scripting with **Atomic Operations**
``` lua
x = GET key_name
x = x+1
SET key_name x
```

- **Temporary key-value pairs** using the following operators
**Expire** -  Set the lifespan of a variable (second)
**TTL** - Returns the remaining lifespan of a variable (second)
To achieve the same result in ms, just add p at the start of the words.

>the possible results are: 
>-1, The key will never expire
>-2  The key has already expired
>the remaining lifetime

To store permanently a TTL variable just write:
``` lua
PERSIST key_name
``` 

#### List
It's possible to manage **data structures**, like **LIST**.
- In order to create it, it's enough to write **RPUSH** (end) or **LPUSH** (beginning).
Note: If they key is empty it will be deleted, as well if it doesn't exists it'll be created.

``` lua
LRANGE key_name first_index last_index
```
In the first index there're only positive number, instead on the last could be negative too.
"-N" implies that will be returned all value besides the "N-1" values.

- To remove items from the list there're LPOP e RPOP 
``` lua
LPOP key_name
```
- It's also possible to obtain the length 

``` lua
LLEN key_name
```

#### Set
they are like the List but they don't have a specific value order and each value can only appear once per set.
- Adds one or more values to a list. Return 1 if the element is correctly added, 0 otherwise.

``` lua
SSAD key_name key_value0, key_value1, ...
```
- Remove one or more elements from a set. Return 1 if the element is correctly removed, 0 otherwise.
``` lua
SREM key_name key_value0, key_value1, ...
```
- Check if it's part of the set. Return 1 if the value is part of the set
``` lua
SIMEMEBER key_name key_value
```
- Returns all the members in the set
``` lua
SMEMBER key_name
```
- Combine two or more set into one set
``` lua
SUNION key_name1, key_name2, ...
```
- Since they're not ordered, it's possible to order it assigning a score that's used to define the order in the set
``` lua
/* in order to order */
ZADD key_name key_score key_value1 ...

/* in order to retrieve */
ZRANGE key_name first_index last_index
```

#### Hashes
Hashes are the best way to store objects, they are mapping between string fields and string values.
- Create a hash and assign one or more string fields with their values of the hash.
 ``` lua
 HSET key_name field_1 value_1 field_2 value_2 etc.
 ```
 - Returns a hash with its field HGETALL
 - Returns a single field from a hash HGET