# Elasticsearch

首先:Elasticsearch服务器必须和Elasticsearch依赖版本对应

根据依赖版本找到响应的spring-data-elasticsearch

在Elasticsearch添加spring相关依赖

### ElasticSearch数据机制概念

索引

在一个索引对象上，可以存储多种不同类型的数据，可以看成关系型数据库中的表

文档

存储在搜索服务器上的数据，一个文档相当于表中的一条记录

文档类型

一个索引对象，可以存储多种不同类型，类型可以在文档上标注

映射

数据如何存储在索引对象上，需要映射配置，数据类型，是否存储，是否分词

### 访问:

	客户端访问:ip:3200
	
	服务端访问:ip:9300
	
	head插件访问:ip:9200/_plugin/head
	
	测试访问:http://localhost:9200/_analyze?analyzer=ik&pretty=true&text=我是中国人



### 步骤:

添加配置文件

```xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:elasticsearch="http://www.springframework.org/schema/data/elasticsearch"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
         http://www.springframework.org/schema/data/elasticsearch http://www.springframework.org/schema/data/elasticsearch/spring-elasticsearch.xsd
         http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context-3.1.xsd
        ">
        <!-- 加载配置文件 -->
        <context:property-placeholder location="classpath:es.properties"></context:property-placeholder>
    
    
    <!-- 配置名称和es服务器节点地址,节点可以配置多个 -->
    <elasticsearch:transport-client id="client"
                                    cluster-nodes="127.0.0.1:9300"  />
    <!-- 扫描Dao 层包 -->
    <elasticsearch:repositories base-package="com.elasticsearch_dao"></elasticsearch:repositories>
    <!-- es模板类 -->
    <bean id="elasticsearchTemplate" class="org.springframework.data.elasticsearch.core.ElasticsearchTemplate">
        <!-- 加载客户端 -->
        <constructor-arg name="client" ref="client" ></constructor-arg>
    </bean>
</beans>
```

### 创建实体类:

```
indexName:索引名称
type:索引类型
@Document(indexName = "demo_index1",type = "article")		//切记名称不能有大写
类名
@Id
id字段		//无论设置什么类型,最后都会转成String
@Field(type = FieldType.String,index = FieldIndex.not_analyzed,store = true)
普通字段
```

@Field 字段与文档映射关系配置，（

[index 是否索引  值:FieldIndex枚举],

[analyzer= "分词器名称"指定分词器],

[字段数据类型type 值：FieldType枚举值]，

[store是否存储 = true 原则：搜索的字段内容是否需要展示，如果需要将内容展示，需要存储]，

[searchAnalyzer 搜索内容使用的分词器是什么]

）



FieldIndex枚举

no	不给当前列建立索引

analyzed	添加索引，分词建立索引

not_analyzed	建立索引不分词，如果内容没有中文，又需要建立索引，会把整个内容放到索引库中

### 创建Dao层

```
创建接口,继承ElasticsearchRepository<实体类,主键类型`>
```

注入Dao,ElasticsearchRepository已经继承了Repository,基本操作