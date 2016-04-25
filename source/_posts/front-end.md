title: front-end
date: 2016-04-25 13:27:26
tags:
- js
---
前端的一些东西...
<!--more-->
#  前端的一些东西

## 一 Node.js

### [1.什么是Node.js](https://nodejs.org)
<img src="/img/nodejs.jpg" height="100" align="left">
Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效。Node.js 的包管理器 [npm](https://www.npmjs.com/)，是全球最大的开源库生态系统。

----------

### [2.安装](https://nodejs.org/en/download/)
![node download](/img/node-download.png)
~~~

node -v //查看node版本
v4.4.0

npm -v //查看npm版本

// npm 命令
c:\demo>npm

Usage: npm <command>

where <command> is one of:
    access, add-user, adduser, apihelp, author, bin, bugs, c,
    cache, completion, config, ddp, dedupe, deprecate, dist-tag,
    dist-tags, docs, edit, explore, faq, find, find-dupes, get,
    help, help-search, home, i, info, init, install, issues, la,
    link, list, ll, ln, login, logout, ls, outdated, owner,
    pack, ping, prefix, prune, publish, r, rb, rebuild, remove,
    repo, restart, rm, root, run-script, s, se, search, set,
    show, shrinkwrap, star, stars, start, stop, t, tag, team,
    test, tst, un, uninstall, unlink, unpublish, unstar, up,
    update, upgrade, v, verison, version, view, whoami

npm <cmd> -h     quick help on <cmd>
npm -l           display full usage info
npm faq          commonly asked questions
npm help <term>  search for help on <term>
npm help npm     involved overview

// install
c:\demo>npm install -h
npm install
npm install <pkg>
npm install <pkg>@<tag>
npm install <pkg>@<version>
npm install <pkg>@<version range>
npm install <folder>
npm install <tarball file>
npm install <tarball url>
npm install <git:// url>
npm install <github username>/<github project>

npm install grunt-cli -g // 全局安装grunt-cli
~~~
![npm install package](/img/npm-install-package.png)

### 3.创建项目
~~~
mkdir demo // 创建demo文件夹
cd demo	//切换到demo
npm init //package.json 这个有点类似maven的pom.xml
~~~
![npm init](/img/init.png)

package.json文件
~~~
{
  "name": "demo",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
~~~



## 二 NPM pachage
### 1.[Grunt](http://gruntjs.com/)
<img align="left" height="200px" src="/img/grunt-logo.png">
Javascript世界的构建工具
为何要用构建工具？
一句话：自动化。对于需要反复重复的任务，例如压缩（minification）、编译、单元测试、linting等，自动化工具可以减轻你的劳动，简化你的工作。当你在 Gruntfile 文件正确配置好了任务，任务运行器就会自动帮你或你的小组完成大部分无聊的工作。
为什么要使用Grunt？
Grunt生态系统非常庞大，并且一直在增长。由于拥有数量庞大的插件可供选择，因此，你可以利用Grunt自动完成任何事，并且花费最少的代价。如果找不到你所需要的插件，那就自己动手创造一个Grunt插件，然后将其发布到npm上吧。先看看入门文档吧。
可用的Grunt插件
你所需要的大多数task都已经作为Grunt插件被开发了出来，并且每天都有更多的插件诞生。插件列表页面列出了完整的清单。下面给出几个你可能听说过的插件：
<img  src="/img/grunt-plugin.png">

~~~
npm install grunt --save//save 参数将这个插件保存到package.json中的dependencies中
~~~
![grunt](/img/install-grunt.png)
![grunt](/img/install-grunt2.png)

[Get start](http://www.gruntjs.net/getting-started)

gruntfile.js 用来配置或定义任务（task）并加载Grunt插件的。
Gruntfile文件案例

在下面列出的这个 Gruntfile 中，package.json文件中的项目元数据（metadata）被导入到 Grunt 配置中， grunt-contrib-uglify 插件中的uglify 任务（task）被配置为压缩（minify）源码文件并依据上述元数据动态生成一个文件头注释。当在命令行中执行 grunt 命令时，uglify 任务将被默认执行。
~~~
module.exports = function(grunt) {

  // Project configuration.
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    uglify: {
      options: {
        banner: '/*! <%= pkg.name %> <%= grunt.template.today("yyyy-mm-dd") %> */\n'
      },
      build: {
        src: 'src/<%= pkg.name %>.js',
        dest: 'build/<%= pkg.name %>.min.js'
      }
    }
  });

  // 加载包含 "uglify" 任务的插件。
  grunt.loadNpmTasks('grunt-contrib-uglify');

  // 默认被执行的任务列表。
  grunt.registerTask('default', ['uglify']);

};
~~~




### [2.Bower](http://bower.io)
#### 1).什么是Bower
<img align="left" height="200px" width="200px" src="/img/bower.png">

twitter推出包管理工具。其特点是对包结构没有强制规范，也因此bower本身并不提供一套构建工具，它充当的基本上是一个静态资源的共享平台。

bower本身不存储模块文件本身（NPM以及SPM则会将模块作者的文件打包保存在自己的服务器中），也不保存模块的版本信息。模块的发布者通过注册（register）的方式，将模块的可访问的公开的git地址记录在bower的数据库中。而所有的版本都是通过模块发布者自己控制代码库的tag来决定。

bower在安装流程基本上可以简单认为是将注册的git地址中的特定tag clone一份到你本地的bower_components 目录中。

看起来bower本身提供的功能，以及实现都比价简单，但是它确实使用最广的前端模块管理工具。它在github上的项目有1w+的star。之所以bower能这么流行，得益于它宽松的规范能很好地直接应用在很多已经存在的项目中，所有人都能通过简单地添加一个bower.json以及补充相关信息，不需要修改代码和目录结构，就马上开始使用注册发布自己的模块。

#### 2).安装
~~~
npm install bower --save

c:\demo>npm install bower install --save
npm WARN package.json demo@1.0.0 No description
npm WARN package.json demo@1.0.0 No repository field.
npm WARN package.json demo@1.0.0 No README data
install@0.6.1 node_modules\install
bower@1.7.9 node_modules\bower

c:\demo>bower -v // 查看bower版本
1.7.9
~~~
#### 3).使用
~~~
Command line reference

cache
help
home
info
init
install
link
list
login
lookup
prune
register
search
update
uninstall
version
~~~

~~~
bower init // 创建bower.json
bower home jquery // 打开jquery的网站
bower install jquery // 安装jquery
~~~

### 3.其他
	gulp	// 和grunt差不多
	hexo	// 写博客
	gitbook	// 写书

## 三 模块化
### 1.什么是模块化

	为什么要使用模块化
	命名冲突 全局污染 维护性 代码复用
	jquery就是一个模块化的库，所有的方法都是通过$这个对象去调用。

### 2.实现
1).通过创建对象来实现
~~~
var module = {
	foo:function(){
		console.log('foo');
	},
	bar:function(){
		console.log('bar');
	}
}
module.foo();
~~~
很直观，解决了全局污染。但是js对象的封闭性不好，重要信息容易泄漏，安全问题。

