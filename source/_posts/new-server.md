---
title: new server
date: 2019-12-25 11:50:10
tags:
  - linux
---

新服务器配置

<!--more-->

## nginx

```
yum install nginx

cd /etc/nginx
nginx
```

## node

```
wget https://nodejs.org/dist/v12.14.0/node-v12.14.0-linux-x64.tar.xz

cd /opt
mkdir node

tar xvf node-v12.14.0-linux-x64.tar.xz

ln -s /opt/node/bin/node /usr/local/bin/node
ln -s /opt/node/bin/npm /usr/local/bin/npm

npm -v

node -v

npm config set registry http://registry.npm.taobao.org/
```

pm2

```
npm install -g pm2

ln -s /opt/node/bin/pm2 /usr/local/bin/
```

## docker

```
https://docs.docker.com/install/linux/docker-ce/centos/

curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh


```

## docker-compose

```
https://docs.docker.com/compose/install/

sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

mv docker-compose-Linux-x86_64 /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```

## git

```
yum install git
```

## ypai

```
https://github.com/YMFE/yapi

git clone https://github.com/YMFE/yapi.git


```

## https

```
https://github.com/certbot/certbot.git

# http to https
server {
    listen 80;
    server_name m.shanghaim.net;
	  #配置 nginx 、验证域名所有权,
        #这一步是为了通过 Let’s Encrypt 的验证，验证 nway.top这个域名是属于我的管理之下。
        location ^~ /.well-known/ {
                #default_type "text/plain";
                 root /home/jay/html/;
         }
}


./certbot-auto certonly --webroot -w /home/jay/html -d  m.shanghaim.net


IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/m.shanghaim.net/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/m.shanghaim.net/privkey.pem
   Your cert will expire on 2020-03-24. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot-auto
   again. To non-interactively renew *all* of your certificates, run
   "certbot-auto renew"
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le


```

```
server{
	listen 443 ssl;
	server_name m.shanghaim.net;

	ssl_certificate      /etc/letsencrypt/live/m.shanghaim.net/fullchain.pem;
	ssl_certificate_key  /etc/letsencrypt/live/m.shanghaim.net/privkey.pem;

	root /home/jay/html;

  location / {
        try_files $uri /index.html;
  }
}

```

## 启动 docker

```
systemctl start docker
```

> protal

```
server {
        listen       80;
        server_name  docker.shanghaim.net;


	location / {
		#root /home/ht;
		#index index.html;
		#try_files $uri /index.html;
		proxy_pass http://localhost:9990;
		#proxy_pass http://sts.api.qcloud.com;
	}
}
```

http://docker.shanghaim.net/

> mongodb

```
use one

db.createUser(
{
    user: "user",
    pwd: "pwd",
    roles: [ { role: "readWrite", db: "one" },
             { role: "read", db: "reporting" } ]
  }
)
```

```
	location ^~/fullstack/ {
		rewrite ^/fullstack/(.*)$ /$1 break;
		proxy_set_header X-Real-IP $remote_addr; # 真实ipip
		proxy_pass http://0.0.0.0:4000;
	}
```
