title: sass
date: 2015-11-16 17:16:59
tags:
- css
- html
---
sass写css
<!--more-->
## 安装ruby
install ruby
sudo apt-get install ruby


## sass
### 安装sass
gem install sass
出现ERROR: Could not find a valid gem时的处理方法
更改镜像
$ gem sources --remove https://rubygems.org/
$ gem sources -a https://ruby.taobao.org/
$ gem sources -l
*** CURRENT SOURCES ***

https://ruby.taobao.org

sudo gem install sass

### sass使用
~~~bash
sass _bootstrap.scss bootstrap.scss
~~~



## compass

### 安装compass
gem install compass

### compass使用
初始化项目
~~~bash
compass create myproject
~~~
编译
~~~bash
compass compile
~~~

ref
http://www.ruanyifeng.com/blog/2012/06/sass.html
http://my.oschina.net/sunshinewyf/blog/513235
