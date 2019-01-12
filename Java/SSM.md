# SSM

## Sping整合SpringMVC

导入依赖:

	spring基本包(context,beans)

	spring-web、spring-webmvc

配置web.xml

	初始化spring参数:

		context-param:指定spring配置文件

	加载Spring监听器

		ContextLoaderListener

	配置SpringMVC的Servlet入口:

		DispatcherServlet

			配置init-param参数

			配置load-on-startup

	创建Spring配置文件

		注解扫描

		SpringMVC三大件

	创建类,声明Controller注解,方法上添加RequestMapping等注解,

		**方法返回参数一定是ModelAndVIew,如果是Sring需要在控制台查看有没访问成功!**