---
title: html disable copy
date: 2019-10-21 22:21:33
tags:
  - js
  - html
---

页面禁止复制

<!--more-->

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0, user-scalable=no"
    />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>禁止复制</title>
    <style>
      * {
        -webkit-touch-callout: none; /*系统默认菜单被禁用*/
        -webkit-user-select: none; /*webkit浏览器*/
        -khtml-user-select: none; /*早期浏览器*/
        -moz-user-select: none; /*火狐*/
        -ms-user-select: none; /*IE10*/
        user-select: none;
      }
      /* input {
        -webkit-user-select: auto;
      } */
    </style>
  </head>
  <body>
    <input placeholder="请输入" />
    <div>禁止复制</div>
  </body>
  <script>
    window.onload = function() {
      var lastTouchEnd = 0;
      document.addEventListener(
        "touchend",
        function(event) {
          var now = new Date().getTime();
          if (now - lastTouchEnd <= 300) {
            event.preventDefault();
          }
          lastTouchEnd = now;
        },
        false
      );
      document.addEventListener("gesturestart", function(event) {
        event.preventDefault();
      });
    };
  </script>
</html>

```
