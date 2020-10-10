# Kafka

消息中间件,发布/订阅模式

一个主题(Topic)下可以有多个分区(partitioner)。

## 生产者

生产者生产消息,根据分区策略选择将消息发送到那个分区.

### 生产命令:

```
./kafka-console-producer.sh --broker-list <kafka节点>:<端口> --topic <发送主题>
```

## 消费者

消费者订阅主题前需要配置分组ID(group id), 多个消费者可以使用同一分组ID。

消费者订阅主题时可以配置只接受主题下指定分组消息。

一条消息，只能被统一分组内,一个消费者消费。

可以被不同分组内消费者**重复**消费。

### 消费命令:

```
./kafka-console-consumer.sh --bootstrap-server <kafka节点>:<端口> --from-begining --topic <主题>
```

### 创建主题

```
kafka-topics.bat --create -zookeeper localhost:2182 --replication-factor 2 --partitions 3 --topic testMcdull222
```

--partitions: 分区数量

-zookeeper: 制定zookeeper地址

--topic: 指定topic名称















