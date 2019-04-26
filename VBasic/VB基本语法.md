# VB基本语法

VB 和其他语言不太一样，不需要每行都有 ;

## 声明变量：

```vb
dim a,b,c
```

[待确定]VB是弱类型语言

声明变量是指定类型:

```vb
dim count as Double
```

## VB数据类型

Double 

String

​	字符串拼接两种用法：

```vb
//1	在字符串和字符串拼接用 + ，字符串和其他类型拼接用&
dim str
str = "a" + str 
//2
str = "a" & str
```

## 声明常量：

符号型常量





### 直接常量

const 名称 as 类型 = 值

```vb
Const Pi as String = 3.1415926
```



## 字符串转数字

int Val(String )

数字相加多用 + 



## 运算符

\+ - * / 



## Select 多条件判断 类似switch

```vb
dim a
a = "zhangsan"
Select case a
case "zhangsan"
    //...
case "lisi"
    //...
case "wangyu"
    //...
case "zhaoliu"
    //...
case "mutouqi"
    //...
ENd Select

```



## IF

```vb
//if
    if a > b then 
        //..
    end if
    //if else
        if a > b then 
            //..
        else 
            //..
        end if
       // if else if 
       if a > b then 
                //..
        else if a > c then 
                //..
        end if




```

## For循环

```vb
for i = 0 to 20
msgbox i
next
```

## 字符串

### 得出字符串长度

int len(String )

### 截取字符串

Stirng mid(String,startindex,num)

string:要截取的字符串

startindex:截取字符串开始位置

num:从开始位置截取几位













