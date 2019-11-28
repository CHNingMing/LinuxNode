# ES6
## import 
用来导入其他js模块，必须以http访问时才生效，使用file://（本地文件打开）会有跨域问题。
1. import 必须在模块中并且代码顶层中使用(import()可以不再模块中使用)
2. import 需要配合export 使用。
3. import的原始值，只能访问，不能重新复制，import的原始值不管有没有用const声明，都不能重新赋值。(import限制访问模块内容是单向的，也就是只读)
4. 一个js文件可以看成一个模块。
5. export就是告诉import那些内容是对外开放（MDN中叫导出，导出函数、导出对象、导出原始值）的。
6. 只有export的方法、变量、对象才能在外部访问。
### import语法
```javascript
import [name] from '[path]'				//引入模块默认对外开放内容name = 默认开放对象
import * as [name] from '[path]'		//引入模块所有对外开放内容name = 开放所有对象
import {name1[ as nameB],name2} from '[path]'		//引入模块指定对外开放内容name1/name2 = 开放指定对象
```
name : 对外开放名称,通过
path : js模块路径(绝对/相对)
name1/name2: 模块中对外开放的变量/函数/对象名称,必须保证name1,name2在指定的模块中有，并且是export声明.否则会报错。

nameB: 在{}中，也支持给个别变量起别名

### export
声明那些对象、函数、值是对外开放的。

### 实际应用
js/index.js
```javascript
//默认对外开放必须是对象
export default {
    name: "ZhangSan",
    fly: function(){
        
    },
    address: {
        city: "",
        addressDetail: ""
    }
}
//指定开放对象
export function optFun1(){
    
}
//指定开放值[原始值]
export const name = "ZhangSan";
```

index.html

```html
<html>
    <head>
        ...
        <script type="module">
            //默认对象引用
            import defaultObj from './js/index.js'
            //指定对象引用
            import optFun1 from './js/index.js'
            //指定多个对象引用
            import {optFun1 as optFun1_1,name} from './js/index.js'
            
        </script>
    </head>
</html>
```













