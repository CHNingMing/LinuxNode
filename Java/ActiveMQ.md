# ActiveMQ

标准JMS实现

主要是项目和项目之间通信,使用

### ActiveMQ作用

```
削峰，提高系统响应速度，解耦合
```

### 使用Dubbo缺点

```
减少项目和项目之间的耦合度
```

### 应用:

```
达到解耦和高并发等其他功能
提高程序速度
用于某个功能执行时间比较长，并且不关心任务返回值的情况下使用
```

### 访问端口:

浏览器端口 端口：8161 

java访问时端口:61616

```
TextMessage	字符串对象
MapMessage	键值对对象
ObjectMessage	可以序列化的Java对象
BytesMessage	一个字节的数据流
StreamMessage	Java原始值数据
```

#### 点对点	Queue

一个消息只被一个消费者消费

能持久化存储，一个消息肯定会被一个消费者消费

#### 广播	Topic

创建一个消息时，只有当前被监听的消费者才能接收到消息，创建消息后在创建的消费者不能接收消息。类似广播收音机

不能持久化存储，一个广播消息不一定被消费者消费

#### Message 对象

消息接收对象接口，获取接收对象

#### 管理面板	

Name 名称  

Number Of Pending Message **等待消费的消息**

Number Of Consumers **消费数量** 

Messages Enqueue 总共消息 **进出队列的数量**

Message Dequeued 出队列的消息 **被消费的消息**





## 5中消息格式:

```
http://haoran-10.iteye.com/blog/2259240

AMQP协议：

即Advanced Message Queuing Protocol,一个提供统一消息服务的应用层标准高级消息队列协议,是应用层协议的一个开放标准,为面向消息的中间件设计。基于此协议的客户端与消息中间件可传递消息，并不受客户端/中间件不同产品，不同开发语言等条件的限制。

MQTT协议：

MQTT（Message Queuing Telemetry Transport，消息队列遥测传输）是IBM开发的一个即时通讯协议，有可能成为物联网的重要组成部分。该协议支持所有平台，几乎可以把所有联网物品和外部连接起来，被用来当做传感器和致动器（比如通过Twitter让房屋联网）的通信协议。

OpenWire协议：OpenWire协议在网上没有对应的介绍，似乎是activeMQ自己定义的一种协议，官方网站对其的介绍如下：

OpenWire is our cross language Wire Protocol to allow native access to ActiveMQ from a number of different languages and platforms. The Java OpenWire transport is the default transport in ActiveMQ 4.x or later. For other languages see the following...

stomp协议：STOMP，Streaming Text Orientated Message Protocol，是流文本定向消息协议，是一种为MOM(Message Oriented Middleware，面向消息的中间件)设计的简单文本协议。

ws协议：即websocket协议，基于h5
```



消息格式:Queue(ActiveMQQueue)		Topic(ActiveMQTopic)

Queue:

	一个消息生产了,肯定会被消费,**并且是一个消费者消费**
	
	ActiveMQ服务器关闭时会把Queue序列化到磁盘上
	
	启动时还会读磁盘上的数据,加入队列中,直到他消费为止

Topic:

	产生消息后不一定会被消费,只有是监听的消费者才能接收消息

### 五种消息正文格式

StreamMessage -- Java原始值的数据流 

MapMessage--一套名称-值对

TextMessage--一个字符串对象（常用）

ObjectMessage--一个序列化的 Java对象

BytesMessage--一个字节的数据流

### JMS是面向消息中间件规范

生产者生产消息		消费者消费消息

### MQ对象

#### 连接缓存类

```
https://www.cnblogs.com/xingzc/p/5943165.html详细介绍

PooledConnectionFactory实现ConnectionFactory接口。为因JmsTemlate每次发送消息时都会重新创建连接，创建connection，session，创建productor。这是一个非常耗性能的地方，特别是大数据量的情况下。因此出现了PooledConnectionFactory。这个类只会缓存connection，session和productor，不会缓存consumer。因此只适合于生产者发送消息。那为什么不缓存consumer呢?官方解释是由于消费者一般是异步的，也就是说，broker代理会把生产者发送的消息放在一个消息者的预取缓存中。当消息者准备好的时候就会从这个预取缓存中取出来进行处理。我想，这个只是在要求消息处理的及时性不是特别高的情况下。如果希望处理能够提高速度，自然也可以从这部分提高效率，减小不断创建consumer的时间（大数据量的情况下）。

PooledConnectionFactory
CachingConnectionFactory
SingleConnectionFactory


```

### 步骤:

首先需要两个东西:生产者     消费者

#### 导入依赖:

```xml
    <dependencies>
        <!-- Spring相关 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-beans</artifactId>
            <version>4.1.7.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>4.1.7.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>4.1.7.RELEASE</version>
        </dependency>
        <!-- Spring整合MQ插件 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jms</artifactId>
            <version>4.1.7.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.apache.activemq</groupId>
            <artifactId>activemq-all</artifactId>
            <version>5.11.2</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
        <!-- Activemq引入了这个,用ActiveMQ必须导入 -->
        <dependency>
            <groupId>org.apache.xbean</groupId>
            <artifactId>xbean-spring</artifactId>
            <version>RELEASE</version>
        </dependency>
    </dependencies>
```

#### 生产者

首先配置生产者配置文件

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:amq="http://activemq.apache.org/schema/core"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
        http://activemq.apache.org/schema/core
   		http://activemq.apache.org/schema/core/activemq-core-5.7.0.xsd
    ">
    <!-- 生产者 -->
    <!-- amq简单标签链接对象 -->
    <!--
		brokerURL:MQ连接地址
	-->
    <amq:connectionFactory id="connectionFactory" brokerURL="tcp://localhost:61616"
                           userName="admin"   password="admin"></amq:connectionFactory>
    <!-- 真正的MQ链接对象 -->
