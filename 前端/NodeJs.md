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
var data =  readFileSync('文件全路径');
console.log(data.toString());
```

### 非阻塞写法套路

```
var data =  readFileSync('文件全路径',function(err,data){
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

