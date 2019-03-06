## CMakeLists文件

项目配置信息描述

### 添加自定义头文件路径

```
include_directories(头文件路径，不用上引号修饰)
```

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

