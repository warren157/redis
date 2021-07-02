# Redis

## Key

> Rediskey是二进制安全的，意味着你可以使用任意的二进制序列作为一个key

### key的规则

+ 非常长的key是不建议的，如果key超过1024字节不是一个好的主意，而且在数据集中查找对内存和带宽的消耗是非常昂贵的

+ 非常短的key也不是一个好的建议，需要设置有意义的key

+ 通常我们设置key的名字为："object-type:id"  例如：user:1000

+ key的最大长度为512MB

  

### key操作

 #### exists

>判断key是否存在，存在返回1 不存在返回0

![image-20210701111213306](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701111213306.png)

#### del 

> 删除指定key 

![image-20210701111322350](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701111322350.png)

#### type 

> 获取key的类型

![image-20210701111422107](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701111422107.png)

#### expire

> 指定key的过期时间

![image-20210701111630414](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701111630414.png)

#### ttl

> 查看key还有多久过期

![image-20210701111843188](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701111843188.png)

## Redis Strings

> redis string 类型是可以与rediskey关联的最简单的数据类型。
>
> 它是Memcached中唯一的数据类型，使用起来简单。
>
> 可以用来缓存html页面。

### set

```set 
set key value
注意：set 会覆盖已存在的key的值
```

![image-20210701103808635](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701103808635.png)

```set
set key value nx
存在不插入
```

![image-20210701105110803](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701105110803.png)

```set
set key value xx
存在覆盖，等同set key value
```

![image-20210701105333823](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701105333823.png)

``` set
set key value ex | px time
设置key 的过期时间 等同与
set key vlaue
expire key time
ex:按秒
px:按毫秒
```

![image-20210701112626195](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701112626195.png)





### mset

> 批量添加key和值

``` set
mset key1 val1 key2 val2
```

![image-20210701112336708](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701112336708.png)

### get

> 语法：get keyName

``` get
get redis
```

![image-20210701103922325](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701103922325.png)

### mget

> 批量获取多个key的值

![image-20210701112336708](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701112336708.png)

### incr

> 描述：该命令是如果key的值是integer类型，该值就自增1
>
> 与其相似的命令有 incrby,decr,decrby

``` set
set key value
incr key
```

![image-20210701110340506](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701110340506.png)

### incrby

```set
incryby key increment
指定增加的数量
```

![image-20210701110505907](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701110505907.png)

### decr 

``` set
decr key 
每次递减1
```

![image-20210701110730013](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701110730013.png)

### decrby

```
decrby key decrement
按照指定值递减
```

![image-20210701111027203](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701111027203.png)

## Redis List

> redis list是通过链表实现的
>
> 链表意味着即使list中有很多数据，但是在头或者尾插入新的元素很快。
>
> Redis列表是用链表实现的，因为对于数据库系统来说，能够以非常快的方式将元素添加到非常长的列表中是至关重要的。另一个强大的优势，是Redis列表可以在固定的时间内以固定的长度获取。
>
> 当快速访问大量元素集合的中间非常重要时，可以使用不同的数据结构，称为排序集。排序集将在本教程后面介绍

### rpush

>向链表的尾部插入新的元素

``` set
rpush key value ...
```

![image-20210701113739810](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701113739810.png)

### lpush 

> 向链表的头插入新元素

``` set
lpush key value ...
```

![image-20210701130253264](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701130253264.png)

### lrange

> 从链表中获取元素的范围。
>
> **注意**：lrange有两个索引，第一个到最后一个元素的范围，两个索引都能为负数，表示倒数第几个开始

``` set
lrange key start end 
```

![image-20210701130734549](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701130734549.png)

### lpop

> Redis列表上定义的一个重要操作是弹出元素的能力。弹出元素是同时从列表中检索元素和从列表中删除元素的操作。可以从左侧和右侧弹出元素
>
> **操作**：lpop左侧弹出元素，rpop 右侧弹出元素

``` set
lpop key 
```

![image-20210701131543377](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701131543377.png)

### rpop

> 右侧弹出元素

``` set
rpop key
```



![image-20210701131631133](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701131631133.png)

### ltrim

> 和lrange相似，但是ltrim没有显示指定的元素范围，而是将此范围设置为新的list，所有超出给定范围的元素都将被删除

