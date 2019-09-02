# C存储类

## auto 存储类

所有局部变量默认的存储类。auto只能修饰局部变量。

```c
int home;
//等同于
auto int home;
```

## register 存储类

告诉编译器，把register 声明变量存储到寄存器中。

寄存器比内存读写速度更快，但是没有内存地址。

也就意味着不能通过 &变量名 取内存地址。

### 菜鸟教程：

```
定义 'register' 并不意味着变量将被存储在寄存器中，它意味着变量可能存储在寄存器中，这取决于硬件和实现的限制。
```

## static 存储类

 静态变量，重复使用类/函数时定义的静态变量只会创建一次。

static可以声明在函数内部或者类内部。

``` c

void test1(void){
    static int num = 0;
    num ++;
}
//执行多个test1时，num会每次+1
class a{
    static int num_c = 0;
}
```

## extern存储类

通过extern可以引入其他.c文件中个别 函数/变量 使用。

**变量不能是静态(static)修饰变量。**

引入时，保证函数返回值，一致。

main.c

```c
#include <stdio.h>
int num_s = 0;
//引入support.c函数
extern void write(void);
void main(int arg,char *args[]){
    write();
    printf("%d",num_s);
    return 0;
}
```

support.c

```c
#include <stdio.h>
//引入main.c内变量
//变量名必须一致
extern int num_s;
void write(void){
    num_s = 99;
}
```

# C枚举

### 定义枚举：

```CQL
enum 枚举名 {枚举属性,...}
```

默认枚举属性值以0开始，后续属性在上一个属性基础上+1.

所以枚举值都是int类型

### 使用枚举:

```c
enum Day{
    MON=1,TUE,WED,THU,FRI,SAT,SUN
}
int main(void){
    //声明枚举类型
    enum Day day;
    //设置类型值
    day = MON;
    printf("%d");
    return 0;
}

```

























