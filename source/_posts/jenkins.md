---
title: jenkins
date: 2018-11-27 11:58:42
tags:
  - 工具
---

自动化部署工具

<!--more-->

- general
- 源码管理
- 构建触发器
- 构建
- 构建后操作

执行 shell

```
# 安装node_modules
#cnpm i

# 打包
npm run build:prod

#压缩
tar -czvf dist.tar.gz dist docker-compose.yml nginx.conf
```

构建后操作 send files or execute commands over SSH

```
SSH Server
    Name xx

    Transfers
        Transfer Set
            Source files        dist.tar.gz  #发送的文件
            Remove prefix                    #去除的前缀
            Remote directory    /jenkins/pc  #发送到的路径
            Exec command
                # 执行命令
                cd /home/jenkins/vmy-pc
                docker-compose down
                #rm dist nginx.conf docker-commpose.yml
                rm -rf `ls |grep -v dist.tar.gz`
                tar -xzvf dist.tar.gz
                rm dist.tar.gz  -rf
                docker-compose up -d
```
