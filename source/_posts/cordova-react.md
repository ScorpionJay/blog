---
title: cordova-react
date: 2018-12-06 09:23:54
tags:
  - cordova
  - react
  - js
---

使用 cordova、react 做一个 app

<!--more-->

## Cordova

[Cordova](https://cordova.apache.org)Apache 的一个开源项目，使用 HTML, CSS & JS 构建一个 App。也就是所谓的壳子。

```
// 安装
npm i -g cordova

//　创建项目
cordova create MyApp

// 添加运行平台
cd MyApp
cordova platform add browser

// 运行
cordova run browser
```

```
// 添加ios
cordova platform add ios
// 添加android
cordova platform add android
// 查看已添加平台
cordova platform ls
```

```
// 编译
```

![Architecture](https://cordova.apache.org/static/img/guide/cordovaapparchitecture.png)

[Overview](https://cordova.apache.org/docs/en/latest/guide/overview/)

模拟器上运行

```
cordova emulate android
```
