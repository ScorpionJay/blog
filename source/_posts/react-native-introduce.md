title: React Native Introduce
date: 2016-06-17 10:06:29
tags:
-  react native
---
[facebook](https://facebook.github.io/react-native/)推出的用js来写app，可以在ios和android上跑。性能接近原生，大大缩短开发周期，热更新，chrome debug都是很好的东西。

<!--more-->


# 新手入门
学习React Native(接下来就叫RN)，先来了解下[常见问题](http://bbs.reactnative.cn/topic/130)，避免入坑。接下来就开始[在windows上搭建环境](http://bbs.reactnative.cn/topic/10)。

- [官方文档](https://facebook.github.io/react-native/)
- [中文文档](http://reactnative.cn/)

# 搭建环境

## [Chocolatey](https://chocolatey.org/)

Chocolatey是一个Windows上的包管理器，类似于linux上的yum和 apt-get。 你可以在其官方网站上查看具体的使用说明。一般的安装步骤应该是下面这样：


Cmd.exe

@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin


## [Python2](https://www.python.org/)
打开cmd，使用chocolatey安装python2,还不支持python3
~~~
choco install python2
~~~

## [Node](https://nodejs.org/en/)
~~~
choco install nodejs.install
~~~

## React native 命令行工具(react-native-cli)
~~~
npm install -g react-native-cli
~~~

## [Android Studio](https://developer.android.com/studio/index.html)
	需要android studio2.0或者更高的版本
	配置环境变量
	build tools 需要23.0.1版本
	配置ANDROID_HOME
	%ANDROID_HOME%\tools;%ANDROID_HOME%\platform_tools


## [git](https://git-scm.com/)
~~~
choco install git
~~~

## [genymotion](https://www.genymotion.com/)
这个模拟器比官方的快很多，下载的时候需要注册。

## 测试安装
~~~
react-native init AwesomeProject
cd AwesomeProject
react-native run-android
~~~
js bundle
http://localhost:8081/index.android.bundle

# 开始写代码
看下生成的代码index.android.js android代码的入口方法

~~~java
package com.x;

import com.facebook.react.ReactActivity;
import com.facebook.react.ReactPackage;
import com.facebook.react.shell.MainReactPackage;

import java.util.Arrays;
import java.util.List;

public class MainActivity extends ReactActivity {

    /**
     * Returns the name of the main component registered from JavaScript.
     * This is used to schedule rendering of the component.
     */
    @Override
    protected String getMainComponentName() {
        return "X";
    }

    /**
     * Returns whether dev mode should be enabled.
     * This enables e.g. the dev menu.
     */
    @Override
    protected boolean getUseDeveloperSupport() {
        return BuildConfig.DEBUG;
    }

    /**
     * A list of packages used by the app. If the app uses additional views
     * or modules besides the default ones, add more packages here.
     */
    @Override
    protected List<ReactPackage> getPackages() {
        return Arrays.<ReactPackage>asList(
            new MainReactPackage()
        );
    }
}

~~~

java文件就这么一个，组件名字“X”

入口js index.android.js 这么写
~~~js
import  {AppRegistry} from 'react-native'
import App from './src/App'

AppRegistry.registerComponent('X', () => App);
~~~


nav 有点不懂

最后[打包](https://s9013.gitbooks.io/book/content/react-native/rn-2-package.html)

app图标

AndroidManifest.xml
android:icon="@mipmap/logo" 这里修改

图片为png格式

在res/minmap 文件夹下加下图片
hdpi mdpi xhdpi xxhdpi 手机分辨率

ldpi：240x320
mdpi：320x480
hdpi：480x800
xhdpi：960*720
xxhdpi：1280×720

修改app名字
res/values/strings.xml
~~~xml
<resources>
    <string name="app_name">哈哈哈</string>
</resources>
~~~


# FQA
## adb devices 有问题

http://stackoverflow.com/questions/5092542/adb-server-is-out-of-date/26763766#26763766