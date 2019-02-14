# VUE

所有元素都通过vue对象绑定

## 普通数据绑定：

```html
<span id="appSpan"> {{ message }} </span>
<script>
    var vue = new Vue({
        el: '#appSpan',
        data:{
            message: 'First Vue!'
        }
    });
</script>
```

如果想重新赋值：

```javascript
vue.data.message = "new Data!"
//可以直接vue.message赋值

```

或通过元素获取data:

```javascript
var span = document.querySelector('#appSpan');
span.__vue__._data.message = "new Data!";
```

## 特殊数据绑定：

通过v-开头的属性都数据vue特殊数据绑定指令

### v-bind:title="值"

绑定元素title属性

```html
<span id="spanA" v-bind:title="message"></span>
//正常绑定message值
```

### v-if

控制元素可见

```html
<span id="spanA" v-if="display"></span>
//设置display值为true时可见，false时不可见
```

### v-for

循环数据，**保证id和v-for没在一个元素上**

```html
<ol id="appFor">
    <li v-for="items in item">{{ item }}</li>
</ol>
<script>	
    new Vue({
        el:'#appFor',
        data:{
            items : ['item1','item2','item3']
        }
    });
</script>
```

两个元素数据绑定：

### v-model

```html
<div id="app">
 <span>{{ spanValue }}</span>
 <input type="text" v-model="spanValue" />
</div>


```



## 绑定方法：

V-on:click="方法名"

```html

<div id="app'">
    <span v-on:click="alertMsg">点击我</span>
</div>
```

```javascript
new Vue({
    el:'#app',
    methods:{
        alertMsg:function(){
            alert('hello method');
        }
    }
});
```

