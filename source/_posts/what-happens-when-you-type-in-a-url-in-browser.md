---
title: what happens when you type in a url in browser
date: 2018-11-26 10:01:37
tags:
  - html
  - js
  - front-end
---

当你在浏览器中输入 url 发生了什么

<!--more-->

## Steps

- cache
- dns
- tcp connect
- http request
- http response
- browser display
- tcp close

statuses
● 1xx indicates an informational message only

● 2xx indicates success of some kind

● 3xx redirects the client to another URL

● 4xx indicates an error on the client’s part

● 5xx indicates an error on the server’s part

## How browser display html

![webkitflow](/blog/img/webkitflow.png)

## REF

- https://wsvincent.com/what-happens-when-url/
- https://github.com/alex/what-happens-when
- https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/
