---
title: Redis Client API
---

# Redis Client API

The Redis Client gives access to a [Redis](https://www.redis.io/) server.

=== "Overview"

- Module: `redis/client`
- Alias: `redis/client`
- Definition: [https://github.com/eclipse/dirigible/issues/723](https://github.com/eclipse/dirigible/issues/723)
- Source: [/redis/client.js](https://github.com/dirigiblelabs/ext-redis/blob/master/redis/client.js)
- Facade: [RedisFacade](https://github.com/eclipse/dirigible/blob/master/api/api-facade/api-redis/src/main/java/org/eclipse/dirigible/api/redis/RedisFacade.java)
- Status: `alpha`

### Basic Usage

```javascript
var response = require("http/v4/response");

var redis = require("redis/client");
var redisClient = redis.getClient();

// String commands

redisClient.set("name", "Alice");

var name = redisClient.get("name");
response.println(name); // Alice

var exists = redisClient.exists("name");
response.println(exists.toString()); // true

// List commands

redisClient.lpush("names", "Alice");
redisClient.lpush("names", "Bob");
redisClient.lpush("names", "Charlie");

redisClient.lpop("names");

var names = redisClient.lrange("names", 0, 1);
response.println(names.toString()); // [Bob, Alice]

response.flush();
response.close();
```

### Functions

---

| Function        | Description                                   | Returns  |
| --------------- | --------------------------------------------- | -------- |
| **getClient()** | Returns an object representing a Redis Client | _Client_ |

### Objects

---

#### Client

| Function                     | Description                                 | Returns   |
| ---------------------------- | ------------------------------------------- | --------- |
| **append(key, value)**       | Append a value to a key                     | _Number_  |
| **bitcount(key)**            | Count set bits in a string                  | _Number_  |
| **decr(key)**                | Decrement the integer value of a key by one | _Number_  |
| **exists(key)**              | Determine if a key exists                   | _Boolean_ |
| **get(key)**                 | Get the value of a key                      | _String_  |
| **incr(key)**                | Increment the integer value of a key by one | _Number_  |
| **keys(pattern)**            | Find all keys matching the given pattern    | _Array_   |
| **set(key, value)**          | Set the string value of a key               | _String_  |
| **lindex(key, index)**       | Get an element from a list by its index     | _String_  |
| **llen(key)**                | Get the length of a list                    | _Number_  |
| **lpop(key)**                | Remove and get the first element in a list  | _String_  |
| **lpush(key, value)**        | Prepend an element to a list                | _Number_  |
| **lrange(key, start, stop)** | Get a range of elements from a list         | _Array_   |
| **rpop(key)**                | Remove and get the last element in a list   | _String_  |
| **rpush(key, value)**        | Append an element to a list                 | _Number_  |
