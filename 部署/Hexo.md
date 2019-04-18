试试在github搭自定义页面网页，异步请求php返回json 动态网站

发现全局安装hexo根本没什么用

```
npm install hexo --save
```

新版hexo独立了server，需要先全局安装hexo-server，在本项目安装

```
npm install hexo-server -g
npm install hexo-server --save
```

# HEXO

入口文件:layout/layout.ejs

源页面:${hexo}/source/_posts/*.md 	设置后在右侧目录显示

资源文件:source/js/s.js			source非hexo下source,是主题内source

Html页:source/*.html

head部分:layout/_partial/head.ejs

layout/_partial/article.ejs			详细文档内容

layout/_partial/sidebar.ejs		右侧目录内容

## 初始化HEXO

npm install hexo-cli -g

hexo init [部署名称]

cd [部署名称]

npm install 

hexo server



