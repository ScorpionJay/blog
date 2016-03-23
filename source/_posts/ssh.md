title: git ssh
date: 2015-10-06 14:02:59
tags:
- hexo
- git
---
ssh （安全外壳协议）
<!--more-->





###	ssh 
	git ssh
	github上拉代码的时候一般使用git clone https url，但是需要输入密码。
	使用ssh就不要了，需要设置下。

![](/img/git.png)[下载](http://www.git-scm.com/download)

	1.运行git bash客户端,输入
	cd ~/.ssh
	ls
	检查id_ras.pub是否存在
	
	2.创建SSH key
	ssh-keygen -t rsa -C "你的邮箱" -f ~/.ssh/github
	
	代码参数含义：
	-t 指定密钥类型，默认是 rsa ，可以省略。
	-C 设置注释文字，比如邮箱。
	-f 指定密钥文件存储文件名。


	接着又会提示你输入两次密码（该密码是你push文件的时候要输入的密码，而不是github管理者的密码），
	$ ssh-keygen -t rsa -C "你的邮箱@qq.com"
	Generating public/private rsa key pair.
	Enter file in which to save the key (/c/Users/Jay/.ssh/id_rsa):
	Created directory '/c/Users/Jay/.ssh'.
	Enter passphrase (empty for no passphrase):
	Enter same passphrase again:
	Your identification has been saved in /c/Users/Jay/.ssh/id_rsa.
	Your public key has been saved in /c/Users/Jay/.ssh/id_rsa.pub.
	The key fingerprint is:
	SHA256:DcBQ79ZbtThXSRZK+8KO43+V+/O4mps3oQjoofQaEsA xxxx@qq.com
	The key's randomart image is:
	+---[RSA 2048]----+
	|    .+o      . +.|
	|.     .o    . = .|
	|.E      o    o...|
	| .     . +  .o.o |
	|  .    .S o +oo..|
	|   .. o..  oooo..|
	|  ...+ . ..+ o .o|
	|   ...o   o ooo= |
	|    ..     .*=+o*|
	+----[SHA256]-----+


	添加你的 SSH key 到 github上面去
	https://github.com/settings/ssh

	Jay@VAIO MINGW64 ~
	$ ssh -T git@github.com
	The authenticity of host 'github.com (192.30.252.128)' can't be established.
	RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
	Are you sure you want to continue connecting (yes/no)?
	Host key verification failed.

	需要输入yes，默认尽然不是yes

	Jay@VAIO MINGW64 ~
	$ ssh -T git@github.com
	The authenticity of host 'github.com (192.30.252.129)' can't be established.
	RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
	Are you sure you want to continue connecting (yes/no)? yes
	Warning: Permanently added 'github.com,192.30.252.129' (RSA) to the list of known hosts.
	Hi s9013! You've successfully authenticated, but GitHub does not provide shell access.

### 配置多个ssh
	一个访问github 一个访问gitcafe

	在.ssh文件夹下新建config文件，内容如下

	Host github
	    HostName github.com
	    User git
	    IdentityFile ~/.ssh/github
	 
	Host gitcafe
	    HostName gitcafe.com
	    User git
	    IdentityFile ~/.ssh/id_rsa

### 测试
~~~bash
Jay@VAIO MINGW64 ~/Desktop
$ ssh -T git@github
Hi s9013! You've successfully authenticated, but GitHub does not provide shell access.

Jay@VAIO MINGW64 ~/Desktop
$ ssh -T git@gitcafe
Hi scorpion! You've successfully authenticated, but GitCafe does not provide shell access.
~~~