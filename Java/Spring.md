# 粗粒度和细粒度问题
细粒度和粗粒度主要解决方法重用问题
将一个业务逻辑复杂的模块拆分成多个业务职责明确的模块，这就是粗粒度到细粒度的转换

# Spring IOC（DI）
## IOC主要作用：
	IOC 控制反转
	IOC是Spring的容器，主要功能就是管理对象的实现
	通过XML或者是properties配置文件配置实现对象的关系
## DI主要作用
	DI 依赖注入
	配合IOC动态的把对象注入到需要对象的程序中
	DI通过反射(CGLIB或者JDK)实现把对象动态注入到程序中
## AOP
面向切面编程，分层开发，把程序分成两部分 **核心关注点** 和 **横切关注点**

# Spring

简化开发，降低模块和模块之间的耦合
解决程序高耦合的问题

## 核心容器
	Spring core		
	SPring beans
## Spring 事物
	事物特性：ACID
	原子性：事物修改的数据要么成功(提交)，要么失败(回滚)
		事物正在操作的数据，其他事物要么看到的是提交前、前数据，要么是提交后数据
	一致性：事物应该在执行前和执行后都保证数据库约束的合法性
	隔离性：事物执行过程中，正在操作的数据不能被其他事物干扰
	持久性：事物一旦提交成功就永久的保存了磁盘上

### 两种注入类型

```
@Autowire

@Resource

@Quiti


```

# Spring 各个组件功能

核心组件：core 、bean 、context

## Spring-core 

spring引入其他组件时，都必须要引入spring-core,这是其他组件的基础

## Spring-beans









# 其他

## spring加载配置文件属性

保证xml中加载了*.properties

jdbc.properties:

```properties
jdbc.optjdbc.server=test opt attributes!
```



```xml

<context:property-placeholder location="classpath:jdbc.properties,classpath:httpclient.properties,classpath:taobao.properties,classpath:redis.properties"/>

```

在spring维护的程序中，直接声明属性：

```java
@Value("${jdbc.optjdbc.server}")
private String optjdbcServer;
```














​	