``` set
ltrim key start end 
```

![image-20210701132641550](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701132641550.png)

### 阻塞队列

> **List有一些特殊的特性，它适用于队列的实现，和进程间的阻塞通信：阻塞操作**
>
> 生产者/消费者模式：一个进程LPUSH，一个进程RPOP
>
> 然而，有些时候这个list是空的，因此RPOP只会返回NULL，在生产者消费者模式中消费者将被迫等待一段时间，然后使用RPOP重试。这称为轮询，在这种情况下不是一个好主意，因为它有几个缺点：
>
> * 强制redis和客户端处理无用的命令，因为list是空的，所有的请求都只会返回NULL
> * 将延迟添加到项的处理中，因为在worker接收到NULL之后，它会等待一段时间。为了减少延迟，我们可以减少RPOP调用之间的等待时间，其效果是放大问题1，即更多无用的Redis调用
>
> 因此，redis实现了BRPOP和BLPOP命令，如果list是空的，就会阻塞一段时间

```set
blpop key timeout
timeout单位是秒
```

![image-20210701135344288](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701135344288.png)

> **_注意_**  : 
>
> 1.BROPO和BLPOP是按照客户端被服务的顺序来的第一个客户端被阻塞等待list，当list被push数据的时候，首先被服务
>
> 2.返回值与RPOP不同，BRPOP有两个元素的数组，包含key的名字
>
> 3.如果超时时间到了，会将null返回

### 总结

> key的自动创建和删除，下面是总结的三种规则
>
> * 当我们增加一个元素到指定的数据类型时，如果key不存在，那么就会在添加元素前先创建一个空的数据类型
> * 当我们从聚合数据类型中删除元素时，如果值仍然为空，则键将自动销毁。流数据类型是此规则的唯一例外
> * 使用空键调用只读命令，如LLEN（返回列表的长度）或删除元素的write命令，总是会产生相同的结果，就好像该键包含该命令期望找到的类型的空聚合类型一样

## Redis Hash

> redis hash和普通的hash一样，具有key - value
>
> Redis 中每个 hash 可以存储 232 - 1 键值对（40多亿）。

### hset

> 设置单个字段的值,一般用于修改操作

``` set
hset key field value
```

![image-20210701154427238](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701154427238.png)

###  hmset 

``` set
hmset key  field1 value1 field2 value2
```

![image-20210701152539803](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701152539803.png)

### hget

> 返回单个的字段

``` set
hget key field
```

![image-20210701153025541](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701153025541.png)

### hmget

> 获取多个字段值

``` set
hmget key field1 field2
```

![image-20210701153224923](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701153224923.png)

### hsetnx 

> 当field不存在时，设置hash字段的值

``` set
hsetnx key field value
```

![image-20210701160214516](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701160214516.png)

### hgetall

> 获取key中的所有字段值

``` set
hgetall key
```

![image-20210701153521297](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701153521297.png)

### hincrby

> 对单个字段进行增加操作,只能对数字类型的字段进行操作

``` set
hincrby key field increment
```

**错误示例 **:

![image-20210701154048885](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701154048885.png)

**正确示例** :

![image-20210701154137703](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701154137703.png)

### hdel

> 删除一个或多个字段,用于删除对象属性

``` set
hdel key field1 [field2]
```

![image-20210701154713901](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701154713901.png)

### hexists 

> 判断对象中是否存在某个属性
>
> 存在返回1，不存在返回0

```set
hexists key field
判断key中是否存在field
```

![image-20210701155413932](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701155413932.png)

### hkeys

> 获取所有hash表中的字段

``` set
hkeys key
```

![image-20210701155803959](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701155803959.png)

### hvals

> 获取hash表所有的值

``` set
hvals key
```

![image-20210701160303740](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701160303740.png)

## Redis Set

> Redis Sets是无序的,不可重复的字符串的集合

### sadd 

> 向集合中添加元素

``` set
sadd key value1 value2 ...
```

![image-20210701161844431](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701161844431.png)

### smembers

> 获取集合中所有元素

``` set
smembers key
```

![image-20210701162717864](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701162717864.png)

### sismember

> 判断元素是否存在 ，存在返回1，不存在返回0

