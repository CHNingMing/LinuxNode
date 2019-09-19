## 手动创建CMake文件

```
cmake_minimum_required(VERSION 3.7)
project(<项目名称>)
set(CMAKE_C_STANDARD 99)C标准
set(SOURCE_FILES ConsoleApplication1/main.c)源文件
add_executable(<项目名称> ${SOURCE_FILES})添加到执行文件
```

