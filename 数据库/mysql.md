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








