---
title: shadowsocks
date: 2018-11-09 15:01:35
tags:
  - linux
---

shadowsocks

<!--more-->

[code](https://github.com/shadowsocks/shadowsocks/tree/master)

# shadowsocks

## Server

### Install

Debian / Ubuntu:

    apt-get install python-pip
    pip install git+https://github.com/shadowsocks/shadowsocks.git@master

CentOS:

    yum install python-setuptools && easy_install pip
    pip install git+https://github.com/shadowsocks/shadowsocks.git@master

For CentOS 7, if you need AEAD ciphers, you need install libsodium

```
dnf install libsodium python34-pip
pip3 install  git+https://github.com/shadowsocks/shadowsocks.git@master
```

Linux distributions with [snap](http://snapcraft.io/):

    snap install shadowsocks

Windows:

See [Install Shadowsocks Server on Windows](https://github.com/shadowsocks/shadowsocks/wiki/Install-Shadowsocks-Server-on-Windows).

### Usage

    ssserver -p 443 -k password -m aes-256-cfb

To run in the background:

    sudo ssserver -p 443 -k password -m aes-256-cfb --user nobody -d start

To stop:

    sudo ssserver -d stop

To check the log:

    sudo less /var/log/shadowsocks.log

Check all the options via `-h`. You can also use a [Configuration] file
instead.

If you installed the [snap](http://snapcraft.io/) package, you have to prefix the commands with `shadowsocks.`,
like this:

    shadowsocks.ssserver -p 443 -k password -m aes-256-cfb

### Usage with Config File

[Create configuration file and run](https://github.com/shadowsocks/shadowsocks/wiki/Configuration-via-Config-File)

To start:

    ssserver -c /etc/shadowsocks.json


    You can use a configuration file instead of command line arguments.

    Create a config file /etc/shadowsocks.json. Example:

    {
        "server":"my_server_ip",
        "server_port":8388,
        "local_address": "127.0.0.1",
        "local_port":1080,
        "password":"mypassword",
        "timeout":300,
        "method":"aes-256-cfb",
        "fast_open": false
    }
    Explanation of the fields:

    Name	Explanation
    server	the address your server listens
    server_port	server port
    local_address	the address your local listens
    local_port	local port
    password	password used for encryption
    timeout	in seconds
    method	default: "aes-256-cfb", see Encryption
    fast_open	use TCP_FASTOPEN, true / false
    workers	number of workers, available on Unix/Linux
    To run in the foreground:

    ssserver -c /etc/shadowsocks.json
    To run in the background:

    ssserver -c /etc/shadowsocks.json -d start
    ssserver -c /etc/shadowsocks.json -d stop

## client

```
启动shadowsocks
sudo sslocal -c /etc/shadowsocks/config.json
{
    "server":"ip",
    "server_port":端口,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"密码",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false,
    "workers": 1,
    "prefer_ipv6": false
}

```

chrome 插件 SwitchySharp

```
SOCKS Host	127.0.0.1
Port	1080
SOCKS v5
```
