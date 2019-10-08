



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

## Chain

类似pojo,主要用在插入和更新上

Chain代替poji:

Chain Chain.make(pojoAttr,value);

```java
Chain pojo = Chain.make("name","zhangsan");
pojo.add("age",18);
dao.update("perso",pojo,Cnd.where("pid","=",1));
dao.add("perso",pojo);
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



# 注解

## 主键注解：

@PK多个复杂主键时试用，标记类中

```java
@PK({"date","type"})
class A{
    Date date;
    Integer type;
}
```

@Name字符串主键时试用标记字段中

@Id 数字类型主键中试用，标记字段中

```java
class A{
    @Name
    Date date;
    @Id
    Integer type;
}
```







# 其他注意：

不要使用内部类当实体,不要使用内部类当实体,不要使用内部类当实体....

