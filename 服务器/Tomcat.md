# Tomcat





## JAVA_HOME/JRE_HOME没设置错误:

直接在setclasspath.(sh/bat)中设置更新变量

### linux设置变量:

追后一行追加:

source 刷新

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









