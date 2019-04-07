# HttpCore





# HttpClient

## 整体步骤:

```
1. 创建请求对象
2. 请求Server端
3. 返回相应(HttpResponse)
```



基于HttpCore

HttpGet

HttpPost



## 短连接/长连接:

### 短连接:

表示客户端只向服务端请求一次情况

### 长连接:

客户端向服务端请求多次的情况使用

服务端可以设置一个请求时间,如果在指定时间内没请求,断开连接

客户端也可以主动断开连接







# HttpParams

请求参数

HttpGet/HttpPost 都有setParams(HttpParams)方法





# HttpResponse

Http reposne对象内容包括：使用协议版本、Http 状态码、文本内容

# 



















