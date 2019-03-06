# JS

#### iframe窗口调用父窗口方法

	parent.windw.父窗口定义的方法(args[] ...);

#### 在方法体中获取调用参数：

​	**arguments**对象，可以直接获取当前调用方法参数

#### JS多层div 点击事件冲突，点击时同时触发多个解决

​	event.stopPropagation(); 

#### JS JSON转字符串

​	JSON.stringify(jsonobj)；

取DOM父级元素：

​	DOM对象.parentNode

#### JS 替换所有字符串

​	var reg = new RegExp('被替换'**,'g'**);

​	xx_str.replect(reg,'替换内容');

#### JS特殊情况下获取样式值:

window.getComputedStyle(Ele).样式名称



### 动态创建DOM

```javascript
var script = document.createElement('script');
script.type = 'text/javascript';
script.src = 'xxx.js';

document.head.append(script);

```

### 动态删除DOM

```javascript
var script = document.createElement('script');
//设置script属性
//head中添加了script
document.head.removeNode(script);

```

### 代码设置断点:

```javascript
//。。
debugger;
//..
```





# JQuery

### 万恶之源:

-- 异步开启关闭

$.ajaxSettings.async = true;

DOM元素设置disabled后，**onclick失效**

### 给JQuery对象注册方法：

$.fn. 方法名称 = function([args...]){ this表示当前对象 }

### load(url,date)

$('').load(url,date)

#### 问题:load没效果(网络没请求)

load时,必须保证$("")可以查询出JQuery对象,如果没有load内部不会调请求

