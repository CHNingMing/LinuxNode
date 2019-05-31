# DispatchServlet

整个访问过程的控制



# Handler

SpringMVC的处理器.处理各种请求



# HandlerMapping

处理器映射器,根据URL找到对应的处理器(Handler),返回Handler执行链

查找Handler:

​	通过XML方式

​	通过注解RequetMapping方式

SpringMVC可以同时匹配多个映射器

总结:映射器配访问URL的方式,有通过bean的name,bean的id,RequestMapping

# HandlerAdapter

处理器适配器,执行指定处理器,返回ViewAndModel对象

在执行Handler时,HandlerAdapter指定了一系列规则,必须保证传入的Handler符合这些规则才会执行.

规则 : spring中的bean必须实现Controller接口(SimpleControllerHandlerAdapter) 或者 HttpRequestHandler 接口(HttpRequestHandlerAdapter)

# ViewResolver

把ModelAndView 根据视图名称解析对应的视图,返回给DispatchServlet



# SpringMVC配置

## WEB.xml配置

```xml
  <servlet>
    <servlet-name>springmvc</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:applicationContext.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>springmvc</servlet-name>
    <url-pattern>/*</url-pattern>
  </servlet-mapping>
```

默认取Web-Info下找到[DispatcherServlet所在标签的servlet-name名称]-servlet.xml(springmvc-servlet.xml)

## Servlet-pattern

配置路径方式:

第一种:    *.action		所有请求以.action结尾

第二种:	/				所有请求,都由springmvc控制(包括配置文件)

第三种: /*				

## --非注解配置--

## 配置处理器映射器

所有的处理器映射器,都实现了 HandlerMapping接口

### BeanNameUrlHandlerMapping

```xml
<bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"></bean>
```

BeanNameUrlHandlerMapping,这个映射器根据 控制层处理器 bean的名称当访问url.

查找spring容器中,所有实现了Controller接口的bean.在拿这些bean的名称当访问的路径.

Controller : **org.springframework.web.servlet.mvc.Controller**

#### 创建一个类,继承Controller:

这个Controller就是一个Handler,控制层处理器.

```java
package com.controller;

import org.springframework.web.servlet.HandlerAdapter;
import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.Controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class IndexController implements Controller {

    public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {

        List<Map<String,Object>> list = new ArrayList<Map<String,Object>>();
        Map<String,Object> map1 = new HashMap<String, Object>();
        map1.put("name","zhangsan");
        map1.put("age",19);
        Map<String,Object> map2 = new HashMap<String, Object>();
        map2.put("name","lisi");
        map2.put("age",21);
        list.add(map1);
        list.add(map2);
        ModelAndView modelAndView = new ModelAndView();
        //添加对象
        modelAndView.addObject("list",list);
        //指向到JSP页面
        modelAndView.setViewName("WEB-INF/view/index.jsp");
        return modelAndView;
    }
}
```

ModelAndView,用法类似Model,也是给JSP中添加对象用的(addObject(name,value)).

除了可以添加对象,还可以指定JSP视图.(modelAndView.setViewName(pageName))

最后返回ModelAndView

## SimpleUrlHandlerMapping

通过id匹配URL

```xml
<bean id="indexController" name="/getList" class="com.controller.IndexController"></bean>
<bean id="items" name="/getItems" class="com.controller.Items"></bean>

<bean class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
    <property name="mappings">
        <props>
            <prop key="/getList_s">indexController</prop>
            <prop key="/items_s">items</prop>
        </props>
    </property>
</bean>
```

```xml
<prop key="/getList_s">indexController</prop>
```

key为访问URL,值为继承Controller类Bean的id





## 配置处理器适配器

### SimpleControllerHandlerAdapter

所有的处理器适配器,都实现了HandlerAdapter接口

```xml
<bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"></bean>
```

主要执行实现Controller接口下的handleRequest方法.并返回一个ModelAndView.

多个访问时,每个访问编写一个类,继承Controller

### HttpRequestHandlerAdapter

```xml
<bean class="org.springframework.web.servlet.mvc.HttpRequestHandlerAdapter"></bean>
```

规定类必须实现HttpRequestHandler

```java

public class IndexController_http implements HttpRequestHandler {

    public void handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws ServletException, IOException {

        List<Map<String,Object>> list = new ArrayList<Map<String,Object>>();
        Map<String,Object> map1 = new HashMap<String, Object>();
        map1.put("name","zhangsan");
        map1.put("age",19);
        Map<String,Object> map2 = new HashMap<String, Object>();
        map2.put("name","lisi");
        map2.put("age",21);
        list.add(map1);
        list.add(map2);
        //添加到属性
        httpServletRequest.setAttribute("list",list);
        //指向到JSP页面
        httpServletRequest.getRequestDispatcher("/WEB-INF/view/index.jsp").forward(httpServletRequest,httpServletResponse);
    }
}
```

一般用这个方法不用在打开页面,用在返回json数据中.



## 配置视图解析器

```xml
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
```

InternalResourceViewResolver 这个类默认解析JSP时支持JSTL表达式

## --非注解配置 END--

## SpringMVC映射器,适配器默认配置

springwebmvc 包下:org/springframework/web/servlet/DispatcherServlet.properties

这个文件中配置了如果映射器/适配器 没有配置的话,默认使用的映射器

必须是一个映射器/适配器也没配置时.

```properties
# 映射器默认配置
org.springframework.web.servlet.HandlerMapping=org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping,\
	org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping
# 适配器默认配置
org.springframework.web.servlet.HandlerAdapter=org.springframework.web.servlet.mvc.HttpRequestHandlerAdapter,\
	org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter,\
	org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter
```

### HandlerMapping

spring 3.1之前使用:org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping

spring 3.1 之后使用:org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping

### HandlerAdapter

spring 3.1之前使用:org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter

spring 3.1 之后使用:org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter



## --注解配置--

### 配置映射器和适配器的注解驱动:

```xml
<mvc:annotation-driven />
```

默认这个标签中已经配置了json转换解析器

设置这个标签后,spring启动时会扫描bean中带有@Controller注解的类.

### 控制层扫描包:

```xml
<context:component-scan base-package="controll所在包"></context:component-scan>
```

设置了扫描包就不用把每个bean单独配置了.















