---
title: ionic
date: 2016-04-05 17:00:38
tags:
- ionic
---
# [ionic官网](http://www.ionicframework.com/)
<!--more-->
## [get started](http://ionicframework.com/getting-started/)

### 安装ionic
~~~sh
 npm install -g cordova ionic
~~~

### 创建项目
~~~sh
 $ ionic start myApp tabs
~~~

### 运行
~~~sh
$ cd myApp
$ ionic platform add android   #添加android平台
$ ionic build android		  #编译android平台包
$ ionic emulate android		#andorid模拟器中安装
$ ionic run android			#andorid真机中安装
~~~

### 注意需要配置android环境变量
	ANDROID_HOME
	PATH %ANDROID_HOME%\platform-tools


---

ionic tab导航在android 真机测试中 导航在顶部解决方法
http://www.myexception.cn/android/1899330.html

.config(function($stateProvider, $urlRouterProvider,$ionicConfigProvider) {

  $ionicConfigProvider.platform.ios.tabs.style('standard'); 
  $ionicConfigProvider.platform.ios.tabs.position('bottom');
  $ionicConfigProvider.platform.android.tabs.style('standard');
  $ionicConfigProvider.platform.android.tabs.position('bottom');

  $ionicConfigProvider.platform.ios.navBar.alignTitle('center'); 
  $ionicConfigProvider.platform.android.navBar.alignTitle('center');

  $ionicConfigProvider.platform.ios.backButton.previousTitleText('').icon('ion-ios-arrow-thin-left');
  $ionicConfigProvider.platform.android.backButton.previousTitleText('').icon('ion-android-arrow-back');        

  $ionicConfigProvider.platform.ios.views.transition('ios'); 
  $ionicConfigProvider.platform.android.views.transition('android');
  
  
  
  
  
 跨域请求
 ~~~java
 package com.wind.controller;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import com.fasterxml.jackson.databind.util.JSONPObject;
import com.wind.vo.UserVo;

/** 
* @ClassName: 		JsonpTestController 
* @Description: 	
* @author 			Jay
* @date 			2016年1月9日 下午3:30:41  
*/
@RestController
@RequestMapping(value="jsonp")
public class JsonpTestController {

	private static final Logger logger = LoggerFactory.getLogger(JsonpTestController.class);

	@RequestMapping(value="test")
	private JSONPObject test(@RequestParam String callback) {
		logger.info("回调函数： {}" , callback);
		UserVo vo = new UserVo("Jay",18);
		return new JSONPObject(callback, vo);
	}
	
}

~~~




# 提高性能 crosswalk

添加
ionic browser add crosswalk

去除
ionic browser revert android

  