
Link : http://qnimate.com/overview-of-redis-architecture/#prettyPhoto

# Redis in-memory cache

- Redis is the most popular in-memory, key-value data store. 
- Amazon Elastic Cache supports Redis which makes redis a very powerful and must know key-value data store. 

## What Is In-Memory, Key-Value Store
Key-Value store is a storage system where data is stored in form of key and value pairs. When we say in-memory key-value store, by that we mean that the key-value pairs are stored in primary memory(RAM). So we can say that Redis stored data in RAM in form of key-value pairs.

In Redis, <mark>key has to be a string</mark> but value can be a string, list, set, sorted set or hash.

These are some example of Redis key-values pairs

name="Kishore"

profession=["web", "mobile"]

Here name and profession are keys. And we have their respective values on right.

### Advantage And Disadvantage of Redis over DBMS
Database Management systems store everything in second storage which makes read and write operations very slow. But Redis stores everything in primary memory which is very fast in read and write of data.

Primary memory is limited(much lesser size and expensive than secondary) therefore Redis cannot store large files or binary data. It can only store those small textual information which needs to be accessed, modified and inserted at a very fast rate. If we try to write more data than available memory then we will receive errors.

## Redis Single Instance Architecture
Redis architecture contains two main processes: 
- Redis client and 
- Redis Server.

![redis-client-server](../images/redis-client-server.jpg)

Redis client and server can be in the same computer or in two different computers.

Redis server is responsible for storing data in memory. It handles all kinds of management and forms the major part of architecture. Redis client can be Redis console client or any other programming language's Redis API.

As we saw that Redis stores everything in primary memory. Primary memory is volatile and therefore we will loose all stored data once we restart our Redis server or computer. Therefore we need a way for datastore persistance.

## Redis Persistance
There are three different ways to make Redis persistance: RDB, AOF and SAVE command.

### RDB Mechanism (Redis Database File)

It's the snapshot style persistence format.

RDB makes a copy of all the data in memory and stores them in secondary storage(permanent storage). This happens in a specified interval. So there is chance that you will loose data that are set after RDB's last snapshot.

### AOF (Append Only File)

It's the change-log style persistent format.

AOF logs all the write operations received by the server. Therefore everything is persistance. The problem with using AOF is that it writes to disk for every operation and it is a expensive task and also size of AOF file is large than RDB file.

### SAVE Command

You can force redis server to create a RDB snapshot anytime using the redis console client SAVE command.

You can use AOF and RDB together to get best persistance result.

For more information of Redis persistance refer this official documentation.

## Backup And Recovery Of Redis DataStore
Redis does not provide any mechanism for datastore backup and recovery. Therefore if there is any hard disk crash or any other kind of disaster then all data will be lost. You need to use some third party server backup and recovery softwares to workaround it.

- If you are using Redis in a replicated environment then there is no need for backup.

## Redis Replication
Replication is a technique involving many computers to enable fault-tolerance and data accessibility. In a replication environment many computers share the same data with each other so that even if few computers go down, all the data will be available.

This image shows a basic Redis replication
redis-replication

![redis-replilcation](../images/redis-replication.jpg)


Master and slaves are redis servers configured as such.

All the slaves contain exactly same data as master. There can be as many as slaves per master server. When a new slave is inserted to the environment, the master automatically syncs all data to the slave.

All the queries are redirected to master server, master server then executes the operations. When a write operation occurs, master replicates the newly written data to all slaves. When a large number sort or read operation are made, master distributes them to the slaves so that a large number of read and sort operations can be executed at a time.

If a slave fails, then also the environment continues working. when the slave again starts working, the master sends updated data to the slave.

If there is a crash in master server and it looses all data then you should convert a slave to master instead of bringing a new computer as a master. If we make a new computer as master then all data in the environemt will be lost because new master will have no data and will make the slaves also to have zero data(new master does resync ). If master fails but data is persistent(disk not crashed) then starting up the same master server again will bring up the whole environment to running mode.

Replication helped us from disk failures and other kinds of hardware failures. It also helped to execute multiple read/sort queries at a time.

For more detailed information on redis replication read this official documentation.

## Persistance In Redis Replication
We saw how persistance can tackle unexpected failures and keep our backend strong. But one way whole data can be lost is if the whole replicated environment goes down due to power failure. This happens because all data is stored in primary memory. So we need persistance here also.

We can configure master or any one slave to store data in secondary storage using any method(AOF and RDB). Now when the whole environment is again started, make the persistent server as the master server.

Using persistance and replication together all our data is completely safe and protected from unexpected failures.

## Clustering In Redis
Clustering is a technique by which data can be sharded(divided) into many computers. The main advantage is that more data can be stored in a cluster because its a combination of computers.

Suppose we have one redis server with 64GB of memory i.e., we can have only 64GB of data. Now if we have 10 clustered computers with each 64GB of RAM then we can store 640GB of data.


![redis-cluster](../images/redis-cluster.jpg)


In the above image we can see that data is sharded into four nodes. Each node is a redis server configured as a cluster node.

If one node fails then the whole cluster stops working.


## Persistance In Cluster
Data is stored in primary memory of nodes. We need to make the data of each node persistance. We can do that using the previously mentioned methods(AOF and RDF). Just configure every node for persistance storage.

