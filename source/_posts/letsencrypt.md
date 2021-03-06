---
title: letsencrypt
date: 2018-08-28 10:55:58
tags:
---

use letsencrypt to configure nginx https

<!--more-->

```
download certbot
git clone https://github.com/certbot/certbot.git
```

```
#配置 nginx 、验证域名所有权,
#这一步是为了通过 Let’s Encrypt 的验证，验证 nway.top这个域名是属于我的管理之下。
location ^~ /.well-known/ {
	default_type "text/plain";
	root /home/api/https/;
}
```

```
./certbot-auto certonly --webroot -w /home/api/https -d  nway.top
```

```
IMPORTANT NOTES:
- Congratulations! Your certificate and chain have been saved at:
/etc/letsencrypt/live/m.shanghaim.net/fullchain.pem
Your key file has been saved at:
/etc/letsencrypt/live/m.shanghaim.net/privkey.pem
Your cert will expire on 2018-09-07. To obtain a new or tweaked
version of this certificate in the future, simply run certbot-auto
again. To non-interactively renew *all* of your certificates, run
"certbot-auto renew"
- If you like Certbot, please consider supporting our work by:

Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
Donating to EFF:                    https://eff.org/donate-le
```

```
nginx 配置ssl
listen 443 ssl;
server_name nway.top;
index index.html;
root  /home/wwwroot;

ssl_certificate      /etc/letsencrypt/live/nway.top/fullchain.pem;
ssl_certificate_key  /etc/letsencrypt/live/nway.top/privkey.pem;
```

```
http转向https
server {
        listen       80;
        server_name  localhost;
		rewrite ^(.*) https://$server_name$1 permanent;
｝
```

```
过期执行
./certbot-auto renew
```

## 出问题了

nginx 配置

```
server {
    listen 80;
    server_name m.shanghaim.net;
    # rewrite ^(.*) https://$server_name$1 permanent; # http转https
    #配置 nginx 、验证域名所有权,
    #这一步是为了通过 Let’s Encrypt 的验证，验证域名是属于我的管理之下。
    location ^~ /.well-known/ {
            root /home/jay/html/;
    }
}
~~~

```

./certbot-auto certonly --standalone --email jay.wang.scorpion@gmail.com -d m.shanghaim.net

```

```

快到期执行
更新证书
./certbot-auto renew

重启 nginx
nginx -s reload

```

## REF

- [https://letsencrypt.org/](https://letsencrypt.org/)
- [https://certbot.eff.org/lets-encrypt/centos6-nginx](https://certbot.eff.org/lets-encrypt/centos6-nginx)
- [HTTPS 简介及使用官方工具 Certbot 配置 Let’s Encrypt SSL 安全证书详细教程](https://linuxstory.org/deploy-lets-encrypt-ssl-certificate-with-certbot/)
```
