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

https://www.cnblogs.com/fashflying/p/6908028.html

主要使用两个注解：

@Cacheable和@CacheEvict

@Cacheable**(value,key,condition)**

​	标记的方法，在方法执行后，自动缓存方法返回的结果。

​	每次调用方法时，都会先去缓存中查找指定key是否有值(方法注解中设置key)，如果有，不调用方法，直接返回。没有，调用方法，存储到缓存，返回。

@CachePut **(value,key,condition)**

​	和@Cacheable类似，标注@CachePut 的方法，在执行前不会检查指定key是否有缓存。会直接调用方法，把方法返回结果缓存到指定key。

@CacheEvict**(value,key,condition,allEntries,beforeInvocation)**

​	方法/类 标注@CacheEvict后，在调用方法前都会清除缓存。可通过condition参数设置清除缓存条件。

### value[必须]:

表示当前方法返回值会被返回到那个cache上

### key:

缓存的key,当没有设置key时，使用默认策略生成key,表示使用方法的参数和类型作为key

#### 使用方法参数指定Key

#参数名

​	#user : user 参数对象值作为key，

​		假设user有id和name属性，也可以通过user.id/user.name作为缓存的key.

#pindex

​	#p0 : 方法第一个参数作为key。

[待确定] 如果key指向的是一个对象，则用对象**内存地址**作为key



#### 使用Spring指定Key

Spring 提供了#root对象，通过这个对象，可以获取到当前方法一系列属性当缓存的key：

| 属性名称 | 描述 | 示例 |
| -------- | ---- | ---- |
| methodName  | 当前方法名                  | #root.methodName     |
| method      | 当前方法                    | #root.method.name    |
| target      | 当前被调用的对象            | #root.target         |
| targetClass | 当前被调用的对象的class     | #root.targetClass    |
| args        | 当前方法参数组成的数组      | #root.args[0]        |
| caches      | 当前被调用的方法使用的Cache | #root.caches[0].name |

默认可以直接写属性名，不用添加#root

### condition

通过传入对象的数据，限制那些需要缓存，那些不需要缓存。



pom，测试通过:

```xml
	<properties>
        <spring.version>3.1.1.RELEASE</spring.version>
        <junit.version>4.10</junit.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>net.sf.ehcache</groupId>
            <artifactId>ehcache-core</artifactId>
            <version>2.5.0</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context-support</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>${spring.version}</version>
        </dependency>


        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>${junit.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>${spring.version}</version>
            <scope>test</scope>
        </dependency>

    </dependencies>
```

# 错误整理

Ehcache 报错:

```
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'exInterfaceController': Injection of autowired dependencies failed; nested exception is org.springframework.beans.factory.BeanCreationException: Could not autowire field: org.springframework.cache.CacheManager com.hangar.cms.action.BaseController.cacheManager; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'cacheManager' defined in file [/opt/JavaWork/518CMS/518CMS/out/artifacts/518CMS_war_exploded/WEB-INF/classes/com/hangar/cms/config/springHibernate.xml]: Cannot resolve reference to bean 'ehcacheManager' while setting bean property 'cacheManager'; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'ehcacheManager' defined in file [/opt/JavaWork/518CMS/518CMS/out/artifacts/518CMS_war_exploded/WEB-INF/classes/com/hangar/cms/config/springHibernate.xml]: Invocation of init method failed; nested exception is net.sf.ehcache.CacheException: Another CacheManager with same name 'sysCache1' already exists in the same VM. Please provide unique names for each CacheManager in the config or do one of following:
1. Use one of the CacheManager.create() static factory methods to reuse same CacheManager with same name or create one if necessary
2. Shutdown the earlier cacheManager before creating new one with same name.



```

主要报错:

```
1. Use one of the CacheManager.create() static factory methods to reuse same CacheManager with same name or create one if necessary
2. Shutdown the earlier cacheManager before creating new one with same name.

```

是hibernate 和ehcache 整合出错,:

```xml
	 <bean id="ehcacheManager" class="org.springframework.cache.ehcache.EhCacheManagerFactoryBean">  
	    <property name="configLocation" value="classpath:ehcache.xml"/>
         <property name="shared" value="true" />
	</bean> 
```

主要添加:

```xml
<property name="shared" value="true" />
```

后正常运行.