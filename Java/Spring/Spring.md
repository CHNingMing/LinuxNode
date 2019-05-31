# Web.xml配置

```xml
  <listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  </listener>
  <!-- Spring配置 -->
  <context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:spring配置文件路径</param-value>
  </context-param>
```

如果没有.找不到这个配置,会自动去项目根目录找applicationContext.xml配置.如果找不到就报错.











