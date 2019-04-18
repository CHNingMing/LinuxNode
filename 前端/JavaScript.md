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

#### JS取DOM实际宽度

dom.offsetHeight

dom.offsetWidth

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

##  JS声明选择器

```javascript

//声明类似JQuery选择器类型
var $ = queryAll = document.querySelectorAll.bind(document);
//同理
var byId = document.getElementById.bind(document);
var fromClass = document.getElementsByClassName.bind(document);
var fromTag = document.getElementsByTagName.bind(document);

```



## 浏览器

### JS取浏览器滚动条位置

```

document.documentElement.scrollTop

```

### 滚动条禁用 PC端

```javascript
document.documentElement.style.overflowY = 'hidden'; 		//禁用滚动条并隐藏
document.documentElement.style.overflowY = 'scroll'; 		//显示滚东条
```

### 滚动条禁用 移动端

**通过touchmove事件配合传入事件对象的preventDefault()方法实现。**

**注意：调用preventDefault方法时，不能将时间触发在html/body中，只能是普通dom中。否则chrome会忽略preventDefault方法，达不到禁用滚动条效果。也会发出提示：**

**Unable to preventDefault inside passive event listener due to target being treated as passive. See** 

```javascript

dom.addEventListener('touchmove',function(even){
    even.preventDefault();
},false);

```

#### preventDefault()

通知浏览器取消事件默认动作。不执行触发元素事件默认动作。阻止事件要触发的动作。

通过触发事件时，传入的事件对象方法。

## 移动端事件

 touchstart  触摸时

​	even_start.touches[0].clientX/clientY		取触摸坐标

touchend	触摸离开时

​	event_end.changedTouches.clientY/clientX

touchmove	触摸移动时











# JQuery

### 异步请求同步:

-- 异步开启关闭

$.ajaxSettings.async = true;

DOM元素设置disabled后，**onclick失效**

### 给JQuery对象注册方法：

$.fn. 方法名称 = function([args...]){ this表示当前对象 }

### load(url,date)

$('').load(url,date)

#### 问题:load没效果(网络没请求)

load时,必须保证$("")可以查询出JQuery对象,如果没有load内部不会调请求

