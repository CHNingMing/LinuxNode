# VS C++ 连接MySql

## 设置头包含和库:

项目 - 属性 - VC++ 目录 

- 包含目录 添加mysql include下目录

- 库目录     添加mysql lib下目录

## 添加libmysql.lib依赖

项目 - 属性 - 链接器 - 输入 - 附加依赖项 - 手动输入  libmysql.lib (这个名字根据上边选择的 lib目录下来的,lib目录下有libmysql.lib)

把mysql lib目录下的libmysql.dll文件复制到项目中(项目运行时会用到),和cpp文件放同一目录。



猜测libmysql.lib文件中指定了libmysql.dl，所以VS编译的时候会通过libmysq.lib中指定的libmysql.dll和可执行文件放在一起。

