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



# URL

存储简单连接情况

```
URL url = new URL("http://xxx.com/xx");
```

# URI

存储复杂连接

```java
import org.apache.http.client.utils.URIBuilder;
import java.net.URL;
new URIBuilder()
	.setScheme(String)  //协议
    .setHost(String)	  //主机
    .setPath(String)	  //请求具体路径
    .setPort(int)		  //端口
    .setParameter(String key,String value)//参数
    .....
    .build();
//可任意简写
new URIBuilder("https://").setHost("www.baidu.com")
new URIBuilder("https://www.baidu.com").setPath("/xxx")
```





# 简单请求

## 请求对象

```java
CloseableHttpClient httpClient = HttpClients.createDefault();
```

## get/post

```java
HttpGet httpget = new HttpGet(URL/URI);
HttpPost httppost = new HttpPost(URL/URI);
```

## 响应对象

```java
CloseableHttpResponse response = closeableHttpClient.execute(HttpGet/HttpPost);
```



## CloseableHttpResponse

请求响应对象

### 获取响应状态码：

```java
CloseableHttpClient对象.getStatusLine().getStatusCode()
```

### 获取响应内容

```java
String EntityUtils.toString(CloseableHttpClient对象.getEntity())
```

