``` set
sismember key value
```

![image-20210701162811087](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701162811087.png)

### smismember

> **注：**该命令在**6.2.0.**版本有效
>
> 批量判断元素是否存在集合中，存在返回1，不存在返回0
>
> 返回结果的顺序和请求的参数顺序一致

``` set
smismember key member [member]
```

![image-20210702085315072](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702085315072.png)

### sinter

>求出各个集合中的并集

``` set
sinter set1 set2 set3 ...
```

![image-20210701164121300](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210701164121300.png)

### sinterstore

> 和sinter命令一样，但是这个命令会将返回值存到目标集合中

``` set
sinterstore destination key [key]
```

![image-20210702084655954](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702084655954.png)

### scard

> 返回集合中的元素的个数

``` set
scard key
```

![image-20210702082728772](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702082728772.png)

### sdiff

> 返回由第一个集合和所有连续集合之间的差异产生的集合成员
>
> **_注意_**  : 如果key不存在的时候，就返回一个空集合

``` se
sdiff key1 key2 ...
```

![image-20210702083339229](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702083339229.png)

### sdiffstore

> 和sdiff命令一样，但是这个命令会将结果集存储到目标集合中

``` set
sdiffstore destination_key key1 key2 ...
```

![image-20210702084113103](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702084113103.png)

### smove

> + 移动元素 从**源**集合到**目标**集合，并将**源**集合中的元素删除。
>
> + 如果元素不存在源集合中，或者源集合不存在，不做任何操作并返回0。
>
> + 如果移动的元素在目标集合中存在，仅仅会移除源集合中的元素。
> + 如果源和目标不是集合结构，就返回错误

``` set
smove source destination member
```

![image-20210702090153265](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702090153265.png)

### spop 

> + 移除并返回一个或多个随机数量的元素
> + 这个操作和srandmember相似，但是它不会移除元素
> + 默认的这个命令弹出单个元素

``` set
spop key [count]  count可选
```

![image-20210702090737424](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702090737424.png)

### srandmember 

``` set
srandmember key [count]
```

> + 当count不传时，从key的集合中随机返回一个元素
> + 当count为正数时，从集合中随机返回count数的元素，不会重复返回元素
> + 当count为负数时，允许重复返回元素

![image-20210702091359783](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702091359783.png)

### srem

``` set
srem key member [member]
```

> + 删除集合中的指定的元素
> + 指定的元素如果集合中不存在就会被忽略
> + 如果key不存在，返回0
> + 如果key不是集合结构，返回错误

![image-20210702092150191](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702092150191.png)

## Redis Sorted Set

### zadd

``` set
zadd key [nx|xx] [gt|lt] [ch] [incr] score member [score member] ...
```

> + 添加元素并指定此元素的分数
> + 如果指定的元素存在分数，则这个分数会被更新，并将元素插入到正确位置，确保排序正确
> + 如果key不存在，则一个新的排序集合被创建
> + 如果key存在，但不是排序集合结构，则返回错误
> + 分数值应该是双精度浮点数的字符串表示形式+inf和-inf值也是有效值。

> **_参数说明_**
>
> **XX** : 仅仅更新存在的元素，不新增新的元素
>
> **NX** : 仅仅新增新元素，不更新已存在的元素
>
> **LT**  ：新增新元素，但是如果元素存在，新的分数小于当前元素的分数则更新
>
> **GT** ：新增新元素，但是如果元素存在，新的分数大于当前元素的分数则更新
>
> **CH** ：修改返回值为发生变化的成员总数，原始是返回新添加成员的总数 (CH 是 *changed* 的意思)。更改的元素是**新添加的成员**，已经存在的成员**更新分数**。 所以在命令中指定的成员有相同的分数将不被计算在内。注：在通常情况下，`ZADD`返回值只计算新添加成员的数量
>
> **INCR** : 对元素的分数进行递增操作

![image-20210702100655779](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702100655779.png)

![image-20210702100726525](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702100726525.png)

### zcard

```set
zcard key
```

> 返回有序集合的成员个数

![image-20210702101043844](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702101043844.png)

### zcount

``` set
zcount key min max
```

> + 统计key的元素的分数在min到max之间的元素个数

![image-20210702101456227](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702101456227.png)

