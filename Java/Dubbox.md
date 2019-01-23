## Dubbox

https://github.com/apache/incubator-dubbo/releases

### 生产者和消费者

模块和模块之间使用的是轻量级的通信协议 http

### 支持的协议

```


```

### 安装步骤：

1. 解压dubbo
2. 修改conf下的zoo_simxx.conf 改成  zoo.conf
3. 修改dataDir下数据文件，保证有目录
4. 进入bin目录，执行./zkServer.sh



### 调用步骤

#### 导jar包

```xml
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
            <groupId>com.alibaba</groupId>
            <artifactId>dubbo</artifactId>
            <version>2.8.4</version>
        </dependency>
        <dependency>
            <groupId>org.apache.zookeeper</groupId>
            <artifactId>zookeeper</artifactId>
            <version>3.4.8</version>
        </dependency>
        <dependency>
            <groupId>org.javassist</groupId>
            <artifactId>javassist</artifactId>
            <version>3.15.0-GA</version>
        </dependency>
        <dependency>
            <groupId>org.apache.curator</groupId>
            <artifactId>curator-client</artifactId>
            <version>2.5.0</version>
        </dependency>
        <dependency>
            <groupId>com.101tec</groupId>
            <artifactId>zkclient</artifactId>
            <version>0.9</version>
        </dependency>

	<!-- 插件 -->

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.tomcat.maven</groupId>
                <artifactId>tomcat7-maven-plugin</artifactId>
                <version>2.2</version>
            </plugin>

            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.6.1</version>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                </configuration>
            </plugin>
        </plugins>
    </build>




```



#### 创建模块和模块之间通信的接口

生产者和消费者**都必须有这个接口**

并且两个模块必须保证这个接口的所在**包明和接口名一致**（Dubbo需要根据**所在包名和接口名区分服务**）

如果是项目，生产者和消费者之间引用同一个接口，就没有包名不一致导致服务不一致问题

```java
package 包名一定要一致～～！

public interface xxx{
    //....
}
```

#### 生产者配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:dubbo="http://code.alibabatech.com/schema/dubbo"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://code.alibabatech.com/schema/dubbo
       http://code.alibabatech.com/schema/dubbo/dubbo.xsd
        ">
    <!-- 提供方应用名称信息，这个相当于起一个名字，我们dubbo管理页面比较清晰是哪个应用暴露出来的  -->
    <dubbo:application name="dubbo-provider1" />
    <!--使用注解方式暴露接口
    <dubbo:annotation package="wang.raye.dubbodemo1" />  -->
    <!-- 使用zookeeper注册中心暴露服务地址 -->
    <dubbo:registry address="zookeeper://localhost:2181"></dubbo:registry>
    <!-- 要暴露的服务接口-->
    <dubbo:annotation package="com.service.impl到通信接口实现类所在包" />

</beans>
```

#### 配置web.xml

```xml
   <!-- 加载配置文件 -->
	<context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:ApplicationContext.xml</param-value>
    </context-param>
	<!-- 加载Spring类加载器 -->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

```

#### 启动tomcat									pom设置war没

#### 消费者

配置文件

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xmlns:dubbo="http://code.alibabatech.com/schema/dubbo"
       xmlns:context="http://www.springframework.org/schema/context"
   xsi:schemaLocation="http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans.xsd
   http://code.alibabatech.com/schema/dubbo
   http://code.alibabatech.com/schema/dubbo/dubbo.xsd
   http://www.springframework.org/schema/context
   http://www.springframework.org/schema/context/spring-context-3.1.xsd
    ">
    <!-- 服务注册中心名称 -->
    <dubbo:application name="dubbo-provider1" />
    <!-- 注册中心地址 -->
    <dubbo:registry address="zookeeper://localhost:2181" />
	<!-- 那个包下的类需要远程注入，写下包名 -->
    <dubbo:annotation package="com.test1" />
    <!-- 扫描包 -->
    <context:component-scan base-package="com.controller" />

</beans>
```



#### 远程调用引用

```

@Reference
private 接口  xxx;


```



# Dubbo 服务治理工具

通过github 下载[dubbo-2.5.10](https://github.com/apache/incubator-dubbo/releases/tag/dubbo-2.5.10)以下版本，因为以上版本已经被砍掉dubbo-admin

1. 下载后解压，进入dubbo-admin
2. 打开/root/桌面/opt/develop/incubator-dubbo-dubbo-2.5.10/dubbo-admin/src/main/webapp/WEB-INF/dubbo.properties
3. 配置连接地址，root登录名，默认用户名：root，密码：root
4. 可以通过服务名，ip地址，应用名搜索
5. 服务名就是**通信接口全类名**，也可以是*表示全部
6. 可以输入ip查询，不用输入端口号自动搜索



