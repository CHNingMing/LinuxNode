



# 基本操作：

## Record

NUTZ自定义实体，类似Map

把查询结果列名为key ,列名对应值 为value

## Entity

各种数据库实体类，类中标注 实体类对应表明，字段，主键/唯一标识

```
@Id：表示主键
@Column("字段名")：对应数据库字段名
@ColDefine(type=ColType.数据类型[,width=数据长度])
```

## Dao 

```
org.nutz.dao.Dao;
```

**数据库基本操作**

```java
Entity/Record dao.fetch(Entity.class,Condition)   //查询单条记录

List<Entity/Record> dao.query(Entity.class,Condition); //查询多条记录
```

## Condition

条件对象

## Cnd

```
org.nutz.dao.Cnd;
```

主要用来创建条件(Condition)
**Condition** Cnd.where("字段","运算符","值")[.and().or()];