2)使用闭包的方法
~~~
var module = (function(){
	var _count = 0;

	var m1 = function(){
		return _count++;
	};

	var m2 = function(){
		return _count--;
	};

	return {
		m1: m1,
		m2: m2
	}
})();
~~~
3)两大标准：CMD AMD
~~~
//1. 通用模块定义 CMD(Common Module Definition)
define(function(require,exports){
	// 获取jquery模块
	var $ = require('jquery');
	
	//调用jquery的ajax方法
	$.ajax({
		...
	});
});
//随时调用外部模块，执行期间，不断遍历查找模块的位置
//特点依赖就近
//seajs

//2.异步模块定义 AMD (Asynchronous Moule Definition) 
define(["my/cart", "my/inventory"],
    function(cart, inventory) {
        //return a function to define "foo/title".
        //It gets or sets the window title.
        return function(title) {
            return title ? (window.title = title) :
                   inventory.storeName + ' ' + cart.name;
        }
    }
);
//进入模块时，就知道了依赖，只有依赖都加载完成，模块内部代码才执行。 
//依赖前置
//requirejs 这个库也支持cmd
~~~

### 3.[Requirejs](http://requirejs.org)
	RequireJS的目标是鼓励代码的模块化，它使用了不同于传统<script>标签的脚本加载步骤。
    可以用它来加速、优化代码，但其主要目的还是为了代码的模块化。它鼓励在使用脚本时以module ID替代URL地址。
