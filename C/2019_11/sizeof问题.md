### sizeof('A')和char a = 'A'; sizeof(a)

C中:

```c
char a = 'a';
printf("%d",sizeof('a'));	//4
printf("%d",sizeof(a));		//1
```

C++中：

```c++
char a = 'a';
printf("%d",sizeof('a'));	//1
printf("%d",sizeof(a));		//1
```





