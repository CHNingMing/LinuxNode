# MyBatis

## XML核心配置文件

#### 配置MyBatis核心配置文件时,一定要注意各项顺序,可以鼠标移动到configuration标签提示查看顺序

LazyLoadingEnable		设置延迟加载,**true表示延迟加载**

aggressiveLazyLoading	当访问类中一个属性时,自动加载其他属性,**默认为true**

两项默认值经常发生变化,一般最好全设置好

## 三种使用MyBatis方式:

### 实体类+XML配置文件

在mappers下配置mapper

<mapper resource="xxx/xx/xx.xml" />

指定xml下的namespace值是**实体类全路径**

### 通过SqlSession下的相关数据库操作方法执行,

操作数据库方法传递参数:

	**实体类全路径.XML配置文件具体操作数据库名**
	
	**如果有参数,在第二个参数传递参数,可以传递多个,参数声明是Object**

### 接口+XML配置文件

在mappers下配置mapper

<mapper resource="xxx/xx/xx.xml" />

指定xml下的namespace值是**接口全路径**

### 接口+注解

在mappers下配置mapper

<mapper class="com.x.xx.Xxx" />

接口中方法上添加@Select注解,主要用来**执行特别简单SQL时使用**

## 应用参数几种方式:

	#:采用SQL预处理方式处理SQL,防止SQL注入
	
	$:使用字符串拼接方式处理SQL
	
	单个参数,**直接#{}或${}获取**
	
	传入POJO对象时,**#{对象属性}**

多参数下取值

### 多参数下取值

	多参数情况下,MyBatis自动把多个参数转成Map集合
	
	默认只能使用:   **0,1,2....** 或者 **param1,param2,param3,param4...** 按照映射**方法内参数顺序取值**
	
	如果使用自定义变量,在方法参数前加@Param注解

```java

public XXX getXXXById(@Param("自定义变量名称" 变量类型 变量参数名/变量名)){
    
}
XML使用时:
<select id="xxx" resultType="XXX" >
	#{自定义变量名称}
</select>

```

## 动态SQL

### if标签

	test="变量判断"

如果test为true,显示if标签下内容

### 多条件

#### choose多条件标签,类似switch

```
<choose>	
	<when test="">	//类似case
		
	</when>
	<when test="">
		
	</when>
	....
	<otherwise>		//如果上边不成立,显示
		
	</otherwise>
</choose>
```

#### trim

	主要用来处理**SQL语句开头和结束**,保证SQL语句没有语法错误
	
	prefix				SQL语句开始前添加指定内容
	
	suffix				SQL语句结束后添加指定内容
	
	prefixOverrides		SQL语句开始前,如果有指定内容,删除
	
	suffixOverrides		SQL语句结束后,如果有指定内容,删除

#### Where 

	自动去除 AND 或者 OR


​	

### Foreach

collection		集合对象

open			开始字符串

separator		每个集合分割字符串

close			结束字符串

item			每个集合对象

index			当前循环遍历索引

### resultMap

对于查询多个表或者一个实体类属性不能满足的情况

	<id colum="数据库主键字段" property="对应实体类属性">标签,配置数据库主键
	
	<result colum="数据库字段" property="对应实体类字段" >
	
	一对一情况下(并且只获取关联表某个字段数据):
	
		<result colum="数据库关联字段" property="实体类关联类属性名.关联类属性(关联类主键)"
	
	一对一情况下获取关联对象:
	
		<association property="实体类下声明关联类属性名" javaType="关联类全路径">
	
			<id .... />
	
			<result .../>
	
		</association>

#### 分布查询

	1.XML中声明一个通过ID查询具体关联表的查询,**XML已经和接口绑定情况下**
	
		select * from xx where id = #{xx}


​	

	<association property="实体类下声明关联对象属性名" select="接口全路径.关联表查询" >
	
	</association>

