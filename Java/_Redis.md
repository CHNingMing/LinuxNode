# Redis

Redis是一个**非关系型内存数据库**,**读取速度快**,**支持丰富的数据类型**,**支持事物**,可以设置**数据过期时间**

是单线程,但是不用担心线程安全问题

### Redis 数据类型

```
String、Hash、List(列表)、set(集合)、zset(有序集合)
```

| 类型                 | 简介                                                   | 特性                                                         | 场景                                                         |
| -------------------- | ------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| String(字符串)       | 二进制安全                                             | 可以包含任何数据,比如jpg图片或者序列化的对象,一个键最大能存储512M | ---                                                          |
| Hash(字典)           | 键值对集合,即编程语言中的Map类型                       | 适合存储对象,并且可以像数据库中update一个属性一样只修改某一项属性值(Memcached中需要取出整个字符串反序列化成对象修改完再序列化存回去) | 存储、读取、修改用户属性                                     |
| List(列表)           | 链表(双向链表)                                         | 增删快,提供了操作某一段元素的API                             | 1,最新消息排行等功能(比如朋友圈的时间线) 2,消息队列          |
| Set(集合)            | 哈希表实现,元素不重复                                  | 1、添加、删除,查找的复杂度都是O(1) 2、为集合提供了求交集、并集、差集等操作 | 1、共同好友 2、利用唯一性,统计访问网站的所有独立ip 3、好友推荐时,根据tag求交集,大于某个阈值就可以推荐 |
| Sorted Set(有序集合) | 将Set中的元素增加一个权重参数score,元素按score有序排列 | 数据插入集合时,已经进行天然排序                              | 1、排行榜 2、带权重的消息队列                                |

### Redis自动备份策略,可以设置备份时间

	配置文件中可以配置

# Redis-server

启动Redis：

```
redis-server
```

指定配置文件启动redis：

```
redis-server [配置文件路径]
```





# Redis-Cli

### 连接Redis

```shell
redis-cli -h 127.0.0.1 -p 6379
```





## 操作数据

### 添加数据

#### set key value [...]

```
set myHello HelloRedis
```

### 删除数据

DEL key [...]

```
del myHello
```

### Hash 哈希

HMSET key **field...**

```
HMSET myhash field1 "field1_value" field2 "field2_value"
```

HGET key **field**

````
HGET myhash field1
````

### List(列表)

#### 创建一个列表：

lpush key value

```
lpush test_list redis
lpush test_list mongodb
lpush test_list rabitmq
```

#### 列出列表：

lrange key startIndex endIndex

```
lrange test_list 0 5
```

### Set(集合)

列表内容不能重复

#### 添加项:

sadd key itemvalue

```
sadd test_set redis
sadd test_set mongodb
sadd test_set rabitmq
sadd test_set rabitmq
```

#### 列出列表：

smembers key

```
smembers key
```

### zset 有序集合

zadd key score member











## 查看配置

```
CONFIG GET *
```

\* 表示所有

可以：

```
CONFIG GET bind
> "bind"
> ""
```

