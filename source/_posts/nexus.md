---
title: nexus
date: 2021-02-04 14:45:34
tags:
---

curl https://download.oracle.com/otn/java/jdk/8u281-b09/89d678f2be164786b292527658ca1605/jdk-8u281-linux-x64.tar.gz?AuthParam=1612408443_326313a279c0a9061ec69de4225b73fa -o jdk-8u281-linux-x64.tar.gz
tar -zxvf jdk-8u281-linux-x64.tar.gz
mv jdk1.8.0_281/ /opt/

vim /etc/profile

# java

export JAVA_HOME=/opt/jdk1.8.0_281
export PATH=$JAVA_HOME/bin:$PATH

source /etc/profile

下载 nexus https://www.sonatype.com/nexus/repository-oss-download

tar -zxvf nexus.tar.gz

[root@hecs-x-medium-2-linux-20200625130706 bin]# ./nexus start
WARNING: ****************************\*\*\*\*****************************
WARNING: Detected execution as "root" user. This is NOT recommended!
WARNING: ****************************\*\*\*\*****************************
Starting nexus

Nexus3 使用 root 报“WARNING: Detected execution as "root" user. This is NOT recommended!”

https://blog.csdn.net/u010741112/article/details/103920117

要么是在 bin 目录下的 nexus.rc 文件添加：
vim nexus.rc 加入 run_as_user=root
要么就是加入系统变量
vim /etc/profile 加入 export RUN_AS_USER=root
然而啥用都没有，启动还是一样的报这个提示。后面查看了一下启动脚本，即 vim nexus，里面有一句：run_as_root=true ，原来是此处直接给拦死了，故只要改成 run_as_root=false 就可以

可能大部分人都是使用./nexus start 吧，但这种是后台启动，看不到实时日志；用./nexus run 是实时启动可以看到日志，但是此启动方式不能退出回命令模式。 ./nexus status #查看启动状态， ./nexus stop #停止

2G 内存