## 特殊符号处理

	     **&            &amp;**
	
		**<            &lt;**
	
	     **>            &gt;**
	
	     **"             &quot;**
	
	     **'              &apos;**

## MyBatis整合Log4j

导入log4j依赖

添加log4j.properties

```
# direct log messages to stdout ###
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.Target=System.out
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{ABSOLUTE} %5p %c{1}:%L - %m%n

### direct messages to file mylog.log ###
log4j.appender.file=org.apache.log4j.FileAppender
log4j.appender.file.File=c\://log//mylog.log  //\u8BB0\u5F55\u65E5\u5FD7\u7684\u6587\u4EF6\u4F4D\u7F6E
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=%d{ABSOLUTE} %5p %c{1}:%L - %m%n

### set log levels - for more verbose logging change 'info' to 'debug' ###

log4j.logger.com.testX.dao=trace,stdout 
com.testX.dao:是映射接口所在包


```







## MyBatis缓存

## 一级缓存	SqlSession级别

一级缓存是默认开启的,当创建一个SqlSession时表示已经开启一个**一级缓存**

### 一级缓存数据有效期

- 多个SqlSession之间缓存不是共享的

- 当SqlSession对象调用clearCache方法的时候自动清除缓存

- 当SqlSession调用Close关闭的时候清除缓存

- 当调用 增  删   改相关方法时,会自动清除缓存

  #### 缺点:

  	不能对本地缓存数据进行精确的控制数据:
  	
  		数据大小
  	
  		数据是否过期
  	
  		更新缓存数据


  	

  #### 实现原理:

  	内部通过Map存储
  	
  	SqlSession内部维护了一个本地缓存,当用户请求来查询数据时,SqlSession自动先去LocalCache找相应数据,如果没有再去请求数据库,如果有(表示之前请求过相同请求)就直接返回给用户

### 二级缓存namespace级别

一个XML文件对应一个二级缓存

#### 请求流程

	当用户请求过来时,先去二级缓存中查询相关数据,如果有直接返回给客户,如果没有再去一级缓存中查询数据,一级缓存中有返回,没有去数据库中查询

#### 使用二级缓存注意事项

	当SqlSesion关闭时(调用Close)才会把数据写入本地缓存

1. 手动开启二级缓存
   1. 在MyBatis核心配置文件<settings><setting name="cacheEnable" value="true">

2. 在响应XML中添加cache标签表示开启缓存标签
3. 在响应XML下响应查询标签中添加useCache="true"属性

### 开放Cache接口,可以整合第三方缓存框架

MyBatis





## -----具体流程

使用mybatis必须导入的jar:mybatis-x-x-x.jar

导入依赖使用：

```xml
<dependency>
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis</artifactId>
  <version>x.x.x</version>
</dependency>
```

SqlSessionFactoryBuilder:主要用来创建SqlSessionFactory

通过SqlSessionFactoryBuilder创建SqlSessionFactory

配置MapperScannerConfigurer，接口映射

扫描基础包

# 问题总结：

### MyBatis一直死循环，不报错：

1. 	保证**映射文件完整性**		标签、参数、保证collection和asse...标签中select对应上每个方法
	. 	select标签有id名称如果写param或者result属性后，是否有对应的值，如果时类路径保证路径正确
	. 	保证每个映射文件namespace正确和对应的实体类正确,实体类对应路径正确
	. 	Entity/Domain下实体类不能有多层，只能有一层
	. 	保证Mapper映射文件中不能有重复的方法

## 启动报错



## test中语法冲突/语法错误/语法不完整报错：

```
Was expecting one of:
 ":" ...
 "not" ...
 "+" ...
 "-" ...
 "~" ...
 "!" ...
 "(" ...
 "true" ...
 "false" ...
 "null" ...
 "#this" ...
 "#root" ...
 "#" ...
 "[" ...
 "{" ...
 "@" ...
 "new" ...
 <IDENT> ...
 <DYNAMIC_SUBSCRIPT> ...
 "\'" ...
 "`" ...
 "\"" ...
 <INT_LITERAL> ...
 <FLT_LITERAL> ...
