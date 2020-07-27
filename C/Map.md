# pair

存储单个key->value时使用。

头文件: 

```c
#include <utility>
```

## 初始化pair

```C
//三种初始化方式
pair<char*, char*> charP;
pair<int, char*> charI(10, "ABCDE");
pair<const char*, const char*> makePair = make_pair("key","value");
```

## 使用

pair是个结构体不是class,所以直接访问first和second属性就可以。

```
pair<int, char*> charI(10, "ABCDE");
cout << charI.first << ":" << charI.second << endl;
```

# map

key->value 结构。

头文件

```c
#include <map>
```

## 初始化map

```c
map<int, const char*> m; //创建空map
```

## 操作Map

```c
map<int, const char*> m;
//新增数据
map.insert(make_pair(0, "ABC"));
map[1] = "DEF";
//遍历map
map<int, const char*>::iterator it;
for(it = m.begin(); it != m.end(); it++){
    cout << it.first << " : " << it.second << endl;
}
//根据Key验证是否有指定值
m.count(1);// 统计map中key为1总共出现次数
//根据key获取指定键/值
map<int, const char*>::iterator findItem = map.find(1);
cout << findItem.first << " : " << findItem.second << endl;
```





