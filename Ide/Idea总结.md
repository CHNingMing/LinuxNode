项目相关

## 项目相关

#### 单元测试

	File-Project Structure-选择Modules-选中当前项目-选择Dependencies下-点击+Jar as directories+IDEA自带了JUnit-*.jar   和  hamcrest-core-*.jar,引入这两个文件

#### 自动创建Web-INF文件夹和webapp

保证pom文件中  packaging 为 war

打开结构 == > Facets ==> +号，添加web.xml

在把项目下的WEB-INF移动到webapp下

## idea tomcat Web部署没有Updae classes and resources项

主要是因为选择的Artifact有关，Artifact后没带exploded，会没有，

重新创建Artifact,选择 **Web Application Artifact**



## IDEA Output Layout设置:

添加在　**Facets**　设置Web资源目录,上框定位web.xml,下框定位部署到tomcat下项目根目录文件(webInfo/webroot)

回到Output Layout设置

Output root		是部署项目后输出文件

#### Available Elements

下是　java编译文件放置位置(一般都是classes下)　和个别lib包

部署好后，在每次运行时会把一下资源文件部署到资源文件中

## 插件

linux 插件目录 ~/.IntelliJIdea2018.2/config/plugin

### 快捷键

#### 创建类

Ctrl+Shift+T		创建测试

Ctrl+H			查看类继承关系

Ctrl+Shift+N		查询class文件,查找框架类挺准

F9				切换运行项目

#### 代码显示

Ctrl+Q				查看方法详情

Ctrl+J				查看详细信息

Ctrl+O				查看当前文件方法

#### 搜索

Ctrl+Shift+F 全局搜索文本

Ctrl+F		局部搜索

Ctrl+Shift+R	全局搜索文本，替换

Ctrl+R		局部替换

Ctrl+N		全局搜索文件

Ctrl+Alt+B	 通过接口查找实现类

#### 编辑器操作

Ctrl+Y	删除一行

折叠\展开当前标签：Ctrl+-、Ctrl+=

折叠所有\展开所有标签：Ctrl+Shift+-、Ctrl+Shift+=

#### Debug

Alt+F8	运行选中的代码/动态执行代码

Ctrl+Shift+F8	查看所有断点

Ctrl+F8 			设置断点

Shift + F8 		跳出函数 

# 问题总结

###  idea 包重叠显示/简写

点击齿轮

Flatten Packes		同名包重叠

Hiden Empty Middle Packes

### idea 点击文件自动打开 关闭

点击齿轮

Autoscroll to Source		去掉对勾

### 提示javax.servlet.http没有找到相关类错误

### 打开项目管理工具 -- 	Dependencies -- Tomcat x.x.x   > 编辑(右边小铅笔)  > 加号  选择tomcat\lib\servlet-api.jar	


### idea去掉编辑器白线条

设置中搜索 - > Show right margin![1544578103651](/root/.config/Typora/typora-user-images/1544578103651.png)

Show right margin (configured in Code Style options)

### idea 不能创建Classs类：

主要原因是因为创建文件时，会通过对应模板创建，如果没有模板会报错。

打开设置 - > Editer -> File and Code Templates -> Class 添加代码：

```java
#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
#parse("File Header.java")


public class ${NAME} {
    
}
```

# 调试

循环中添加条件，满足条件断点调试。

右击红色断点，Condition 下输入条件。

例如输入:

i == 200

点击Done。

i 为 200 时断点调试。