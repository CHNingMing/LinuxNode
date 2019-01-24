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

## 流对象Buffer

