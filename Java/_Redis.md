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

#### 添加

```
zadd <key> <score> <value>
```

score : 排序字段

key : 键

value ： 值

#### 列出列表

```
zrange <key> <startindex> <endindex> WITHSCORES
```

startindex : 从第startindex个项开始

endindex ：到第endindex个项结束



```shell

zadd key1 0 value1
zadd key1 1 value2
zadd key1 4 value4
zadd key1 3 value1

```

## 发布订阅

### 创建：

```shell
# SUBSCRIBE <subscribeName>
SUBSCRIBE sub1
# 创建口会阻塞客户端，重新开启一个redis-cli
```

### 发布订阅:

```shell
# PUBLISH <subscribeName> value
publish sub1 "hello ~"
# 对应订阅者会受到"hello ~"信息


```

## 事务

redis事务执行分成三步：

1. 开启事务

2. 命令入列

3. 执行事务



事务不会再其中一条命令失败后回滚，也不会因为其中一条命令失败影响后续命令知行。

#### 开启事务：

```
MULTI
```

至此，输入的命令都会加入到事务中，

直到输入exec命令，把输入的所有命令依次执行。

#### 命令入列：

```
set name "zhangsan"
>QUEUED
set name "wangwu"
>QUEUED
get name
>QUEUED
```

#### 执行事务：

```
exec
1) OK
2) OK
3) "wangwu"
```

#### 放弃事务：

DISCARD

在执行MULTI后，命令都会加入到执行队列，

如遇到exec,执行队列中命令

遇到discard,取消当前事务



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

# Redis配置

参考：https://www.cnblogs.com/kreo/p/4423362.html

## redis.conf配置

配置文件中引入其他conf配置：

```properties
include /xx/*.conf
include /xx/*.conf
include /xx/*.conf
```

## 保存配置

save <间隔时间(秒)> <写入次数>

```properties
 # 每 900 秒检测到key变动 3 次保存
 save 900 3
 # 没 100 秒检测到key变动 10 次保存
 save 300 10 
```



# RedisTemplate

spring 基于 Jedis封装的操作Redis工具

## 导入pom:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

## 配置配置文件:

```yml
spring:
  redis:
    database: 0	# 默认数据库
    host: 37.29.43.35 
    port: 6379 
    password: 123456 
    
    lettuce: # 连接池相关配置
      pool:
        max-active: 8
        min-idle: 0
        max-idle: 8
        max-wait: -1
    timeout: 30000
```

## 坑:

RedisTemplate 和 StringRedisTemplate 是有区别的，数据不通用！！

有两种序列化方式：String的序列化;  JDK序列化策略

StringRedisTemplate 用的是String的序列化

RedisTemplate  用的是JDK序列化策略

### 手动配置RedisTemplate序列化方式

StringRedisTemplate 存储的数据RedisTemplate默认是读不到的，如果RedisTemplate想读到StringRedisTemplate 存储的数据，需手动配置RedisTemplate成String的序列化方式。

```java
RedisSerializer<String> stringRedisSerializer = new StringRedisSerializer();
redisTemplate.setKeySerializer(stringRedisSerializer);
redisTemplate.setValueSerializer(stringRedisSerializer);
```

































