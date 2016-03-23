title: git
date: 2015-10-06 15:40:43
tags:
- git
---

学习git
<!--more-->
	ssh
	
	ssh-keygen -t rsa -C "youremail@example.com"

	github
	
	git init 	git初始化
	git remote	
	
	git add			添加修改
	git commit -"message"	提交修改
	git push		推送到远程
	
	git status		查看状态
	git checkout		下载
	git branch		分支
	git log			记录
	git diff		检查不同
	git merge		合并
	git branch -b dev	新增分支dev并切换到dev
	git branch -d dev	删除分支dev
	
	
	
	touch README.md
	git init
	git add README.md
	git commit -m "first commit"
	git remote add origin https://github.com/s9013/node.git
	git push -u origin master
	
	
	git init
	git checkout --orphan gh-pages
	git add .
	git commit -m "first commit"
	git remote add origin https://github.com/username....git
	git push origin gh-pages
	##问题
	git init 产生的目录解释
	error: src refspec master does not match any.
	引起该错误的原因是，目录中没有文件，空目录是不能提交上去的
	Updates were rejected because the tip of your current branch is behind
	git pull origin gh-pages 强制拉服务器的
	'git' 不是内部或外部命令，也不是可运行的程序
	path中添加git的安装路径cmd 例如D:\git\cmd


## 删除远程分支 
~~~bash
git push origin --delete gh-pages
~~~