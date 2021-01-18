# 引入Maven

```xml
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>connect-api</artifactId>
    <version>2.5.0</version>
</dependency>
```

本实例connector配置文件:

```
name=connector name
topic=test-topic

```

# SourceConnector

从其他系统取数,发到Kafka

## 1. 创建ConnectorSource继承类

```java
public class ConnectorSourceDemo extends SourceConnector {
    //方便Task 发数据时标记主题名称
    public static String TOPIC_CONFIG = "";
    // 定义配置文件按项元数据
    //define(<名称>,<类型>,<默认值>,<不晓得>,<缺少此项配置,提示内容>)
    private final ConfigDef configDef = new ConfigDef()
            .define("name", ConfigDef.Type.STRING, null, ConfigDef.Importance.HIGH, "name is not null ")
            .define("topic", ConfigDef.Type.STRING, ConfigDef.Importance.HIGH, "The topic to publish data to")
        	//999为默认数据，若没配置,使用   只做实例,没得用
            .define("num", ConfigDef.Type.INT, 999, ConfigDef.Importance.HIGH, "")
            ;

    AbstractConfig abstractConfig = null;
    //启动connector调用
    public void start(Map<String, String> map) {
        //配置文件多个配置项(map)映射到(configDef)
        abstractConfig = new AbstractConfig(configDef, map);
        //手动设置主题
        TOPIC_CONFIG = abstractConfig.getString(TOPIC_CONFIG);
        System.out.println(abstractConfig.getInt("num"));
        System.out.println("-------------------------------------------------");
    }

    public Class<? extends Task> taskClass() {
        //返回Task class,实际发送到kafka时Task
        return ConnectorSourceTask.class;
    }
	//配置Task
    public List<Map<String, String>> taskConfigs(int i) {
        Map<String, String> config = new HashMap<String, String>();
        //必须配置topic,不配置应该会报错
        config.put("topic", abstractConfig.getString(TOPIC_CONFIG));
        return Collections.singletonList(config);
    }
	//connector停止时,释放资源
    public void stop() {
        System.out.println("stop connector!~");
    }

    public ConfigDef config() {
        return configDef;
    }
	
    public String version() {
        return "hello version!";
    }
}
```

### 2.创建SourceTask继承类

一个connector可以有多个task

```java
public class ConnectorSourceTask extends SourceTask {

    public String version() {
        return "task1.1.1";
    }
	//task启动时调用
    public void start(Map<String, String> map) {
        System.out.println("start task!");
    }
    private int num = 0;
    //要发送到kafka数据集合,task启动后会频繁掉poll方法,拿到List<SourceRecord>,发送到kafka 服务器
    //此处是实际从各个系统拿数据，拼成SourceRecord消息对象,发送到kafka过程
    public List<SourceRecord> poll() throws InterruptedException {
        num ++;
        List<SourceRecord> list = new ArrayList<SourceRecord>();
        System.out.println("test");
        //故意延时会,怕掉死了
        Thread.sleep(3000);
        Random random = new Random();
      	//*V* SourceRecord(<源分区>,<源位置>,<主题名称>,<key Schema>,<key Struct>,<value Schema>, <value Struct>) *V*
        /*SourceRecord sourceRecord = new SourceRecord(Collections.singletonMap("keyName", ""),
                Collections.singletonMap("value", random.nextInt(100)), ConnectorSourceDemo.TOPIC_CONFIG, null, Schema.STRING_SCHEMA, "connector key",
                Schema.STRING_SCHEMA, "{'age':"+String.valueOf(random.nextInt())+", 'money': "+String.valueOf(random.nextDouble())+", 'a': "+String.valueOf(random.nextBoolean())+"}", System.currentTimeMillis());*/
        Map<String, String> sourcePartition = Collections.singletonMap("keyName", "");
        Map<String, String> sourceOffset = Collections.singletonMap("value", "");
        //Schema可以理解成数据格式规范,Struct 是实际数据
        //简单没有嵌套Schema格式
        Schema keySchema = SchemaBuilder
            	//struct好像没用
                .struct().name("key-name")
                .field("name", Schema.STRING_SCHEMA)
                .field("id", Schema.INT32_SCHEMA);
        //没有嵌套keySchema对应Struct
        Struct structKey = new Struct(keySchema)
                .put("name", "A")
                .put("id", new Integer(random.nextInt(100)));
        Schema objSchema = SchemaBuilder.struct()
                .field("fly", Schema.BOOLEAN_SCHEMA)
                .field("play", Schema.BOOLEAN_SCHEMA)
                .field("see", Schema.BOOLEAN_SCHEMA);
        //复杂Schema格式
        Schema valueSchema = SchemaBuilder
                .struct().name("value-name")
                .field("age", Schema.INT32_SCHEMA)
                .field("money", Schema.FLOAT32_SCHEMA)
                .field("a", Schema.BOOLEAN_SCHEMA)
            	//obj是个对象,数据格式是objSchema
                .field("obj", objSchema)
                .build();
        Struct objStruect = new Struct(objSchema)
                .put("fly", new Boolean(random.nextBoolean()).booleanValue())
                .put("see", new Boolean(random.nextBoolean()).booleanValue())
                .put("play", new Boolean(random.nextBoolean()).booleanValue());
        Struct struct = new Struct(valueSchema)
                .put("age", new Integer(random.nextInt(10)).intValue())
                .put("money", new Double(random.nextDouble()).floatValue())
                .put("a", new Boolean(random.nextBoolean()).booleanValue())
            	//数据格式 objSchema 对应 objStruect
                .put("obj", objStruect)
                ;

        SourceRecord sourceRecord = new SourceRecord(sourcePartition, sourceOffset, ConnectorSourceDemo.TOPIC_CONFIG, 0, keySchema, structKey, valueSchema, struct);
        list.add(sourceRecord);
        return list;
    }

    public void stop() {
        System.out.println("stop..");
    }
}
```

connector启动后会疯狂调poll方法。