```

### if比较

首先保证两个变量类型一致

字符串比：  xx='字符串'  /   xx=”字符串“   保证字符串位数大于1



## 步骤：

导入依赖：

```xml
  <!-- mybatis必须依赖 -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.2.8</version>
        </dependency>
        <!-- 数据库驱动 -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.6</version>
        </dependency>
        <!-- 数据库连接池 -->
        <dependency>
            <groupId>c3p0</groupId>
            <artifactId>c3p0</artifactId>
            <version>0.9.1.2</version>
        </dependency>
        <!-- Spring相关依赖 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>4.1.7.RELEASE</version>
        </dependency>
        <!-- 操作数据库必备 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>4.1.7.RELEASE</version>
        </dependency>
        <!-- MyBatis整合Spring依赖 -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>1.2.2</version>
        </dependency>
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
        <!-- 测试 -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
```



创建数据库配置文件：db.properties

```
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://192.168.56.103:3306/demo
username=root
password=203358
```

创建MyBatis配置文件：conf.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    
</configuration>
```

创建Spring配置文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.1.xsd
        http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.3.xsd
        http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-4.3.xsd
        ">
    <!--加载配置文件-->
    <context:property-placeholder location="classpath:db.propertis" />

    <!-- 配置数据库连接池 -->
    <bean id="database" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="driverClass" value="${driver}" />
        <property name="jdbcUrl" value="${url}" />
        <property name="user" value="${username}" />
        <property name="password" value="${password}" />
    </bean>
    <!-- 创建MyBatis会话工厂 -->
    <bean id="sqlSessionFactoryBean" class="org.mybatis.spring.SqlSessionFactoryBean" >
        <property name="dataSource" ref="database"/>
        <!-- 要映射的XML文件位置 -->
        <property name="mapperLocations" value="classpath:Mapper/*.xml"></property>
        <!-- 配置远程MyBatis配置文件位置 -->
        <property name="configLocation" value="classpath:spring/conf.xml"></property>
        <!-- 类型别名,所在包路径 -->
        <property name="typeAliasesPackage" value="com.mybatis_demo.domain" ></property>
        <!-- 映射接口 -->
    </bean>
    <!--自动对象关系映射-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <!--指定会话工厂名称-->
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactoryBean"/>
        <!-- 扫描Dao层 -->
        <property name="basePackage" value="com.mybatis_demo.dao" />
    </bean>
    <!-- 扫描基础包 -->
    <context:component-scan base-package="com.mybatis_demo" />


    <!-- 声明式事物管理 -->
<!--    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="database" />
    </bean>-->
    <!-- 添加注解 -->
    <!--<tx:annotation-driven transaction-manager="transactionManager" />-->


</beans>
```

创建操作数据库接口：

```java
MatchRecord：临时实体类对象
	public List<MatchRecord> findAll();	//集合情况下
    public MatchRecord findOne(@Param("id") Integer id);//传递进来参数情况下
    public MatchRecord findTest(@Param("sql") String sql);
    public void add(MatchRecord match);//添加情况下

```

根据接口创建映射文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!-- 接口全路径 -->
<mapper namespace="com.mybatis_demo.dao.MatchDao">
    <!-- 简单查询 -->
    <select resultType="MatchRecord" id="findAll"  >
        select * from match_record
    </select>
    <select id="findOne" resultType="MatchRecord" parameterType="Integer">
        select * from match_record where id = ${id}
    </select>
    <!-- 查询时语句 -->
    <select id="findTest" resultType="MatchRecord" parameterType="String">
        ${sql}
    </select>
    <!-- 插入时语句 -->
    <insert id="add" parameterType="MatchRecord">
        insert into match_record values(#{id},#{match_data},#{result});
    </insert>
</mapper>
```

最后自动注入接口，调用接口方法





