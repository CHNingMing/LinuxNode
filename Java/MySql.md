## 查询数据库表大小

select * from information_schema.tables;

table_schema : 数据库名称 

DATA_LENGTH： 表大小

## information_schema表

**columns**表：这个表存储了所有表中的表字段信息。

**tables**表：这个表里存储了所有数据库中的表的信息，包括每个表有多少个列等信息。

**schemata**表：这个表里面主要是存储在mysql中的所有的数据库的信息

