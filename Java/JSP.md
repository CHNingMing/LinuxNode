

# C标签：

	C标签:
	<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
	fn标签:
	<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions"%>



## c:if 配合 EL 表达式判断

```xml
<c:if test="${param.参数 逻辑运算符 值}">
    显示内容
</c:if>
```

切记～～！！！！！test="JSTL表达式外千万不要有**空格**"

## c:forEach

```xml

<c:forEach item="list集合" var="循环每个元素变量名" step="每次循环步长,跳着循环" begin="开始位置" end="结束位置" varStatus="每次迭代信息" >
    
</c:forEach>

```





​	

​	

# EL表达式

## 获取参数：

	${param.参数名}

## 获取参数顺序：

pageContext

request

session

application

## 获取指定域：

#### 获取Session

	${sessionScope.xxx}





# Servlet 源码下载

http://archive.apache.org/dist/tomcat/tomcat-7/v7.0.28/src/



# 执行Java代码

## 保证Java有返回值

<%= java代码 %>

## 没有返回值

<% java代码 %>