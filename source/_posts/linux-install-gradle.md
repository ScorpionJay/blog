title: linux install gradle
date: 2015-10-13 10:13:10
tags:

- linux
- java

---

install gradle

<!--more-->

## download

[download gradle](https://gradle.org/install/#manually)

## extract and move

```
$ mkdir /opt/gradle
$ unzip -d /opt/gradle gradle-4.10-bin.zip
$ ls /opt/gradle/gradle-4.10
LICENSE  NOTICE  bin  getting-started.html  init.d  lib  media
```

## config

```
vi /etc/profile
$ export PATH=$PATH:/opt/gradle/gradle-4.10/bin
```

## excute

```
source /etc/profile
```

## validate

```
gradle -version
```

bingo
