# MYSQL API

## 初始化

mysql_init(MYSQL * mysql);

## 设置编码(防止中文乱码)

mysql_set_character_set(MYSQL *mysql, char * csname)

## 连接

mysql_real_connect(MYSQL *mysql, const char *host,
					   const char *user,
					   const char *passwd,
					   const char *db,
					   unsigned int port,
					   const char *unix_socket,	//NULL
					   unsigned long clientflag);	//0

## 执行查询

mysql_query(MYSQL *mysql,char * sql);

mysql_real_query(MYSQL *mysql, char * query , unsinged int length)

query: sql

length: sql的长度，和mysql_query的区别是少了算query长度操作,mysql_query自动算sql语句长度

## 获取结果集

获取上次执行查询后的结果集

MYSQL_RES * mysql_storr_result(MYSQL *mysql);

## 获取受影响行数

unsigned int mysql_affected_rows(MYSQL *mysql);

## 获取结果集中一行

MYSQL_RES mysql_fetch_row(MYSQL_RES * mysqlRes);





