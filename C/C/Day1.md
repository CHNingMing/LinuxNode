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

​	

#### 打印占位符打印单个%需要两个%%	

### 八进制

​	值以0开头表示整个数据是八进制

### 两种常量名定义:

#### const

const 数据类型 变量名=值;    (c中不安全)

数据类型 const 变量名=值;

#### #define

define声明的变量，预处理阶段，会把用到的变量替换成对应值

#define 变量名 值;

通过输出预处理文件，可以发现两个定义常量区别

### 常见常量写法：

十进制、八进制或十六进制的常量

十进制(默认) : 100

八进制 : 0123

十六进制 : **0x/0X**123E

长整数 :1111L

无符号整数：100U

无符号长整数 :100UL

## 无符号整数和有符号整数区别

类型支持负数，就是有符号整数，不支持就是无符号整数

数值最后都会以二进制存储，二进制最左边一位表示数值是正数还是负数。

如果二进制最左边一位数值是和后边二进制连起来表示一个整数(没有存储整数负数位)，表示这是无符号整数。



# 数据类型

###  各种类型字符串打印方式:

整形：%d

短整型：%hd

长整形：%ld

长长整形：%lld

无符号整形：%u

### 地址占位符:%p

内存地址是按照16进制存储的

## lang

lang类型C中没有明确规定长度，根据系统不同长度不同,window 为 4,linux 32位时为4,64 位时为8.

虽然没有明确规定，但是规定short必须小于int,int 必须小于lang,lang 必须小于lang lang

## lang lang

C99定义，一般电脑装的都是C89

 

## char

占用1个字节

## int

2 或 4 字节



