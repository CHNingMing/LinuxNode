# Tomcat





## JAVA_HOME/JRE_HOME没设置错误:

直接在setclasspath.(sh/bat)中设置更新变量

### linux设置变量:

追后一行追加:

source /etc/profile

或者

export JAVA_HOME=/xxx  现场指定变量



### Tomcat 远程调试

**bin/catalina.sh**第一行添加:

```
CATALINA_OPTS="-Xdebug  -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n"
```

address=8000  代表端口号

Idea添加Remote(添加tomcat位置)

填写tomcat所在ip,debug端口

点击debug等与监听8000端口

选择断点,调试....



# Tomcat修改部署目录

/a_filezilla_file : 项目所在目录

/a_filezilla_file/userp ： 项目具体目录

## 修改localhost路径

### 编辑conf/server.xml

定位到  <Host name="localhost" appBase="webapps" unpackWARs="true" autoDeploy="true">:

#### Host

appBase： 项目所在目录

unpackWARs： 是否解压war包

autoDeploy： 表示把新的WEB项目放到appBase指定的目录时，自动载入项目

reloadable:  表示这个Host开启热部署

#### Context

path: 项目访问路径，实际访问 **<host下name>**:**<port>**\\**<Context下path>**

```xml

<Host name="localhost"  appBase="/a_filezilla_file/userp"
            unpackWARs="true" autoDeploy="true">
        <Context path="" reloadable="false" docBase="/a_filezilla_file/userp">
			<Logger className="org.apache.catalina.logger.SystemOutLogger" verbosity="4" timestamp="true"/>
		</Context>
    
</Host>
```

修改appBase,这个目录为项目所在目录。

```xml
<Host name="localhost"  appBase="/a_filezilla_file/userp" unpackWARs="true" autoDeploy="true">
```

一般配置多个项目时(列:/a_filezilla_file/userp,/a_filezilla_file/userp1,/a_filezilla_file/userp2)，这写的是多个项目共同的父级目录。因为后边的Context目录才是真正指向项目的目录。

**并且这个目录必须在Host标签appBase属性设置目录下**

```xml
<Host name="localhost"  appBase="/a_filezilla_file“ unpackWARs="true" autoDeploy="true">
```

添加一个Context标签：

```xml
<Context path="[项目路径]" reloadable="false" docBase="/a_filezilla_file/userp">
    
</Context>
```

项目路径：如果填空，则表示localhost:8080(port)/项目文件 直接访问

## 添加Host自定义路径

Host在Tomcat中代表虚拟主机。如果自定义Host，需要在主机通过hosts添加一条自定义域名记录

```xml
<Host name="www.userp.com" appBase="/a_filezilla_file">
    <Context path="[项目路径]" docBase="/a_filezilla_file/userp">
        
    </Context>
</Host>
```

### 编辑hosts:

任意位置添加一条记录：

127.0.0.1	www.userp.com

浏览器访问时为:

```http
www.userp.com:8080
```













