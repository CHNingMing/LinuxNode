

[TOC]

# Solr

	搜索关键词中需要去除**空格**
	空格会破坏关键词分词

### Sort排序

```java
new Sort(Sort.Directory.ASC/DESC,"字段")
    query.addStort(Sort对象);
```

### Spring task

	任务调度

### Array转换集合注意

```
Array.asList(数组对象)
数组转成集合后，集合长度固定，不能使用add和remove方法
```



	









