## CMakeLists文件

项目配置信息描述

CmakeLists 命令参数不用添加引号修饰

### 设置最低CMake版本

```
cmake_minimum_required(VERSION 2.8)
```

VERSION 2.8： 指定版本号

指定项目名称，一般和项目文件夹对应

```
project(qt_gtk_hello)
```

qt_gtk_hello:项目名称

### 添加自定义头文件路径

```
include_directories(头文件路径，不用上引号修饰)
```

### 编译文件:

```
add_executable(编译后文件 源文件)
```

编译后文件：编译后文件名称

源文件：源文件名称，可以有多个，每个按空格分开



## 安装CMake

```
下载：https://cmake.org/download/
```

解压后执行./bootstrap

执行make

执行make install



### CMake GTK

CMakeLists.txt

```
find_package (PkgConfig REQUIRED)
pkg_check_modules (GTK3 REQUIRED gtk+-3.0)
set(CMAKE_C_STANDARD 11)
include_directories (${GTK3_INCLUDE_DIRS})
link_directories (${GTK3_LIBRARY_DIRS})
set(SOURCE_FILES main.c)
add_executable(wibus ${SOURCE_FILES})
add_definitions (${GTK3_CFLAGS_OTHER})
target_link_libraries (wibus ${GTK3_LIBRARIES})

```

