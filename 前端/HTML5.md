# HTTP

[百度百科]

https://baike.baidu.com/item/HTTP%E6%97%A0%E7%8A%B6%E6%80%81%E5%8D%8F%E8%AE%AE/5808645?fr=aladdin

## HTTP无状态协议

表示每一次HTTP请求都是一个全新的状态。每次HTTP请求不能拿到上次HTTP请求交互的数据。

## Cookie

Cookie存储在客户端，以文件形式存在。

针对HTTP无状态协议的缺陷，Cookie 产生了，服务器通过响应特定请求头，告诉浏览器创建一个Cookie，并存储Cookie对应信息。

在以后浏览器请求时，都会带上Cookie文件。

ps：前提保证Cookie所属域名和当前域名对应，并且Cookie没有过期。这些信息在浏览器创建Cookie时设定。

默认Cookie存储目录：

windows

```
[系统盘]:\Documents and Settings\[用户名]\Cookies目录中找到存储的Cookie
```

## Session

在服务端存储，客户端通过cookie存储Sessionid。

服务端可设置：

​	Session 最大存活时间

​	Session 空闲存活时间

服务端主动创建Session，会生成一个Sessionid，并响应回客户端。

客户端收到Sessionid后，会把Sessionid存储到Cookie中。

在以后HTTP请求时，都会带上这个Cookie。

# HTML5 存储

## sessionStorage

主要用来存储临时数据

同源策略限制: http[s]://host:port

但标签页限制:存储的数据只限**当前标签页**可以访问

KeyValue形式存储数据。

存储上限限制。

只在本地存储，不会通过HTTP请求发送到服务端。

### sessionStorage操作：

返回指定索引key

```cassandra
string sessionStorage.key(int index)
```

返回指定key对应value

```c
string sessionStorage.getItem(string key)
```

添加/更新数据

```
void sessionStorage.setItem(string key,string value)
```

通过key删除数据

```
void sessionStorage.removeItem(string key) 
```

清空列表

```
void sessionStorage.clear() 
```

## localStorage

**同步操作**

存储的数据没有时间限制。

直接以对象形式使用，直接复制属性+值





## IndexedDB

**异步操作**

浏览器提供的本地数据库，支持建立索引。但是不支持SQL语句

键值对存储对象，**键不允许重复**，否则会报错。

**同步操作**

同源策略

**存储空间没有限制**

**支持二进制存储**

### 事件

#### onerror

某些操作错误，如：数据库打开错误，请求事务操作失败等..

#### onsuccess

操作成功回调

#### onupgradeneeded

function ([IDBVersionChangeEvent](https://developer.mozilla.org/en-US/docs/Web/API/IDBVersionChangeEvent) )



数据库升级时触发，数据库第一次创建也会触发。一般在这个事件里创建数据库索引等其他约束和初始化内容。



#### oncomplete

在数据库接口创建好时调用，一般用来写入数据库初始数据。

```javascript
request.onupgradeneeded = function(event) {
    var db = event.target.result;
    //这样设置必须保证传入对象中有主键id属性
    var store =  db.createObjectStore('stent表名',{keyPath:'主键id'});
    //创建索引
    store.createIndex('name','name',{ unique: flase });
    store.createIndex('email','email',{ unique: true });
    //保证上述操作完成后在添加数据
    store.transaction.oncomplete = function(){
        var customObjectStore = db.transaction('stent表名','readwrite').objectStore('stent表名');
        //...插入数据操作
        customObjectStore.add({'主键id':1,name:'张三','email':'gengmingyan@yeah.net'});
        
    }
    
}




```





### 操作

#### 创建数据库/打开数据库

window.indexedDB.open(dbname,[version])

dbname:数据库名称

version:数据库版本号

```

var request = window.indexedDB.open('db_test',1);

```

需要打开的数据库如果存在，直接打开。

如果不存在，则创建。并触发onupgradeneeded(数据库升级)事件。







