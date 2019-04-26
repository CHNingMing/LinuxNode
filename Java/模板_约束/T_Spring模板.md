SpringXML

```
<?xml version="1.0" encoding="UTF-8"?>
```

Spring 约束

``` xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:jms="http://www.springframework.org/schema/jms"
    xmlns:tx="http://www.springframework.org/schema/tx" 
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:mvc="http://www.springframework.org/schema/mvc" 
    xmlns:task="http://www.springframework.org/schema/task"
	<!-- 插件部分 -->
    xmlns:amq="http://activemq.apache.org/schema/core"
    xmlns:elasticsearch="http://www.springframework.org/schema/data/elasticsearch"
	<!-- Dubbo -->
	xmlns:dubbo="http://code.alibabatech.com/schema/dubbo"
	<!-- WebService -->
	xmlns:jaxws="http://cxf.apache.org/jaxws"
	xmlns:jaxrs="http://cxf.apache.org/jaxrs"
	<!-- 插件部分结束 -->
xsi:schemaLocation="
    http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/tx
    http://www.springframework.org/schema/tx/spring-tx-3.1.xsd
        http://www.springframework.org/schema/aop
    http://www.springframework.org/schema/aop/spring-aop-3.1.xsd
        http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context-3.1.xsd
        http://www.springframework.org/schema/mvc
    http://www.springframework.org/schema/mvc/spring-mvc-3.1.xsd
        http://www.springframework.org/schema/task
    http://www.springframework.org/schema/task/spring-task-3.1.xsd
	<!-- 插件部分 -->
        http://activemq.apache.org/schema/core
    http://activemq.apache.org/schema/core/activemq-core-5.7.0.xsd
        http://www.springframework.org/schema/jms
    http://www.springframework.org/schema/jms/spring-jms.xsd
	   http://code.alibabatech.com/schema/dubbo
   	http://code.alibabatech.com/schema/dubbo/dubbo.xsd
		http://cxf.apache.org/jaxws 
	http://cxf.apache.org/schemas/jaxws.xsd
		http://cxf.apache.org/jaxrs
	http://cxf.apache.org/schemas/jaxrs.xsd

	<!-- 插件部分结束 -->
">
```

Spring插件

```

   <build>
        <plugins>
            JDK设置插件
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














