---
layout: post
title: "shadowsocks guide"
date: 2015-04-24 22:29:10 +0800
comments: true
categories: GFW
---

shadowsocks基于Socket通信，利用远端服务器做代理，实现翻墙。

###安装

#####PyPI
```
pip install shadowsocks
```
#####Debian/Ubuntu
```
wget -O- http://shadowsocks.org/debian/1D27208A.gpg | sudo apt-key add -
echo "deb http://shadowsocks.org/debian wheezy main" >> /etc/apt/sources.list
```

###配置
```
{
    "server":"my_server_ip",
    "server_port":8388,
    "local_port":1080,
    "password":"barfoo!",
    "timeout":600,
    "method":"table"
}
```
为了支持IPV6，可以将Server地址写为`::`如
```
{
    "server":"::",
    "server_port":1024,
    "local_port":1080,
    "password":"aiyanxu",
    "timeout":600,
    "method":"aes-256-cfb"
}
```
###启动
#####服务器端
```
ssserver -c config-file
```
#####客户端
```
sslocal -c config-file
```

