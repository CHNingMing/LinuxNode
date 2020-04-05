

# MySql C

环境:MinGW

## 环境

官网下载mysql api.

mysql-connector-c-6.1.11-win32		根据编译环境/运行环境 				 [待确定]

解压，主要用到文件中include 和 lib 文件夹内容，复制到项目位置。

include: 程序中引入头

lib: 用到libmysql库，但是mysql 没有提供gcc的.a类型，只提供了 .lib类型的，这是vs可以直接用的。

​	需要把.lib 文件转换成 .a文件，不能直接把lib转成.a，需要先用reimp把.lib 转成 .def,在用dlltool把def转成.a\

​	下载MinGW工具包，主要用reimp工具，这是单文件程序。

### 转换成del

把reimp和libmysql.lib放一起，cmd执行：

```cmd
reimp -d libmysql.lib
```

执行后生成libmysql.def

### 编辑libmysql.def: 

```
mysql_init	`mysql_init@4
mysql_real_connect	mysql_real_connect@32
mysql_real_query	mysql_real_query@12
```

### dlltool生成.a

```
dlltool -k -d libmysql.def -l libmysql.a
```

## 配置

配置cmake:

```cmake
...
include_directories("include文件夹(当前路径/绝对路径)")
add_executable(${PROJECT_NAME} main.cpp)
target_link_libraries(${PROJECT_NAME} E:\\dev\\CWork\\CADD_MYSQL_DEMO\\lib\\libmysql.a)
...
```

E:\\dev\\CWork\\CADD_MYSQL_DEMO\\lib\\libmysql.a 是.a绝对路径,项目当前路径还不行.....[待解决]





