# KafkaConnector

kafka自带工具,其他系统数据导入到kafka，从kafka导出到其他系统比较方便。

## 配置

配置文件是config/connect-standalone.properties

```properties
bootstrap.servers=localhost:9092  #kafka服务器
rest.port=8083	#http接口端口
offset.storage.file.filename=/tmp/connect.offsets #指定connector 发送位置
```

## 单节点启动

```
./bin/connect-standalone.sh ./config/connect-standalone.properties ./config/connector配置文件.properties [./config/connector配置文件.properties ...]
```

一个connector配置文件对应一个connector, 一次可以启动多个, 至少启动一个。

## HTTP API

GET /connectors 返回一个活动的connect列表
POST /connectors 创建一个新的connect；请求体是一个JSON对象包含一个名称字段和连接器配置参数

GET /connectors/{name} 获取有关特定连接器的信息
GET /connectors/{name}/config 获得特定连接器的配置参数
PUT /connectors/{name}/config 更新特定连接器的配置参数
GET /connectors/{name}/tasks 获得正在运行的一个连接器的任务的列表

DELETE /connectors/{name} 删除一个连接器，停止所有任务，并删除它的配置

GET /connectors 返回一个活动的connect列表

POST /connectors 创建一个新的connect；请求体是一个JSON对象包含一个名称字段和连接器配置参数

GET /connectors/{name} 获取有关特定连接器的信息
GET /connectors/{name}/config 获得特定连接器的配置参数
PUT /connectors/{name}/config 更新特定连接器的配置参数
GET /connectors/{name}/tasks 获得正在运行的一个连接器的任务的列表

DELETE /connectors/{name} 删除一个连接器，停止所有任务，并删除它的配置



## 资源

### JDBC connector 实现

https://www.confluent.io/hub/

https://github.com/debezium/debezium







