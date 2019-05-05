# 字符串转对象

Object JSONObject.parse(json字符串)

Object可以是:Map、JSONObject、实体类...

```java


String json = "{\"msg\":\"成功\",\"token\":\"59c703306973772162643816abdd44ad\",\"status\":1}";
JSONObject jsonObject = (JSONObject) JSONObject.parse(json);
jsonObject.getString("token")
Map<String,Object> jsonmap = (Map<String,Object>)JSONObject.parse(json);

```













