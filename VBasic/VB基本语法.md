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

### 跳出for循环

```vb
exit for
```



## 字符串

### 得出字符串长度

int len(String )

### 截取字符串

Stirng mid(String,startindex,num)

string:要截取的字符串

startindex:截取字符串开始位置,**开始位置不能小于 0** 

num:从开始位置截取几位





## 注释

```vb
rem 注释内容
```





## 函数

[访问修饰] function 函数名称([数据类型 参数明...]) [as 返回值类型]

function 定义的函数必须有返回值，返回值通过 as 数据类型   声明

函数名称 = 返回值

end function

```vb

public function hello() as String
    hello = "Hello VB Function!"
end function


private Sub xx_click()
    rem hello返回内容就是 Hello VB Function!
    msgbox hello()  
end sub

```

### 结束函数方法体，类似return 

```vb


public function hello( a as Integer)
    if a = 1 then
        msgbox a
        exit funciton
    end if
    msgbox "a不等于1"
    
    
end function


```

## 过程

类似函数，与函数不同的是，过程没有返回值。

[修饰符] sub 过程名()

```vb

private sub hello()
    msgbox "hello"
end sub

rem ....
rem 调用sub
hello
```







## 数组

声明简单数据

dim 名称([长度]) as 数据类型

```vb

dim bytes() as byte
dim bytes(5) as byte
```

**接受方法返回的数组时，声明的数组不能明确规定长度！！**









