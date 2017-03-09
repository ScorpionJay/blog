title: nodejs  express 构建博客
date: 2016-10-26 17:29:39
tags:
- node
---
博客
<!--more-->
nodejs  express 构建博客

# 介绍（introduce）

nodejs v8
express node.js web framework
mongodb nosql database

# [express](http://expressjs.com/)

install express
~~~bash
npm install express-generator -g
express -e blog
cd blog & npm install
~~~

生成下面的目录（this will generate this structure）：
~~~bash
blog
├──  bin
|	|── www			   // 启动服务
├──  public			   // 公用目录
|	|── images
|	|── javascripts
|	|── stylesheets
├──  routes				// 路由目录
|	|── index.js
|	|── users.js
├── views				//视图目录
|	|── error.ejs
|	|── index.ejs
├──  app.js				// 配置文件
├──  package.json
~~~

~~~bash
npm start //start service
~~~

open http://localhost:3000/




