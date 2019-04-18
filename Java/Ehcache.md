# Eacache

以键值对形式存储。





## ehcache和redis比较

ehcache 直接在jvm虚拟机中缓存(直接缓存到内存中)，速度快，效率高。但是缓存共享麻烦，集群分布式不方便。

redis 通过socket 访问缓存，效率和ehcache比，速度慢，和数据库比，速度快。

## CacheManager 

默认管理cache 容器，控制cache生命周期

### 创建方法

```java

CacheManager cacheManager = CacheManager.create("src/main/resources/encache.xml");

```

CacheManager.create(

​	Configuration	配置文件对象 |

​	InputStream	文件流		 |

​	URL				网络文件	 |

​	String			文件路径	 |

);

encache 详细属性

https://www.cnblogs.com/crazylqy/p/4238148.html

## ehcache配置文件

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"         xsi:noNamespaceSchemaLocation="https://www.ehcache.org/ehcache.xsd">
    <!-- 磁盘缓存位置 -->
    <!-- java.io.tmpdir表示当前系统临时文件目录 -->
    <diskStore path="java.io.tmpdir/encahce" />
    <!-- 默认缓存 -->
    <defaultCache
            maxEntriesLocalHeap="10000"
            eternal="false"
            timeToIdleSeconds="120"
            timeToLiveSeconds="120"
            maxEntriesLocalDisk="10000000"
            diskExpiryThreadIntervalSeconds="120"
            memoryStoreEvictionPolicy="LRU">
    </defaultCache>
    <!-- 自定义缓存 -->
    <cache name="HelloWorldCache"
           maxElementsInMemory="1000"
           eternal="false"
           clearOnFlush="true"
           timeToIdleSeconds="3"
           timeToLiveSeconds="5"
           overflowToDisk="false"
           memoryStoreEvictionPolicy="LRU">
    </cache>
    
    
    
</ehcache>
    
```

name:自定义缓存名称

timeToLiveSeconds:表示在缓存中存活的最长时间

timeToIdleSeconds:表示距离上次访问后，最大空闲时间，空闲时间超过这个值会被销毁。



**defaultCache**:默认缓存

maxEntriesLocalHeap: 堆内存中最大缓存对象数,0没有限制

**[过时，被maxEntriesLocalHeap取代]** maxElementsInMemory:缓存最大个数

maxEntriesLocalDisk:硬盘最大缓存个数

eternal:缓存对象是否永久有效，设置true(永久有效)后timeToLiveSeconds/timeToIdleSeconds属性不在生效

diskExpiryThreadIntervalSeconds 设置检测Element失效检测和清理线程清理间隔时间。





ps:0 表示无限时间



## Ehcache整合Spring

主要使用两个注解：

@Cacheable和@CacheEvict

@Cacheable**(value,key,condition)**

​	标记的方法，在方法执行后，自动缓存方法返回的结果。

​	每次调用方法时，都会先去缓存中查找指定key是否有值(方法注解中设置key)，如果有，不调用方法，直接返回。没有，调用方法，存储到缓存，返回。

@CachePut **(value,key,condition)**

​	和@Cacheable类似，标注@CachePut 的方法，在执行前不会检查指定key是否有缓存。会直接调用方法，把方法返回结果缓存到指定key。

@CacheEvict**(value,key,condition,allEntries,beforeInvocation)**

​	方法/类 标注@CacheEvict后，在调用方法前都会清除缓存。可通过condition参数设置清除缓存条件。

value[必须]:

表示当前方法返回值会被返回到那个cache上

key:

缓存的key,当没有设置key时，使用默认策略生成key,表示使用方法的参数和类型作为key

