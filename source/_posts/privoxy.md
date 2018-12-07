---
title: privoxy
date: 2018-12-06 20:49:34
tags:
---

ubuntu terminal 代理

<!--more-->

sudo install privoxy

修改配置
sudo vimi /etc/privoxy/config

查找 forward-socks5
修改成
forward-socks5 / 127.0.0.1:1080 .

启动
sudo systemctl start privoxy.service

配置代理

export http_proxy=http://127.0.0.1:8118
export https_proxy=https://127.0.0.1:8118

测试 看 goole 的页面是否能显示
curl www.google.com

取消代理
要取消该设置：
unset http_proxy
或：
unsethttps_proxy

## REF

https://www.cnblogs.com/liuxuzzz/p/5324749.html
https://blog.csdn.net/xuchaovip/article/details/56835088

--

## 问题 Ubuntu 下重新安装软件 配置文件不重新生成得问题解决

apt-get remove phpmyadmin
dpkg -P phpmyadmin
apt-get install phpmyadmin

https://blog.csdn.net/wangzhjj/article/details/53466282
