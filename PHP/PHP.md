# PHP

## 变量

### 声明变量:

```php
[global/static] $变量名称=值
//在方法体内访问方法体外变量时使用global
global $变量;
//每个函数执行完后都会删除函数内所有变量,如果想让某个变量不删除static修饰
static $变量;
```

### 全局变量

$GLOBALS[<全局变量名>]=值

## echo

输出制定字符串

echo "字符串中可以直接套变量$变量名"

## print

print和echo功能类似,只不过有返回值,返回值总为1,并且效率没有echo 高

## 集合/数组类型

### array

集合对象 array(obj...)

#### 访问元素

```php
$arr = array("","","");
echo "字符串中访问$arr[0]"
//不要单独输出arr,会报不能将Array转成string
```

### var_dump($obj)

输出对象详细信息



# mysqli

## 普通查询

mysqli_query(conn(连接对象),query(sql),resultmode(可选,模式));

resultmode:

- MYSQLI_USE_RESULT（如果需要检索大量数据，请使用这个）
- MYSQLI_STORE_RESULT（默认）

## mysqli_result对象

针对成功的 SELECT、SHOW、DESCRIBE 或 EXPLAIN 查询，将返回一个 mysqli_result 对象。针对其他成功的查询，将返回 TRUE。如果失败，则返回 FALSE。				-- 菜鸟教程

### fetch_all取出结果集所有对象

```
$result->fetch_all()
```

### fetch_assoc取出一行结果

```
$result->fetch_assoc()
```

# $_Get

### $_Get出现提示信息：Notice: Undefined index:

原因是因为有NULL的对象,判断是否为NULL也不行

```
//假设没有这个参数(null)
if( $_GET['fun_name'] != null ){		//照样还是会提示错误,不影响正常运行
    
}
$_GET['fun_name'] != null		改成			isset($_GET['fun_name']);

```

