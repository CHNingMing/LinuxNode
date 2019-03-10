# Typedef使用





# 常用头文件

string.h 		常用字符串处理

stdlib.h		对内存操作



### unsigned/signed有/无符号类型

unsigned:

​	值范围只能是正数

修饰:

​	unsigned  类型  变量;

占位符%u:

​	表示无符号占位符



### 占位符

​	%x		输出一个十六进制

​	%o		输出一个八进制

#### 打印占位符打印单个%需要两个%%	

### 八进制

​	值以0开头表示整个数据是八进制

### 两种常量名定义:

const 数据类型 变量名;    (c中不安全)

#define 变量名 ;



# 数据类型

###  各种类型字符串打印方式:

整形：%d

短整型：%hd

长整形：%ld

长长整形：%lld

无符号整形：%u



## lang

lang类型C中没有明确规定长度，根据系统不同长度不同,window 为 4,linux 32位时为4,64 位时为8.

虽然没有明确规定，但是规定short必须小于int,int 必须小于lang,lang 必须小于lang lang

## lang lang

C99定义，一般电脑装的都是C89

 

## char

占用1个字节



