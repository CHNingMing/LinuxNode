# 连接MySql

1.保证连接mysql代码没再主线程,单独打开一个线程

android之android.os.NetworkOnMainThreadException异常

2.保证开启

报错:SecurityException: Permission denied (missing INTERNET permission?)

```
<uses-permission android:name="android.permission.INTERNET" />
```

访问网络权限

