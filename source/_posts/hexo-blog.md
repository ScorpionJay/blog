title: Hexo构建博客
date: 2015-08-27 16:20:11
tags:
- hexo
---


### 什么是Hexo？
<!--more-->
	Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

### 安装
	安装前确保已经安装node
	npm install hexo-cli -g

安装中出现问题

	C:\Users\Administrator>npm install hexo-cli -g
	npm ERR! Windows_NT 6.1.7601
	npm ERR! argv "D:\\tools\\node\\\\node.exe" "D:\\tools\\node\\node_modules\\npm\\bin\\npm-cli.js" "i
	nstall" "hexo-cli" "-g"
	npm ERR! node v0.12.4
	npm ERR! npm  v2.10.1
	
	npm ERR! shasum check failed for C:\Users\ADMINI~1\AppData\Local\Temp\npm-9628-983c6cae\registry.npm
	js.org\hexo-cli\-\hexo-cli-0.1.8.tgz
	npm ERR! Expected: 17dcb7301f82f75568bb9125b2f79b2aca4b07b8
	npm ERR! Actual:   45c1fe325c66795f7bf3893a9a9f5ac246ec6014
	npm ERR! From:     https://registry.npmjs.org/hexo-cli/-/hexo-cli-0.1.8.tgz
	npm ERR!
	npm ERR! If you need help, you may report this error at:
	npm ERR!     <https://github.com/npm/npm/issues>
	
	npm ERR! Please include the following file with any support request:
	npm ERR!     C:\Users\Administrator\npm-debug.log

解决方法

	Expected和Actual不一样，下载的时候出了问题。切换到国内镜像
	npm config set registry http://registry.cnpmjs.org


###成功

	D:\tools\桌面\hexo>npm install hexo-cli -g
	npm WARN optional dep failed, continuing fsevents@0.3.8
	C:\Users\Administrator\AppData\Roaming\npm\hexo -> C:\Users\Administrator\AppData\Roaming\npm\node_m
	odules\hexo-cli\bin\hexo
	hexo-cli@0.1.8 C:\Users\Administrator\AppData\Roaming\npm\node_modules\hexo-cli
	├── abbrev@1.0.7
	├── minimist@1.1.3
	├── bluebird@2.9.34
	├── chalk@1.1.0 (supports-color@2.0.0, escape-string-regexp@1.0.3, ansi-styles@2.1.0, strip-ansi@
	3.0.0, has-ansi@2.0.0)
	├── tildify@1.1.0 (os-homedir@1.0.1)
	└── hexo-fs@0.1.3 (escape-string-regexp@1.0.3, graceful-fs@3.0.8, chokidar@0.12.6)

### 建站
``` bash
	hexo init <forder>
```

	生成如下目录
	.
	├── _config.yml	配置信息
	├── package.json 
	├── scaffolds	
	├── scripts		
	├── source
	|   ├── _drafts
	|   └── _posts
	└── themes


	scaffolds
	模版 文件夹。当您新建文章时，Hexo 会根据 scaffold 来建立文件。
	
	scripts
	脚本 文件夹。脚本是扩展 Hexo 最简易的方式，在此文件夹内的 JavaScript 文件会被自动执行。
	
	source
	资源文件夹是存放用户资源的地方。除 _posts 文件夹之外，开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。
	
	themes
	主题 文件夹。Hexo 会根据主题来生成静态页面。


### 新建一篇文章
``` bash
	hexo new [layout]<title>
```

### 生成静态文件
``` bash
	hexo generate
```

### 发布
``` bash
	hexo publish [layout] <filename>
```

### 启动服务器
``` bash
	hexo server
```
	
	选项	描述
	-p, --port	重设端口
	-s, --static	只使用静态文件
	-l, --log	启动日记记录，或覆盖记录格式


	打开浏览器localhost:4000就可以访问了

### 部署
``` bash
	hexo deploy
```

	配置文件中需要如下配置
	deploy:
	  type: git
	  repo: https://github.com/s9013/hexoblog.git

----------

	部署到github上css js不能加载问题
	# URL
	## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
	url: http://s9013.github.io/hexoblog   //仓库地址
	root: /hexoblog/					   //项目名
	permalink: :year/:month/:day/:title/
	permalink_defaults:

----------

	目录有点问题
	修改thems landscape _config.yml
	# Header
	menu:
	  Home: /hexoblog   加上项目名
	  Archives: /hexoblog/archives	加上项目名
	rss: /atom.xml
	


### 清除缓存
``` bash
	hexo clean
```


### 插件待续...


### ref

1. [https://hexo.io/zh-cn/docs](https://hexo.io/zh-cn/docs)
2. [http://blog.fens.me/hexo-blog-github](http://blog.fens.me/hexo-blog-github)
