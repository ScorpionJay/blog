---
title: linux
date: 2018-09-10 09:06:57
tags:
  - linux
---

linux note

<!--more-->

# linux

## shortcut key

- ctrl + c 终止
- ctrl + d 关闭终端
- ctrl + l 清屏幕
- ctrl + a 命令的最前面
- ctrl + e 命令的最后面

## directory

- /
- /bin
- /dev
- /etc
- /home
- /opt
- /var

## bash

| bash  | description                                        |
| ----- | -------------------------------------------------- |
| man   | help                                               |
| ls    | list directory contents                            |
| cd    | change directory                                   |
| pwd   | print name of current/working directory            |
| mkdir | make direcorys                                     |
| rm    | remove files or directories                        |
| mv    | move (rename) files                                |
| cp    | copy files and directories                         |
| cat   | concatenate files and print on the standard output |
| tail  | output the last part of files                      |

```
ls | grep -v test
```

## tar

压缩解压

- c
- v
- f
- x
- z

```
tar -czvf test.tar.gz test
tar -xzvf test.tar.gz
```

## nmap

扫描工具

---

## curl wget

lsof -i:8388
kill -9 pid
