title: mongodb
date: 2015-09-30 22:39:34
tags:
- mongodb
---
Mongo DB 是目前在IT行业非常流行的一种非关系型数据库(NoSql)
<!--more-->
### 下载
[官网](https://www.mongodb.org/downloads#production)
下载的是msi版本
![](/../img/mongodb_download.png)

### 安装

	安装mongodb
	D:\dev\Mongodb3.0.6
	D:\dev\Mongodb3.0.6\bin
	根目录下新建data文件夹 在data下新建db、log两个文件夹
	D:\dev\Mongodb3.0.6\data\db
	D:\dev\Mongodb3.0.6\data\log

### 配置
用管理员启动cmd 切换到bin路径下
~~~bash
mongod --dbpath D:\dev\Mongodb3.0.6\data\db 
	   --logpath D:\dev\Mongodb3.0.6\data\log\db.log 
	   --install --serviceName MongoDB
~~~
运行如下图
![](/../img/mongodb_config.png)

### 启动服务
启动关闭服务（管理员身份）
~~~bash
net start MongoDB
~~~

~~~bash
net stop MongoDB
~~~

### 查看数据库
	输入mongo
	show dbs
![](/../img/mongodb_mongo.png)


	> show dbs
	local  0.078GB
	> db.test
	test.test
	> show dbs
	local  0.078GB
	> db.test.insert({name:'jay'})
	WriteResult({ "nInserted" : 1 })
	> db.test.find()
	{ "_id" : ObjectId("560bfb122e4dab1fe3beb408"), "name" : "jay" }


### 工具
[MongoVUE](http://www.mongovue.com/)
[Robomongo](http://www.robomongo.org/)	
	

### mongoimport导入数据
~~~bash
mongoimport -h 192.168.1.227:27017 -d dbname -c collectionName /type csv  -f"name,age"   --file d:\test.csv
~~~