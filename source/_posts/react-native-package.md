---
title: React Native Generating Signed APK 
date: 2016-06-22 13:04:31
tags:
- react native
---

RN生成签名apk
<!--more-->
# 生成一个签名密钥

[数字身份](https://zh.wikipedia.org/wiki/%E6%95%B0%E5%AD%97%E8%BA%AB%E4%BB%BD)

[keytool百度百科](http://baike.baidu.com/link?url=HqFC2A03zv86lOJZc0TSyp6CtnQ8boPP15j6ggLnc32pjNod_ZIA7qIX7lgkvyeMNJJB5CfaKRR97KYKIBQokq)

### 使用keytool命令生成一个私有密钥
~~~sh
 keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
~~~

这条命令会要求你输入密钥库（keystore）和对应密钥的密码，然后设置一些发行相关的信息。最后它会生成一个叫做my-release-key.keystore的密钥库文件。

在运行上面这条语句之后，密钥库里应该已经生成了一个单独的密钥，有效期为10000天。--alias参数后面的别名是你将来为应用签名时所需要用到的，所以记得记录这个别名。


参数详解： 
-dname "CN=xx,OU=xx,O=xx,L=xx,ST=xx,C=xx"  dn名为"CN=..." 
-alias scent                别名为scent的一个证书 
-keyalg 
     DSA RSA                    DSA或RSA算法(当使用-genkeypair参数) 
     DES DESede AES      DES或DESede或AES算法(当使用-genseckey参数) 
-keysize 
     512 ~ 1024             密钥的长度为512至1024之间(64的倍数)(当使用-genkeypair和-keyalg DSA参数) 
     > 512                       密钥的长度大于512 (当使用-genkeypair和-keyalg RSA参数) 
     56                            密钥的长度为56 (当使用-genseckey和-keyalg DES 参数) 
     112 168                   密钥长度为112或168(当使用-genseckey和-keyalg DESede 参数) 
     128 192 256             密钥长度为128或192或256 (当使用-genseckey和-keyalg AES 参数) 
-keypass  123456              这个证书的私钥密码为123456 
-keystore prospectlib         证书库的名称为prospectlib 
-storepass 123456             证书库的访问密码为123456 
-validity  900            证书有效期为900天 
-file  scent.cer           从scent.cer文件导入证书，或者导出证书到scent.cer文件 
-v                               显示详细信息 
-rfc                            以Base64的编码格式打印证书 
-storetype JCEKS          密钥库的类型为JCEKS。常用的有JKS(默认),JCEKS(推荐),PKCS12,BKS,UBER。每个密钥库只可以是其中一种类型。

![](/../img/keytool.png)

在桌面上会生成my-release-key.keystore文件

把my-release-key.keystore文件放到你工程中的android/app文件夹下。
编辑~/.gradle/gradle.properties，添加如下的代码（注意把其中的****替换为相应密码）

![](/../img/gradle.properties.png)

~~~sh
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=*****
MYAPP_RELEASE_KEY_PASSWORD=*****
~~~

设置全局的gradle变量



## 添加签名到应用的gradle配置文件

编辑你工程目录下的android/app/build.gradle，添加如下的内容：
~~~sh
...
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        release {
            storeFile file(MYAPP_RELEASE_STORE_FILE)
            storePassword MYAPP_RELEASE_STORE_PASSWORD
            keyAlias MYAPP_RELEASE_KEY_ALIAS
            keyPassword MYAPP_RELEASE_KEY_PASSWORD
        }
    }
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release
        }
    }
}
...
~~~

如图：
![](/../img/build.gradle.png)


## 生成发行APK包

切换到android目录
~~~
cd android

gradlew assembleRelease
~~~

如图：

![](/../img/apk.png)

好像这个文件夹下要先有一个未签名的app-release-unaligned.apk 不懂 我执行了两次好了



## 测试应用的发行版本

~~~sh
gradlew installRelease
~~~

安装到模拟器中，不会自动打开app，自己手动打开，不用再开启js 服务了，因为你的代码全部打包到apk中了。


## 启用Proguard代码混淆来缩小APK文件的大小（可选）
Proguard是一个Java字节码混淆压缩工具，它可以移除掉React Native Java（和它的依赖库中）中没有被使用到的部分，最终有效的减少APK的大小。

重要：启用Proguard之后，你必须再次全面地测试你的应用。Proguard有时候需要为你引入的每个原生库做一些额外的配置。参见app/proguard-rules.pro文件。

要启用Proguard，编辑android/app/build.gradle文件：

![](/../img/yasuocode.png)

前后比较

![](/../img/yasuo.png)