# WebService

百度：

```
Web service是一个平台独立的，低耦合的，自包含的、基于可编程的web的应用程序，可使用开放的XML（标准通用标记语言下的一个子集）标准来描述、发布、发现、协调和配置这些应用程序，用于开发分布式的互操作的应用程序。
```

### 两种风格：

#### 提供两种服务

	(JAX-)RS服务

	传输 XML 格式和 JSON 格式，基于HTTP协议

	(JAX-)WS服务

	传输 XML 格式，基于SOAP协议

#### jetty

WebService可以运行在两种容器中，一种是**Jetty**,一种是**Tomcat**

```
cxf-rt-transports-http-jetty
```

#### 访问服务全路径

ip地址 => 端口 => 项目名 => web.xml定义名称 => 类注解定义名称 => 方法注解定义名称

#### 访问请求

```
Post 请求方式访问，保存操作；
Put 请求方式访问 修改操作；
Get请求访问 查询操作
直接访问资源：查询所有信息
在资源后边添加(一层路径)，代表参数
添加参数访问资源：查询特性信息
Delete 请求方式访问，删除操作
```



### 步骤：

#### 创建服务端：

导入依赖：

```xml
      
      <dependency>
            <groupId>org.apache.cxf</groupId>
          	<!-- jaxrs就是Restful -->
            <artifactId>cxf-rt-frontend-jaxrs</artifactId>
            <version>3.1.1</version>
        </dependency>
        <dependency>
            <groupId>org.apache.cxf</groupId>
            <artifactId>cxf-rt-transports-http</artifactId>
            <version>3.1.1</version>
        </dependency>
        <dependency>
            <groupId>org.apache.cxf</groupId>
            <artifactId>cxf-rt-wsdl</artifactId>
            <version>3.1.1</version>
        </dependency>

```

#### 配置web.xml

```xml
   <servlet>
        <servlet-name>cxfServlet</servlet-name>
        <servlet-class>org.apache.cxf.transport.servlet.CXFServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>cxfServlet</servlet-name>
        <url-pattern>/rest/*</url-pattern>
    </servlet-mapping>
```

#### 创建服务通信接口

```java
@WebService
public interface BookInfoService {
    @WebMethod
    public BookInfo getBook();

    @WebMethod
    public BookInfo getBookById(String id);

    @WebMethod
    public BookInfo getBookByObjBook(BookInfo bookInfo);

    @WebMethod
    public List<BookInfo> getBookAll();

}
```

#### 创建通信实体类

想返回什么参数自己创建吧

#### 创建通信接口实现类

```java
[] : 可选注解

类上定义注解：
    [
		@@Path("/定义路径")	
		@Produces("text/xml")传输格式
    ]
	@WebService(endpointInterface = "实现接口路径" , name = "服务名称")
方法上注解：
	@GET
    @Path("/访问路径")
    @Produces({支持的传输格式})
    	Produces:表示这个方法有返回值，支持的返回类型		推荐使用MediaType枚举
    @Consumes({支持的传输格式})
       	Consumes:表示这个方法有参数，支持的接收参数类型		推荐使用MediaType枚举
```

#### 创建客户端

创建接收实体类

xxx

主要通过WebClient请求服务路径

WebClient WebClient.create("请求路径")		// 设置请求路径

WebClient WebClient.accept(接收参数类型MediaType枚举选择)



T	WebClient.get(某实体类.class);			//设置返回实体类		单个对象情况

List<T> WebClient.getCollection(某实体类.class);	//设置返回实体类		多个对象情况









