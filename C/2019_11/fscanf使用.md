## fscanf

按指定内容格式读取文件内容。

函数原型:int fscanf (FILE *file, const char formatStr, ...)

file: 文件流，fopen获取

formatStr: 格式化字符串,...对应格式化字符串内容。

**返回值** : 返回通过formatStr格式，成功赋值到对应变量中的数量,  **不是实际读入长度.**

例:

A.txt

```
ABCD 1
EFG 2
HIJK
```

```c
#include <stdio.h>

int main(void)
{
    FILE *file;
    file = fopen("xxx/A.txt", "r");
    ....
    char tmpStr[100];
    int num = 0;
    int i = 0;
    while(!feof(file)) {
        i = fscanf(file, "%s %d", tmpStr, num);
        printf("%d", i);
    }
    
   	....
   	fclose(file);
}
```

输出 ：

```
2
2
1
```

前两个2表示成功给tmpStr 和num赋值，最后一个1表示只给了tmpStr赋值，没能给num赋值。

