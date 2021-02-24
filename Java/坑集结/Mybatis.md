## 明明设置A类型,mybatis报错却报通过B类型get

```java
java.sql.SQLException: Invalid value for getInt() 或  java.sql.SQLException: Invalid value for get*()
```

如果select 出来的列明和表名名称一样，column那就要区分一下大小写了...

必须保证resultMap中collection标签下的column指向的名称和数据库表列名称一致,包括大小写,不以select 出的列名为准