~~~
<!DOCTYPE html>
<html>
    <head>
        <title>My Sample Project</title>
        <!-- data-main attribute tells require.js to load
             scripts/main.js after require.js loads. -->
        <script data-main="scripts/main" src="scripts/require.js"></script>
    </head>
    <body>
        <h1>My Sample Project</h1>
    </body>
</html>
~~~

~~~
requirejs.config({
    //By default load any module IDs from js/lib
    baseUrl: 'js/lib',
    //except, if the module ID starts with "app",
    //load it from the js/app directory. paths
    //config is relative to the baseUrl, and
    //never includes a ".js" extension since
    //the paths config could be for a directory.
    paths: {
        app: '../app'
    },
	shim:{
		//...
	}
});

// Start the main app logic.
requirejs(['jquery', 'canvas', 'app/sub'],
function   ($,        canvas,   sub) {
    //jQuery, canvas and the app/sub module are all
    //loaded and can be used here now.
});
~~~

~~~
define(["jquery", "jquery.alpha", "jquery.beta"], function($) {
    //the jquery.alpha.js and jquery.beta.js plugins have been loaded.
    $(function() {
        $('body').alpha().beta();
    });
});
~~~

[optimization](http://requirejs.org/docs/optimization.html)
	r.js是requireJS的优化（Optimizer）工具，可以实现前端文件的压缩与合并，
	在requireJS异步按需加载的基础上进一步提供前端优化，减小前端文件大小、减少对服务器的文件请求。

[r.js配置](https://github.com/requirejs/r.js/blob/master/build/example.build.js)


## 四 [Angularjs](https://angular.io) 
AngularJS[1]  诞生于2009年，由Misko Hevery 等人创建，后为Google所收购。是一款优秀的前端JS框架，已经被用于Google的多款产品当中。AngularJS有着诸多特性，最为核心的是：MVVM、模块化、自动化双向数据绑定、语义化标签、依赖注入等等。
[api](http://docs.angularjs.cn/api)

app controller  directive fillter 
angular-route
angular-ui-router


## 五 [React](http://facebook.github.io/react/)
React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设Instagram 的网站。做出来以后，发现这套东西很好用，就在2013年5月开源了。
由于 React的设计思想极其独特，属于革命性创新，性能出众，代码逻辑却非常简单。所以，越来越多的人开始关注和使用，认为它可能是将来 Web 开发的主流工具。
这个项目本身也越滚越大，从最早的UI引擎变成了一整套前后端通吃的 Web App 解决方案。衍生的 React Native 项目，目标更是宏伟，希望用写 Web App 的方式去写 Native App。如果能够实现，整个互联网行业都会被颠覆，因为同一组人只需要写一次 UI ，就能同时运行在服务器、浏览器和手机。
React主要用于构建UI。你可以在React里传递多种类型的参数，如声明代码，帮助你渲染出UI、也可以是静态的HTML DOM元素、也可以传递动态变量、甚至是可交互的应用组件。

## 六 [Ionic](http://ionicframework.com/)
ionic 是一个强大的 HTML5 应用程序开发框架(HTML5 Hybrid Mobile App Framework )。 可以帮助您使用 Web 技术，比如 HTML、CSS 和 Javascript 构建接近原生体验的移动应用程序。
ionic 主要关注外观和体验，以及和你的应用程序的 UI 交互，特别适合用于基于 Hybird 模式的 HTML5 移动应用程序开发。
ionic是一个轻量的手机UI库，具有速度快，界面现代化、美观等特点。为了解决其他一些UI库在手机上运行缓慢的问题，它直接放弃了IOS6和Android4.1以下的版本支持，来获取更好的使用体验。
ionic 特点
1.ionic 基于Angular语法，简单易学。
2.ionic 是一个轻量级框架。
3.ionic 完美的融合下一代移动框架，支持 Angularjs 的特性， MVC ，代码易维护。
4.ionic 提供了漂亮的设计，通过 SASS 构建应用程序，它提供了很多 UI 组件来帮助开发者开发强大的应用。
5.ionic 专注原生，让你看不出混合应用和原生的区别
6.ionic 提供了强大的命令行工具。
7.ionic 性能优越，运行速度快。
