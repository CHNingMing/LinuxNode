# NPM

类似Maven，区别管理的是JS代码

## 安装：

NodeJS新版都带NPM工具。

## 模块：

一个模块中包含多个JS文件

### 安装模块：

npm install <模块名> [参数]

默认(执行目录下没有package.json)模块安装到用户目录

#### 本地安装[默认]和全局安装

Npm install <模块名>

Nom install <模块名> -p



安装的命令行执行模块去node_module/.bin/下找



### 列出安装模块：

npm list			//列出当前目录模块

npm list -g			//列出全局模块



## package.json

类似Maven的POM.xml，管理各个包的信息

可以通过**npm init** 创建一个package.json

期间会回答一系列问题：

```
//问题
名称
版本
项目简介
作者
...
最后yes
```

不想回答问题时直接 npm init --yes,直接生成package.jsons

PS:安装模块时(除全局安装-g)只有当前目录有package.json才会在指定目录创建node_modules

如果项目已有package.json，使用：

```
npm install --save-dev
```

#### 两种依赖：

​	dependencies	：运行依赖

​	devDependencies	：	开发依赖

# WebPack

前端静态文件打包工具，自身支持js,遵循commandJS模块化规范（可以使用require引入js模块）规范

开发时可以用require()引入其他模块（js文件）,在通过Webpack编译成一个或多个可执行js文件,html引入这个输出Js

## 安装WebPackage

暂时只使用当前目录安装成功，全局安装总是提示安装webpack-cli，但是又安装不上

```
npm install webpack --save-dev
//执行webpack
node_module/.bin/webpack [参数]
//第一次执行提示安装webpack-cli，输入yes安装
```

### Webpack.config.js

WebPackage配置文件

执行webpack首先检查当前目录是否有Webpack，有时按照配置文件打包

基本配置文件：

```js
module.exports = {
    entry:'./app/index.js',
    output:{
        path: './output1',
        filename: 'output-file.js'
    }
};

```

#### entry可接受三个参数：

对象形式：

​	entry{ "key":"*.js" }

​	后期再 个别地方可以使用这个key:

​		列入：filename:'[name]_file.js'

​	最后[name]解析成key:key_file.js

数组形式：

​	打包多个入口文件

```json
entry{
    vendor:['main.js','main_1.js'...]
}
```







### Webpack参数

#### Webpack  [\*.js,\*.js,\*.js...]

如果没有webpack.config.js时，使用 webpack  *.js *.js *.js...同事打包多个入口文件

默认在当前目录创建dist/main.js,最后html页引入这个main.js正常执行js

