### zdiff 

``` set
zdiff numkeys key [key ...] [withscores]
```

> 这个命令和[ZDIFFSTORE](https://redis.io/commands/zdiffstore) 相似，但是zdiffsotre会存储结果集
>
> **_注意_**  ： 该命令在**6.2.0**支持

![image-20210702104423842](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702104423842.png)

### zdiffstore

``` set
zdiffstore destination numKeys key [key ...]
```

> + 计算第一个和所有连续输入排序集之间的差值，并将结果存储在目标中。输入键的总数由numkeys指定
> + 如果destination存在将会被覆盖

### zincrby

``` set
zincrby key increment member
```

> + member按照increment的值增加
> + 如果member不存在，会新增一个member并且score等于increment
> + 如果key不存在，会为指定的member创建一个新的set
> + 如果key存在但是key不是sorted set结构，则会报错
> + increment可以是负数，双精度浮点数

![image-20210702111131710](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702111131710.png)

### zinter

``` set
zinter numKeys key [key ...] [WEIGHTS weight [weight ...]] AGGREGATE SUM|MIN|MAX] [WITHSCORES]
```

> **_注意_**  ： 适用于**6.2.0.**以上版本
>
> WEIGHTS：给指定的key的成员的分数乘以该权重的值
>
> AGGREGATE：聚合操作， 默认是sum 

![image-20210702125845028](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702125845028.png)

### zinterstore

``` set
zinterstore destination numkeys key [key ...] [WEIGHT weight [weight ...]] [AGGREGATE SUM|MIN|MAX]
```

> + 计算指定key的交集并将结果存储到destination中

![image-20210702130822491](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702130822491.png)

### zlexcount

``` set
zlexcount key min max
```

> 返回key中成员分数在 min 到max之间的个数

![image-20210702131323963](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702131323963.png)

### zmscore

``` set
zmscore key member [member ...]
```

> + 返回指定成员的分数
> + 如果成员不存在就返回nil
> + 该命令在**6.2.0**版本以上可用

![image-20210702131737594](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702131737594.png)

### zpopmax

``` set
zpopmax key [count]
```

> + 删除和返回分数最高的成员和成员的分数
> + count没有指定默认是1
> + count大于1时，成员按照分数倒序排序

![image-20210702132258978](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702132258978.png)

### zpopmin

``` set
zpopmin key [count]
```

> + 删除和返回分数最低的成员和成员的分数
> + count没有指定默认是1
> + count大于1时，成员按照分数正序排序

### zrandmember

``` set
zrandmember  key  [count [WITHSCORES]]
```

> + 当只有key参数时，随机返回一个成员
> + 如果count>0 返回的是不同的元素，长度等于count
> + 如果count>0 且大于集合长度，则该命令将只返回整个排序集，而不返回其他元素
> + 如果count<0 允许多次返回相同的成员

![image-20210702133209570](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702133209570.png)

###  zrange

``` set
zrange key min max [BYSCORE|BYLEX] [REV] [LIMIT offset count][WITHSCORES]
```

> + 该命令在 **6.2.0** 及以上版本可以替代[ZREVRANGE](https://redis.io/commands/zrevrange), [ZRANGEBYSCORE](https://redis.io/commands/zrangebyscore), [ZREVRANGEBYSCORE](https://redis.io/commands/zrevrangebyscore), [ZRANGEBYLEX](https://redis.io/commands/zrangebylex) and [ZREVRANGEBYLEX](https://redis.io/commands/zrevrangebylex).命令
> + 返回指定范围的成员集合

![image-20210702134209698](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702134209698.png)

### zrangebylex

``` set
zrangebylex key min max [LIMIT offset count]
```

> + 当所有的成员的分数相同，则根据字典排序
> + 返回分数在min和max之间的成员
> + 指定间隔
>   + 有效的开始和结束必须以 `(` or `[` 表示不包含或者包含
>   + 如果指定 `+`or `-`表示正无穷和负无穷

![image-20210702135152913](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702135152913.png)

### zrangebyscore 

```s et
zrangebyscore key min max [WITHSOCRES] [LIMIT offset count]
```

> + 返回成员分数在min和max之间的所有成员
> + 返回的顺序是分数从低到高
> + 区间设置
>   + min和max可以用 -inf和+inf表示从负无穷到正无穷
>   + 可以用 `(` 表示不包含

![image-20210702140217188](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702140217188.png)

### zrangestore

``` set
zrangestore dst src min max [BYSCORE|BYLEX] [REV] [LIMIT offset count]
```

> + 和zrange一样，但是取出来的成员会存储到 `dst` 中
> + 该命令在`6.2.0`以上版本使用

![image-20210702140429512](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702140429512.png)

### zrank 

``` set
zrank key member
```

> + 返回成员在key中的索引，分数是从小到大排序
> + rank是从0开始
> + 使用[ZREVRANK](https://redis.io/commands/zrevrank)获得从大到小排序的索引

![image-20210702141133704](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702141133704.png)

### zrem

``` set
zrem key member [member ...]
```

> + 删除key中指定的成员，如果成员不存在就忽略
> + 如果key不是一个排序集合则返回错误

![image-20210702141341503](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702141341503.png)

### zremrangebylex 

``` set
zremrangebylex key min max
```

> + 删除存储在由min和max指定的字典范围之间的键处的排序集中的所有元素

![image-20210702141825860](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702141825860.png)

### zremrangebyrank

``` set
zremrangebyrank key start stop
```

> + 根据索引删除，从0开始

![image-20210702142240340](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702142240340.png)

### zremrangebyscore

``` set
zremrangebyscore key min max
```

> + 删除分数在min到max之间的成员 

![image-20210702142538568](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702142538568.png)

### zrevrange

``` st
zrevrange key start stop [WITHSCORES]
```

> + 返回指定范围的成员倒序返回
> + `6.2.0`这个命令废弃，用zrange代替，里面的REV参数

![image-20210702142948415](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702142948415.png)

### zrevrangebylex

``` set
zrevrangebylex  key max min [LIMIT offset count]
```

> + 根据字典倒序排序，并返回指定大小范围的成员
> + LIMIT相当于分页，可用于获取TOP10等需求
> + 这个命令通常是用于分数一样的成员

![image-20210702143533036](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702143533036.png)

### zrevrangebyscore 

``` set
zrevrangebyscore key max min [WITHSCORES] [LIMIT offset count]
```

> + 根据分数倒序排序，并返回指定大小范围的成员
> + LIMIT相当于分页，可用于获取TOP10等需求

![image-20210702143734161](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702143734161.png)

### zrevrank

``` set
zrevrank key member
```

> + 获取member在key中从后往前排第几，默认从0开始

![image-20210702144111199](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702144111199.png)

### zscan 

``` set
zscan key cursor [MATCH pattern] [COUNT count]
```

> + 用于迭代有序集合中的元素（包括元素成员和元素分值）
> + curosr:游标
> + pattern:匹配模式
> + count:指定从数据集里返回多少个元素，默认值为10

![image-20210702144623990](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702144623990.png)

### zscore

``` set
zscore key member
```

> + 返回成员的分数

![image-20210702144750806](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702144750806.png)

### zunion

``` set
zunion numKeys key [key ...] [WEIGHTS weight [weight]] [AGGREGATE SUM|MIN|MAX] [WITHSCORES]
```

> + 和zunionstore命令相似，但是这个命令只结果不存储结果
> + 该命令在`6.2.0` 版本以上可以使用

![image-20210702145055297](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702145055297.png)

### zunionstore

``` set
zunionstore dst numkeys key [key ...] [WEIGHTS weight [weight]] [AGGREGATE SUM|MIN|MAX]
```

> + 求并集并存储到`dst`目标集合中
> + WEIGHT：使用“权重”选项，可以为每个输入排序集指定乘法因子。这意味着在传递给聚合函数之前，每个输入排序集中每个元素的得分都要乘以这个因子。如果未给定权重，则乘法因子默认为1
> + AGGREGATE：使用AGGREGATE选项，可以指定如何聚合联合的结果。此选项默认为SUM，其中元素的分数在其存在的输入之间求和。当此选项设置为“最小”或“最大”时，结果集将包含元素在存在的输入之间的最小或最大得分
> + 如果`dst`存在则被覆盖

![image-20210702145600390](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20210702145600390.png)