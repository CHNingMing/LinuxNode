# NodeJS

## linux NodeJS环境安装

官网下载:https://nodejs.org/en/download/

Linux 二进制包:64

解压任意位置,打开bin下,node可以直接链接到/usr/bin/node

NPM 需要单独写脚本包一层:

```shell
#!/bin/bash
cd /...Node二进制目录/bin
./npm $*
## $* 获取所有参数
```

## linux   引入模块

obj require('模块名称')

## 常用套路

### 常用阻塞写法套路

```javascript
var fs = require('fs');
var data =  fs.readFileSync('文件全路径');
console.log(data.toString());
```

### 非阻塞写法套路

```
var data =  fs.readFileSync('文件全路径',function(err,data){
    console.log(data.toString());
});
```

### 大部分方法支持回调,并且回调函数是最后一个参数

### 回调函数中第一个参数是错误时错误对象



## 事件对象EventEmitter

### 声明事件对象

```javascript
var events = require('events');
EventEmitter events.EventEmitter();
var eventsEmitter = new events.EventEmitter();
```

### 绑定事件

```javascript
eventsEmitter.on('事件名称',[function | fun])
函数:匿名函数或者函数对象
```

#### 两个监听事件:

newListener			监听事件绑定

removeListener		监听事件解除

```javascript
eventsEmitter.on('newListener',function(){
    console.log('events新绑定了方法');
});
```

###  触发事件

```javascript
eventsEmitter.emit('newListener');
```

### 统计 事件 /函数 数量

listenerCount([event]);

```javascript
eventEmitter.listenerCount();
```



## 缓冲区Buffer

### 创建Buffer对象

**Buffer** Buffer.**from**(string[,encoding]);			制定字符串初始化缓冲区

**Buffer** Buffer.**from**(buffer);						制定流初始化缓冲区

**Buffer** Buffer.**from**(array);						制定数组创建缓冲区,必须保证数组是数字

**Buffer** Buffer.**alloc**(size[,fill[,encoding]]);		创建一个指定大小的缓冲区

创建一个长度为256的流:

```javasc
var buf = BUffer.alooc(256);
```

### 写入缓冲区

int write(string[,offset[,length]\[,encoding]]);

写入:hello buffer

```javascript
buf.write("Hello Buffer");
buf.write("Hello Buffer",5)
buf.write("Hello Buffer",5,5)
buf.write("Hello Buffer",5,5,'utf8')
```

### 读缓冲区数据

string toString([encoding[,start[,end]]])

```javascript
buf.toString(buf);
buf.toString(buf,5,5);
```

## 流对象Stream

相关方法:

	 finish
	
		写入完成后方法

引入fs模块

```javascript
var fs = require('fs');
var writeStream() = fs.createWriteStream('文件名称');
```

### 写入数据

```javascript
writeStream.write(string[,encoding]);
```

## 全局变量

__dirname		当前运行目录

## 模块

创建一个模块：

Hello.js

```javascript
exports.fun = ()=>{

	//....

}
var fun1 = function(){
    //....
}
exports.fun1 = fun1;
```

引用模块和调用模块方法：

```javascript
var hello = require('./Hello.js');//模块中写引入js的目录
hello.fun();//hello对象引用上方接口的exports对象
hello.fun1();
```

### Exports

外部调用对象，公开的接口

设置对外函数/对象等直接给exports赋值就可以：

```javascript
exports.fun = function(){
    //....
}
exports.name = '张三';
exports.age = 10;
```

### Model

有时候想把对象封装到模块中：

Hello.js

```javascript
function Hello(){
    var name;
    this.setName (nameVal) =>{
        name = nameVal;
    }
    this.getName () => {
        return name;
    }
}
module.exports = Hello;
```

# HTTP模块

## createServer创建一个服务

```javascript
var http = require('http');
var url = require('url');
http.createServer((request,response)=>{
    request.url		//获取访问全url
    url.parse(request.url).pathname;
}).listen(8888);
```

# URL模块

## 取参数

### 获取参数对象

参数对象 parse(req.url,true).query

### 取参数对应值：

参数对象.请求参数name

栗子：

请求路径：localhost:端口?para1=value1&param2=value2

```javascript
var url = require('url');
var http = require('http');
http.createServer(function(req,resp){
    var param = url.parse(req.url,true).query;
    console.log(param.para1);
    console.log(param.param2);
}).listen([端口号]);
```

## 取访问路径：

string parse(url).pathname 

# 函数

## 几种函数类型

首先声明一个类

```javascript
funciton ClassOBJ = (){
    // 此处为构造方法执行代码
    this.nameA = "";		//类实例属性
    this.fun1 = () => {		//实例方法
        //...
    }
}
//prototype关键字修饰创建的是实例类
ClassOBJ.prototype.funA = () => {
    //外部添加实例方法
}
ClassOBJ.funStatic = () => {
    //添加静态方法
}
```



### 类自带属性

Name: 默认为类名



# Util

## 类继承

util.inherits(子类,父类);

子类继承父类通过**prototype**对象设置的**函数/属性**

列：

```javascript
function Base(){
    this.method_2 = (){
        console.log('基础类私有方法');
    }
    this.name = "基础类私有属性";
}
function Base_A(){
    
}
Base.prototype.method1 = (){
    console.log('会被继承的方法');
}
Base.prototype.age = 18;//会被继承的属性
```

## 对象转字符串

util.inspect(object[,showHidden]\[,depth][,colors]);

object：目标对象

showHidden:显示对象隐藏信息.  bool

Depth:递归输出对象信息层数.  int

colors：醒目样式显示信息  bool

## 判断是否为数组

isArray(object)

## 正则对象校验

util.isRegExp(object)

object:如果对象是正则表达式返回true,否则false

# FS文件操作

## 取文件属性：

```javascript
var fs = require('fs');
fs.stat('文件路径',function(err,state){});
/*
	err:错误信息
	state: 文件属性
*/
```

### state

isFile()		是否是文件

isDirectory()	是否是目录

# Express

首先安装 Express:

```
cd 执行JS文件目录
npm install express --save
npm install body-parser --save
npm install cookie-parser --save
npm install multer --save

```

### Express

**get**(<请求URL,可以正则>,<Funcation(request,response)>)

**post**(<请求URL,可以正则>,<Funcation(request,response)>)



```javascript
var express = require('express');
var app = express();
//表示访问根目录时输出hello world!
app.get('/',function(req,resp){
    resp.sned('hello world!');
});
//
app.post('/user_*',(req,resp)=>{
    //...
});

//开启服务
var server = app.listen(8010,function(){
   //开启后执行代码
});

```

### 设置静态资源位置：

app.use( express.static( <静态资源路径> ) );









