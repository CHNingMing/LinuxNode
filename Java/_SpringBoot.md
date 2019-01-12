# SpringBoot

整个Spring Boot 主要目的是为了简化搭建框架过程

## EJB

```
EJB是sun的JavaEE服务器端组件模型，设计目标与核心应用是部署分布式应用程序。简单来说就是把已经编写好的程序（即：类）打包放在服务器上执行。凭借java跨平台的优势，用EJB技术部署的分布式系统可以不限于特定的平台。EJB (Enterprise JavaBean)是J2EE(javaEE)的一部分，定义了一个用于开发基于组件的企业多重应用程序的标准。其特点包括网络服务支持和核心开发工具(SDK)。 在J2EE里，Enterprise Java Beans(EJB)称为Java 企业Bean，是Java的核心代码，分别是会话Bean（Session Bean），实体Bean（Entity Bean）和消息驱动Bean（MessageDriven Bean）。在EJB3.0推出以后，实体Bean被单独分了出来，形成了新的规范JPA。			--百度百科
```

### 轻量级和重量级关系

```
轻量级：一套技术，可以自定义选择用那些技术
重量级：一套技术，如果想用这套技术其中一点，整套技术都需要运行
```

### SpringBoot目录

```
spring-boot-starter 核心模块，包含自动配置支持、日志库和对 YAML 配置文件的支持。
spring-boot-starter-aop 支持面向切面编程（AOP），包含 spring-aop 和 AspectJ 。
spring-boot-starter-data-mongodb 包含 spring-data-mongodb 来支持 MongoDB。
spring-boot-starter-redis 支持Redis键值存储数据库，包含spring-redis
spring-boot-starter-jdbc 支持使用 JDBC 访问数据库。
spring-boot-starter-test 包含常用的测试所需的依赖，如 JUnit、Hamcrest、Mockito 和 spring-test 等。
spring-boot-starter-web 支持 Web 应用开发，包含 Tomcat 和 spring-mvc、spring-webmvc
spring-boot-starter-websocket 支持使用 Tomcat 开发 WebSocket 应用。
spring-boot-starter-ws 支持 Spring Web Services。
spring-boot-starter-log4j 添加 Log4j 的支持。
spring-boot-starter-logging 使用 Spring Boot 默认的日志框架 Logback。
spring-boot-starter-mail 支持javax.mail模块
spring-boot-starter-remote-shell 支持远程 SSH命令操作。
spring-boot-starter-tomcat 使用 Spring Boot 默认的 Tomcat 作为应用服务器。
spring-boot-starter-jetty 使用 Jetty 而不是默认的 Tomcat 作为应用服务器。
```

### 步骤：