<!--    <bean id="mqConnectionFactory" class="org.apache.activemq.ActiveMQConnectionFactory">
        <property name="brokerURL" value="" />
        <property name="userName" value="" />
        <property name="password" value="" />
    </bean>-->
    <!-- CachingConnectionFactory  -->
    <!--
        缓存MQ的
            produter    生产者
            session     会话
		适合生产者,提高消息发送速度
    -->
    <bean id="cachingConnectionFactory" class="org.springframework.jms.connection.CachingConnectionFactory">
        <!-- 
			targetConnectionFactory:目标连接工厂
			sessionCacheSize:会话数量,默认是 1 个
 		-->
        <property name="targetConnectionFactory" ref="connectionFactory" />
        <property name="sessionCacheSize" value="5" />
    </bean>
    <!-- MQ模板类 -->
    <bean id="jmsTemplate" class="org.springframework.jms.core.JmsTemplate">
        <!-- 连接工厂 -->
        <property name="connectionFactory" ref="cachingConnectionFactory"></property>
        <!-- 消息转换 -->
        <property name="messageConverter">
            <bean class="org.springframework.jms.support.converter.SimpleMessageConverter"></bean>
        </property>
    </bean>
    <!-- topic模式 广播模式 -->
    <!-- spring_topic:队列名称 -->
    <bean id="topic" class="org.apache.activemq.command.ActiveMQTopic">
        
        <constructor-arg name="name" value="spring_topic"></constructor-arg>
    </bean>
    <!-- queue模式 队列模式 -->
<!--    <bean id="queue" class="org.apache.activemq.command.ActiveMQQueue">
		<!-- 队列名称 -->
        <constructor-arg name="name" value="spring_queue"></constructor-arg>
    </bean>-->
</beans>
```

#### 发送消息

```java
Javax.jms.Destination

@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:生产者配置文件.xml")
public class Test3 {

    @Autowired
    //ActiveMQ模板类
    private JmsTemplate jmsTemplate;

    @Autowired
    //根据类型注入配置文件中配置好的 (队列/广播) Bean
    //队列和广播都实现Destination接口
    private Destination destination;

    @Test
    public void test1(){
        //destination:自动注入进来的对象
        jmsTemplate.send(destination, new MessageCreator() {
            @Override
            public Message createMessage(Session session) throws JMSException {
                //通过Session发送各种对象
                return session.createMapMessage();
                return session.createTextMessage();
                return session.createStreamMessage();
                return session.createObjectMessage();
                return session.createBytesMessage();
                //例子
                return session.createTextMessage("spring......topic!~!");
            }
        });
    }
}
```

#### 消费者

一般消费者使用监听器监听

创建一个监听类,一会监听消息  注意需要添加报扫描:

```java
@Component
public class ActiveMQQueue implements MessageListener {
    public void onMessage(Message message) {
        /*
        StreamMessage -- Java原始值的数据流 
        MapMessage--一套名称-值对
        TextMessage--一个字符串对象（常用）
        ObjectMessage--一个序列化的 Java对象
        BytesMessage--一个字节的数据流
        各种类型接收
        */
        //例子
        TextMessage value = (TextMessage) message;

        try {
            System.out.println(value.getText());
        } catch (JMSException e) {
            e.printStackTrace();
        }
    }
}
```

创建消费者配置文件

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:amq="http://activemq.apache.org/schema/core"
       xmlns:jms="http://www.springframework.org/schema/jms"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
        http://activemq.apache.org/schema/core
   		http://activemq.apache.org/schema/core/activemq-core-5.7.0.xsd
   		http://www.springframework.org/schema/jms http://www.springframework.org/schema/jms/spring-jms.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <!-- 扫描包 -->
    <context:component-scan base-package="com.activemq_demo1"></context:component-scan>

    <!-- 消费者 -->
    <amq:connectionFactory id="connectionFactory" brokerURL="tcp://localhost:61616"
                           userName="admin"   password="admin"></amq:connectionFactory>
    <bean id="cachingConnectionFactory" class="org.springframework.jms.connection.CachingConnectionFactory">
        <property name="targetConnectionFactory" ref="connectionFactory" />
        <property name="sessionCacheSize" value="5" />
    </bean>

    
    <!-- 配置监听 -->
    <!-- 
		cachingConnectionFactory:连接工厂
		destination-type:监听模式  队列/广播
		container-type:好像是多线程相关		default/simple
 	-->
    <jms:listener-container connection-factory="cachingConnectionFactory" destination-type="topic" container-type="default" >
        <!--
 			destination:监听名称
			activeMQQueue:监听器对象
 		-->
        <jms:listener destination="spring_topic" ref="activeMQQueue"></jms:listener>
    </jms:listener-container>
<!--    <jms:listener-container connection-factory="cachingConnectionFactory" destination-type="queue" container-type="default" >
        <jms:listener destination="spring_queue" ref="activeMQQueue"></jms:listener>
    </jms:listener-container>-->
</beans>

```

接收消息:

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:消费者配置文件.xml")
public class Test2 {

    @Test
    public void test1(){
        //一定要加while 死循环,要不不能接收
        while(true){}
    }

}

```

#### Tomcat下运行:

```xml
消费者监听器会自动监听,tomcat下只要加载配置监听器的配置文件就可以了
```



