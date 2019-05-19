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
mvn install:install-file -Dfile=1包文件 -DgroupId=组名称 -DartifactId=依赖名称 -Dversion=版本名称 -Dpackaging=jar
```

# Maven导出jar

## 不依赖jar项目:

pom.xml

```xml
<project>
    <!-- pom 主体 -->
    <build>
        <plugins>
            <!-- 编译环境 -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
  				<version>3.1</version>
                <configuration>
                    <target>1.7</target>
                    <source>1.7</source>
                    <!-- 编码格式 -->
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <!-- 生成jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>2.4</version>
                <configuration>
                    <archive>
                        <manifest>
                             <!-- 类入口路径,保证类中有main函数 -->
                            <mainClass>com.main.Main</mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

执行:

​	mvn clean

​	mvn package

## 依赖jar项目

```xml
<build>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.1</version>
                    <configuration>
                        <target>1.7</target>
                        <source>1.7</source>
                        <encoding>UTF-8</encoding>
                    </configuration>
                </plugin>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-jar-plugin</artifactId>
                    <version>2.4</version>
                    <configuration>
                        <archive>
                            <manifest>
                                <!-- 执行jar内指定jar目录 -->
                                <addClasspath>true</addClasspath>
                                <!-- 表示执行jar所有依赖取当前目录lib文件夹下找 -->
                                <classpathPrefix>lib/</classpathPrefix>
                                <!-- 入口类 -->
                                <mainClass>com.main.Main</mainClass>
                            </manifest>
                        </archive>
                    </configuration>
                </plugin>
                 <!-- 把maven依赖转成jar输出到指定目录插件 -->
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-dependency-plugin</artifactId>
                    <executions>
                        <execution>
                             <!-- id名称任意 -->
                            <id>copy-dep</id>
                             <!-- 以package/install执行时触发 -->
                            <phase>package</phase>
                            <goals>
                                <!-- 插件命令  -->
                                <goal>copy-dependencies</goal>
                            </goals>
                            <configuration>
                               <!-- 插件目录  --> 
                               <!-- ${project.build.directory}可通过Ctrl查看  --> <outputDirectory>${project.build.directory}/lib</outputDirectory>
                            </configuration>
                        </execution>
                    </executions>
                </plugin>

            </plugins>
    </build>
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

# maven 标签

## plugins 和 pluginManager 区别：

plugins下插件表示使用插件。

pluginManager下表示声明插件。

​	主要用在两个项目相互继承的情况下。

​	父类pluginManager声明的 插件，可以在子类中直接引用。































# maven 命令

## mvn dependency:tree

查看当前maven项目依赖树


































