[TOC]

## Content-Type：

Content-Type是响应到客户端时告诉浏览器响应内容以哪种方式解析。

### enctype：

指定请求类型

### 请求类型：

#### x-www-form-urlencoded

form get提交时方式

```json
name=value1&age=18&sex=man...
```

#### multipart/form-data

将数据转成二进制类型

#### Text/plain

纯文本传输，空格转换成+号

## 判断解析浏览器

根据加载不同css/js兼容ie

### 除IE外其他浏览器情况：

```html
<!--[if !IE]><!--> 除IE外都可识别 <!--<![endif]-->
```

### 所有IE可以识别：

```html
<!--[if IE]> 所有的IE可识别 <![endif]-->
```



## 跨域请求:

### 服务端响应时设置允许服务端访问的请求头	[推荐]

//正常异步请求

服务端响应数据时除了Content-Type外，添加

```
Access-Control-Allow-Origin: *
```

*表示所有网站允许异步访问

也可以是：

```
Access-Control-Allow-Origin: https:\\www.baidu.com
```

指定网站允许访问

注意:

​	如果网站所在域名是https，请求目标的域名是http，就算服务端响应时设置响应头允许访问也会被拦截,因为https网站必须保证所有跨域异步请求必须是https的。



#### 理解：

个人认为发送请求后实际服务端返回数据了，只不过返回数据后被浏览器拦截了

拦截时先验证属不属于同一个源,域名:端口相同

如果不同时报错

### jsonp方式跨域	[不推荐]

通过\<script>可以请求任何网站资源实现

动态加载script取跨域请求资源,返回一个js脚本，这个js脚本在调用本地方法,传入响应数据

整体步骤:

#### 声明一个方法作为请求回调

#### 请求资源：

​	js动态在head中添加\<script>

#### 响应内容格式为js脚本格式:

​	设置Content-Type为：Content-Type:application/x-javascript

​	响应内容格式:

​		声明方法名({响应json数据})

​	内容格式其实是调用上方声明方法

#### 例子:

 index.html

```html
//...
<head>
    <script type="text/javascript" src='index.js'></script>
    <script>
        onRequest('http://www.xxx.com/xx/xxx',(data)=>{
            console.log('接受数据...');
            console.log(data);
        });
    </script>
    
</head>

//...

```

跨域请求

http://www.xxx.com/xx/xxx访问响应数据格式:

​	设置响应头:Content-Type:application/x-javascript		表示返回一个js脚本

​	内容：

​			onResponse( {name:'zhangsan',age:18} )

index.js

```javascript

var result_data = null;
function onRequest(url,fun){
   	//创建临时script
    var script = document.createElement('script');
    script.id = 't_script';
    script.src = url;//跨域请求数据链接
    script.type = 'text/javascript';
    document.head.append(script);
    fun(result_data);
}
//声明接受响应数据方法
function onResponse(data){
    //删除临时script
    //...
    //设置接受数据
    result_data = data;
}
```



## 自定义网站图标

```html
  <link rel="icon" href="publicizinggoods/favicon.png" type="image/x-icon" />
  <link rel="shortcut icon" href="publicizinggoods/favicon.png" type="image/x-icon" />
```

publicizinggoods/favicon.png	: 基于当前站点图标







