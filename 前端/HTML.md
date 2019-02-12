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







 













# 

