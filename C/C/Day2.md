### 生成随机数:

### srand()

初始化rand()函数生成随机数

### rand()

生成随机数,生成0～RAND_MAX范围随机数。

#### RAND_MAX:

stdlib中声明，主要用来定义随机数生成的最大值

### goto

​	goto 标记名;

​	运行时跳转指定标记名位置运行

```c

//...

goto t_flag;
//...


t_flag:			//注意标记位最好是冒号



//...


```

### 二维数组：

求二维数组实际大小:    数组行\*列\*数组类型大小

二维数组实际上是一个连续的以为数组,把二维数组的所有元素连起来

首元素地址

首行地址

数组地址

#### 二维数组特殊定义方式:

数据类型 name\[num]\[num] = {{1,2,3},{4,5,6}}

数据类型 name[num]\[num] = { 1,2,3,4,5,6 }

数据类型 name []\[num] = { 1,2,3,4,5,6 }

## 传递数组给函数三种方式

### 指针传递:

```c
void myfun(int param){
    //...
}
```

### 已知数组大小:

```c
void myfun(int param[10]){
    //...
}
```

### 位置数组大小:

```c
void myfun(int param[]){
    //...
}
```









### 字符串:

声明字符串:

char * name = "";

字符串全部以 **/0** 结束 ,/0 = 数字0,但不等与'0'，因为'0'在ascii中,字符 0 对应ascii值为48

c语言没有字符串数据类型，通过char数组代替

### Print

#### 占位符限定字符串个数:

%[num]s

```
printf("%9s");
```

打印9个字符

#### PS:%s占位符读字符时读到\0结束字符串

C89下for报:

```c
‘for’ loop initial declarations are only allowed in C99 or C11 mode
```

#### 打印变量地址符:%x

```c
int num = 9;
printf("%x",&num);
```













