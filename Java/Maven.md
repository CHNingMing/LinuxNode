# MavenProfile

主要目的是为了把项目分成开发环境和部署环境

把项目分成**开发环境**和**部署环境**两部分

通过*.properties区分,maven通过打包时指定参数来选择那个***.propertie文件

### 步骤:

#### 在resource下分别创建开发环境文件夹和部署环境文件夹

#### 把项目开发环境配置文件和部署环境配置文件放在各自的文件夹下

#### pom中配置配置文件目录

```xml
<profiles>
	<profile>
        <!-- 环境唯一标识 -->
		<id>dev</id>
        <!-- 替换的内容 -->
        <properties>
            <!-- dev:开发环境配置文件夹 -->
            <env>dev</env>
        </properties>
        <!-- 如果不指定固定的profile,就是用当前这个profiles配置 -->
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
	</profile>
    <profile>
        <!-- profile可以写多个 -->
    </profile>
</profiles>
```

#### pom配置加载配置目录

```xml
<build>
    	......
    <!-- 配置节点名称 -->
	    <finalName>develop</finalName>
        <resources>
            <resource>
                <!-- 主资源目录 -->
                <!-- env:profiles下的自定义标签 -->
                <directory>src/main/resources/${env}</directory>
            </resource>
        </resources>

</build>
```

# Maven安装本地jar

```
mvn install:install-file -Dfile=jar包文件 -DgroupId=组名称 -DartifactId=依赖名称 -Dversion=版本名称 -Dpackaging=jar
```

# Maven跳过测试

### 两种跳过测试方法：

	mvn package 
	
		-DskipTests，不执行测试用例，但编译测试用例类生成相应的class文件至target/test-classes下。
	
		-Dmaven.test.skip=true，不执行测试用例，也不编译测试用例类。

# Maven两种管理统一依赖方法

1. ## 定义版本号变量
   ```xml
   <properties>
       <spring-framework-version>4.3.7.REALEASE</spring-framework-version>
       <!-- spring-framework-version:自定义版本号变量,引用时${版本号变量名} -->
   </properties>
   ```

2. ## 使用Maven自带的dependencyManagement管理

   聚合工程定义,项目可以直接声明依赖不用设置版本号

   ```
   <dependencyManagement>
     <dependencies>
       <dependency>
         <groupId>xx</groupId>
         <artifactId>xxxx</artifactId>
         <version>0.0.0.0</version>
       </dependency>
     </dependencies>
   </dependencyManagement>
   ```

   # 常用命令

   compile编译



# 错误总结：

## pom文件出错：

expected START_TAG or END_TAG not TEXT (position: TEXT seen ...**错误信息**... @334:6)  @ /opt/JavaWork/b2bweb/pom.xml, line 错误附近行, column 列

例如：

```
expected START_TAG or END_TAG not TEXT (position: TEXT seen ...
</configuration>s\r\n\t\t\t</
... @334:6)  @ /opt/JavaWork/b2bweb/pom.xml, 
line 334
,
column 6
```










