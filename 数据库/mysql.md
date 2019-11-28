[TOC]

# MySql

设置mysql密码:

```mysql

set password for 用户名@localhost = password('新密码');

```

设置连接权限：

```mysql
-- 设置权限
GRANT ALL PRIVILEGES ON *.* TO 'root(用户名)'@'192.168.39.1(允许连接的ip)' IDENTIFIED BY 'yourpasswd(连接时密码)' WITH GRANT OPTION
-- 刷新权限
flush privileges;
```

### 列转行

把一列数据按指定格式转换成一行显示,必须和分组配合使用

```mysql
select * from goods;
```

+------+------+
| id| price|
+------+------+
|1 | 10|
|1 | 20|
|1 | 20|
|2 | 20|
|3 | 200 |
|3 | 500 |
group_concat默认 ,  号分割

```mysql
select id, group_concat(price) from goods group by id;  
```

+------+--------------------+
| id| group_concat(price) |
+------+--------------------+
|1 | 10,20,20|
|2 | 20 |
|3 | 200,500|
+------+--------------------+
指定分隔符分割 

```mysql
select id ,group_concat(price,separator ';') from goods group id;
```
|1 | 10;20;20 |
|2 | 20|
|3 | 200;500 |
分割时排序

```mysql
select id,group_concat(price order by price desc) from goods group id;
```

### 日期处理

#### TIMESTAMPDIFF

算出两个日期之间差

类型

1. FRAC_SECOND。表示间隔是毫秒

2. SECOND。秒

3. MINUTE。分钟

4. HOUR。小时

5. DAY。天

6. WEEK。星期

7. MONTH。月

8. QUARTER。季度

9. YEAR。年

   ```mysql
   select TIMESTAMPDIFF([类型],开始日期,结束日期)
   ```

## Group

### 组连接:group_concat()

必须配合group 关键字使用。

group_concat([ distinct ] 连接字段 [ order by 排序字段 [separator '分割符'] ])

```sql
-- 假设t_a name有重复，id不重复,以_分割
select name,group_concat(distinct id order by id separator '_') from t_a group by name
```

### MySql 查询中涉及到中文字段查询时中文转换成？号问题：

在连接数据库时，添加对应参数:

```
?generateSimpleParameterMetadata=true&useUnicode=true&characterEncoding=utf8
```





## debian 安装mysql:

打开mysql官网，选择apt-repository,下载deb包，这个包安装需要一些命令，打开debian源基础上添加一个163源，即可安装那两个命令（查看系统版本命令）。

这个包时自动根据当前系统选择mysql版本。

安装时选择OK。

```
apt-get update
apt-get install mysql-server
```

期间输入密码和选择mysql密码强度，选择弱。

## 存储过程

### 基本语法

```sql
create [definer=用户@IP] procedure <名称> ( [ IN param <type>] [OUT param <type>] [INOUT param <type> ])
begin
-- 存储过程体

end
```

IN:输入参数

OUT:输出参数

INOUT:即是输入参数也是输出参数

OUT和INOUT声明的变量在存储过程体中**必须赋值**







## 函数





## 游标

1. 创建跳出游标条件变量

2. 声明游标
3. 设置游标跳出条件(类似监听)
4. 打开游标
5. 循环游标

```sql
create  definer = root@localhost function getLastInsertIdFun() returns varchar(100)
begin
    declare result varchar(300);
    declare t_str varchar(30);-- 临时存储游标循环变量
    declare done boolean;
    declare cursorA CURSOR FOR select o_no from rable_1;
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;
    open cursorA;
    read_loop: LOOP -- 创建一个read_loop名的循环
        -- 取一个数据到t_str
        fetch cursorA into t_str;
        if done then
            leave read_loop; -- 跳出循环，break;
            ITERATE read_loop; -- 跳出本次循环,continue;
        end if;
    end read_loop;
    close cursorA
    return result;
 end

```









## 问题：

systemctl status mysql.service				查看mysql错误信息

此次问题因为数据库容量满了。

# mysql密码重置

先停止mysql：

```
service mysql stop
```

运行安全模式：
```
mysqld --skip-grant-tables --user=root
```

启动安全模式后，会堵塞终端，在开一个终端，执行:

```
mysql -u root
```



如果提示没有mysqld文件夹，创建：

```
mkdir /usr/run/mysqld
```

报错后，三种查看错误方式：

```shell
systemctl status mysql.service
journalctl -xe
cat /var/log/mysql/error.log
```

error.log报错：

mysqld: File './binlog.index' not found (OS errno 13 - **Permission denied**)

**加粗英文表示权限被拒绝**

binlog.index在：/var/lib/mysql/binlog.index

给binlog.index所在的mysql目录设置权限：

```
chgrp -R mysql /var/lib/mysql
chown -R mysql /var/lib/mysql
```

**出问题Mysql版本：Server version: 8.0.16 MySQL Community Server - GPL**



# 问题

## TinyINT 长度为1 时,值只显示true/false

在连接字符串添加参数:

```&amp;tinyInt1isBit=false
&tinyInt1isBit=false
```

​	



