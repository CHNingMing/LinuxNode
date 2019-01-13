

## GTK环境部署：

#### 安装code:blockIDE

创建项目时选择:GTK+

右键左侧项目列表，选择Build Options  - > Debug/Release  

​					-> Compiler settings -> Other compiler Options:

​					-> Linker settings - > Other linker options:

添加：

```
`pkg-config --libs --cflags gtk+-3.0`
```

​					

​					

#### 安装：libgtk-3-dev

```
gcc C源文件.c -o [执行文件名称] `pkg-config --cflags --libs gtk+-3.0`
```







