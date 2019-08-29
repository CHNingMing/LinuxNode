看云：<https://www.kancloud.cn/sogouwap/amxx>

## 系统函数

# plugint_init

所有函数注册都在这个代码块中。

```
public plugint_init{
	//
}
```



## register_plugin

注册插件

```
public plugin_init()
{
     register_plugin("插件名", "插件版本号", "插件作者名")
}
```

## client_print

打印信息

```
client_print(id, print_chat, "这是一些信息",信息中对应占位符值)
```

id : 要输出的玩家id，如果为0是全部玩家

print_chat : 输出玩家方向

## register_clcmd

输入指定指令调用方法。

```
register_clcmd("say /abc", "thefunc")

//当前人id
public thefunc(id){

}
```

表示按y输入   /abc   调用thefunc方法

## 常用函数

copy(target,len,source)



# 各种变量命名：

int

默认为int

```
new a,b,c
a = 1
```

数组

a数组

```
new a[30]
new a[30] = {1,2,3,4}
```

字符串

name 字符串

```
new name[] = "ZhangSan"
```

浮点型

```
new float:money = 0.0
new float:moneys[32] = {0.0,1.0,2.0}
```



#### 全局变量

```
#define version = "1.2.0"
```





















