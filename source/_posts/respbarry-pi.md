---
title: Raspberry pi
date: 2018-11-22 18:15:15
tags:
  - pi
  - 树莓派
---

Raspberry pi 是一种小型数字计算机，在现代技术领域具有广泛的应用。 它是一个可编程的设备，可以按要求工作。它具有形状和大小的多功能性，以及操作的动态特性，有助于以简单的方式和较短的过程来实施创新思想。

<!--more-->

## 烧入系统

官方下载软件及系统，设置账号，wifi，开启 ssh。

## ssh 登录

```
ssh pi@raspberrypi.local
```

[docker 脚本安装](https://docs.docker.com/engine/install/debian/#install-using-the-convenience-script)

## 安装 docker

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

> 启动

```
sudo systemctl start docker
```


## 内网穿透

nps 安装
