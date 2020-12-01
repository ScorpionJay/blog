title: git 操作手册
date: 2015-1-1 15:40:43
tags:

- git

---

git 操作手册

<!--more-->

## 基本用法

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

## git pull

```
git pull = git fetch + git merge
git pull --rebase = git fetch + git rebase
```

## 分支

> 查看本地分支

```
git branch
```

> 查看远程分支

```
git branch -r
```

> 查看本地和远程分支

```
git branch -a
```

> 切换分支

```
git branch 分支名
```

> 本地分支推送到远程分支

```
git push origin test
```

> 删除本地分支

```
git branch -d 分支名
```

> 删除远程分支

```
git push origin --delete 分支名
```

git clone 获取远端 git 库，只包含了远端 git 库中的当前工作分支，

如果想要获取其他分支信息，使用 git branch -r 来查看，

如果也想获取下来，使用 git checkout -b 本地分支名 远程分支名，

如果本地已经存在分支名，则不需要'-b'参数

eg.

```
git checkout -b gh-pages remotes/origin/gh-pages
```

## 回滚

```
git log --pretty=oneline

git reset --hard HEAD^

git reset --hard HEAD~2

git reset --hard 3628164

git push -u origin master -f
```

## 日志

查看提交历史信息

```
git log
git log --pretty=oneline
```

## 合并

```
git merge

git fetch origin master


本地需要提交

git merge

然后手动解决冲突
```

## 合并提交

```
git rebase -i HEAD~2

将第二个的pick修改为s :wq保存

输入新的comments :wq保存

git log --pretty=oneline 可以查看

提交到远程
git push --force
```

## 远程地址

> 查看远程地址

```
git remote -v
```

> 修改远程地址

```
#git remote set-url <name> <url>
git remote set-url origin url
```

or

```
git remote rm origin
gir remote add origin git@github.com:ScorpionJay/blog.git
```

> 可以添加多个远程地址

```
gir remote add 远程名称 git@github.com:ScorpionJay/blog.git
```

## git 区分大小写

```
git config --global core.ignorecase false
```

## 常见问题

> gitignore 不起作用

```
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```

> 忽略/恢复跟踪

```
git update-index --assume-unchanged src/utils/config.js  #忽略跟踪
git update-index --no-assume-unchanged src/utils/config.js #恢复跟踪
```

> 分支强制覆盖

```
git push origin test:master -f  //将test分支强制（-f）推送到主分支master
```