## Clustering And Replication Together
Suppose due to disk crash, one of our node goes down then the whole cluster stops working and never resumes. There is no way we can recover back the node as the data is completely lost.

To avoid this situation we can take a manual backup of each node regularly. But thats a tough and improper task. Therefore we can rely on replication to solve this problem.

![cluster-replication-redis](../images/cluster-replication-redis.jpg)

Here we convert each node server to a master server. And we keep a slave for every master. So if any node(master) fails, the cluster will start using the slave to keep the cluster operating.

## Redis Client
Client program like  (jedis for java) to connect to redis server and retrieve data.

## Redis commands

###Redis datastructures
```
string , list , hash , set and sorted set
```
####String
######Set value
```
set <key name> <value>
set name "hiren"
```
######Get value
```
get <key name>
get name #return "hiren"
```
######Get value using range
```
getrange <key> <range>
getrange name 0 3 #return "hire"
```
######Set value using range
```
setrange <key> <position> <value> 
setrange name 5 RST
```
######Override value
```
getset <key> <new value>
getset name "Rater Santo Tara"
```
######Multiset value
```
mset <key> <value> <key> <value>
mset name "Rater Santo Tara" age 20
```
######Increment value (only works for numbers)
```
incr age ## increment age by 1
```
######Decrement value
```
decr <key>
```
######Increment and decrement by specific number
```
incrby <key> 5
decrby <key> 20
```
######Float increment (only for integer )
```
incrbyfloat <key> <float value> 
```
######Set expire time
```
setex <key> <time in second> <value>
setex name 4 hiren
```
######Only set value if doesnt exits
```
setnx <key> <value>
```
######Multi setnx
```
msetnx <key> <value> <key> <value>
```
######Length of a value
```
strlen <key>
```

#### List
###### Lpush ( Left push )
```
lpush <list name or key >  <value> <value>
```
###### Rpush ( Right push )
```
rpush <key or list name > <value> <value>
```
###### Lpushx and Rpushx (push if the list is exits)
```
lpushx <list name or the key > <value>
rpushx <list name or the key > <value>
```
###### Length of a list
```
llen <list name >
llen hiren
```
###### Get values
```
lrange <list name> <starting position> <ending position>
```
Tips : For grabbing whole list use starting position = 0 and ending position = -1 

###### Pop from left or right side
```
lpop <value>
rpop <value>
```
###### Remove value
```
lrem <list name> 2 <value>
```
###### Insert middle 
```
linsert <list name> before <existing value> <new value>
linsert <list name> after <existing value> <new value>
```
###### Get value using index
```
lindex <list name> <index no>
```
###### Set value using index
```
lset <list name> <index number> <new value>
```
###### Trim
```
ltrim <list name> <starting position> <ending position>
```
#####List sorting
######Basic Sorting
```
sort <list key>
```
###### Sort with limit
```
sort <list key> limit <starting point> <ending point>
```
###### Sort descending or ascending 
```
sort <list key> asc
sort <list key> desc
```
###### Sort characters
```
sort <list key name> alpha
```

####Hash
###### Set command
```
hset <key> <subkey> <value>
hset hiren age 20
```
###### Get command
```
hget <key> <subkey>
```
###### Get all value
```
hgetall <key>
```
###### Return only keys or values
```
hvals <key>
hkeys <key>
```
###### Check value existence 
```
hexits <key> <subkey>
```
###### Increment
```
hincrby <key> <subkey>
hincrbyfloat <key> <subkey>
```
###### Check length
```
hlen <key>
```
###### Multiple get
```
hmget <key> <subkey> <subkey>
```
###### Multipke set
```
hmset <key> <subkey> <value> <subkey> <value>
```
###### Set if doesnt exits
```
hsetnx <key> <subkey> <value>
```
###### Delete
```
hdel <key> <subkey>
```
#### Set
###### Add single or multiple value
```
sadd <set name> <value> <value>
```
###### Remove value
```
srem <set name> <value>
```
###### Show all members
```
smembers <set name>
```
###### CHeck if already exists or not
```
sismember <setname> <value>
```
##### Check how many item in set
```
scard <set name>
```
###### Take random item from set
```
sranmember <set name>
```
###### Take random member out of the set
```
spop <set name>
```
###### Check member defference in two set
```
sdiff <set name> <set name>
```
###### Check difference and store in new set
```
sdiff <new set name>  <set name> <set name>
```
##### Intersection(common members) in both set
```
sinter <set 1> <set 2>
```
###### Union between sets
```
sunion <set 1> <set 2>
```
###### Store union result
```
sunionstore  <new set >  <set 1> <set 2>
```
######Move value from 1 set to another
```
smove <old set> <new set> <value>
```

## Other Commands

######  Search all keys
```
keys *
```
###### Search using specific pattern
```
keys hiren*
keys hire
```
######Check if key exist
```
exits <key name>
```
###### Check type of a key
```
type <key name>
```
##### Delete key
```
del <key name>
```
###### Move to different database
```
move <key name>  <database number>
move hiren 2
```
###### Select database
```
select <database number>
select 1
```
###### Expire
```
expire <key name> <Second>
```
######Time to live
```
ttl <keyname> <secound>
```