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





