---
title: docker-compose-sample
date: 2018-10-29 11:48:53
tags:
  - docker
---

docker-compose sample

<!--more-->

## 项目结构

```
docker-compose-sampel
├── docker-compose.yml      docker-compose 配置文件
├── java                    api
│   ├── api.war             java war
├── mysql                   数据库
│   └── db
│       ├── auto.cnf
│       ├── ibdata1
│       ├── ib_logfile0
│       ├── ib_logfile1
│       ├── mysql [error opening dir]
│       ├── one [error opening dir]
│       └── performance_schema [error opening dir]
└── nginx                   nginx
    ├── Dockerfile
    ├── etc
    │   └── nginx.conf      nginx配置文件
    ├── html
    │   └── index.html      静态文件
    └── log                 日至
        ├── access.log
        └── error.log
```

## docker-compose.yml

```
version: "3"
services:
  mysql:
    image: mysql:5.6      #镜像
    container_name: mysql #容器名
    volumes:
      - ./mysql/db:/var/lib/mysql
      # - ./mysql/config/my.cnf:/etc/my.cnf
    ports:
      - 3306:3306   #暴露出来的端口
    environment:
      - MYSQL_ROOT_PASSWORD=123456  #mysql密码
    command: --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci #设置mssql编码
    networks:   #网络
      app_net:
        ipv4_address: 172.16.238.10 #指定ip
      # - app_net

  java:
    image: openjdk:8
    container_name: java
    volumes:
      - ./java:/opt/app
    # ports:
    #   - 8080:8080
    # links:
    #   - mysql
    networks:
      # app_net:
      #   ipv4_address: 172.16.238.11
      - app_net
    command: java -jar /opt/app/api.war #运行war

  nginx:
    # image: nginx:alpine
    image: nginx
    container_name: nginx
    volumes:
      - ./nginx/html:/usr/share/nginx/html
      - ./nginx/etc:/etc/nginx/conf.d
      - ./nginx/log:/var/log/nginx
    ports:
      - 80:80
    # links:
    #   - mysql:default
    networks:
      # app_net:
      #   ipv4_address: 172.16.238.12
      - app_net

networks:
  app_net:
    driver: bridge
    ipam:
      driver: default
      config:
        - subnet: 172.16.238.0/24
        - subnet: 2001:3984:3989::/64
```

## network

networks 创建网络，java 连接 mysql,url 中 ip 使用 mysql 服务名

```
spring.datasource.url=jdbc:mysql://mysql:3306/one?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
```

nginx 方向代理使用 java 服务名

```
location /api/{
		#proxy_pass http://172.16.238.11:8080;
		proxy_pass http://java:8080;
	}
```

docker network ls

查看服务 ip
docker inspect 容器名

## 运行

```
docker-compose up
docker-compose down
docker-compose start
```

## code
[代码](https://github.com/ScorpionJay/docker-compose-sample)