---
title: docker
date: 2018-09-26 15:23:59
tags:
  - docker
---

docker

<!--more-->

# docker

docker

- image
- container

## 安装 docker

```
# 安装docker.io 是ubuntu团队维护的一个包
sudo apt install docker.io

# 启动docker
systemctl start docker


# Verify
sudo docker run  hello-world

# pull nginx image
sudo docker pull nginx

# first run
# create container
# run container
docker run

# start|stop container
docker start|stop

# list container
docker ps -a

# remove container
docker rm

# remove image
docker  rmi

# rename container
docker rename old_name new_name

# enter container
sudo docker exec -it container_name  /bin/bash


sudo docker build -t react:v1 .
sudo docker images
sudo docker run --name react react:v2


# 打包镜像提交到 dockerhub

docker login -u scorpionjay

docker images
docker tag python_node scorpionjay/python_node
docker push scorpionjay/python_node
```

## [docker-compose](https://docs.docker.com/compose/install/#install-compose)

```
install

# 下载docker-compose 网络太慢可以到github手动下载
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose


sudo chmod +x /usr/local/bin/docker-compose

# 软连接
sudo ln -sf /usr/local/bin/docker-compose /usr/bin/docker-compose

# 验证版本
docker-compose --version


sudo docker-compose up -d
sudo docker-compose down
```

## jenkins

```
docker run --name myjenkins -p 8080:8080 -v /var/jenkins_home jenkins

docker start myjenkins
```
