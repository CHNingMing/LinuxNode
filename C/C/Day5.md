## 随机数

通过rand()函数配合srand()函数实现随机数

生成随机数

### srand(time_t)

### rand();

# time.h

## time_t类型

所在包<time.h>

### srand(time_t);初始化随机数

### time(NULL)	获取当前时间秒值

## 实例

```c
include <stdio.h>
include <time.h>
int main(void){
	srand(time(NULL));
	rand();
}


```



## 









