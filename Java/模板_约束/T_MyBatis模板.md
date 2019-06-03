\>MySql5.7版本

```
driver=com.mysql.jdbc.Driver
url=jdbc:IP地址:端口/数据库?useUnicode=true&characterEncoding=utf-8  设置数据库编码
username=
password=

```

<MySql 5.7版本

```
url: jdbc:mysql://IP地址:端口/数据库?autoReconnect=true&useUnicode=true&characterEncoding=utf8&zeroDateTimeBehavior=CONVERT_TO_NULL&useSSL=false&serverTimezone=UTC


```

zeroDateTimeBehavior=CONVERT_TO_NULL		CONVERT_TO_NULL必须是大写,小写也会报错.