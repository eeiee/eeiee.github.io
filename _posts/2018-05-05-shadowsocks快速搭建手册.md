---
title: "shadowsocks 快速搭建手册，只需四步"
layout: post
category: net
tags: [ss]
excerpt: "shadowsocks 快速搭建手册，只需四步"
---
科学上网其实很简单，包教包会！一共只需要四步~
## 第1步：选择服务器
服务器的要求只有一个：可以访问被屏蔽网站。

一般选择国外服务器，常见的选择有三个：Linode,DigitalOcean和[搬瓦工](https://bandwagonhost.com/aff.php?aff=31008)。本文就以性价比最高，操作最方便的搬瓦工举例说明。

### 选择服务器型号
进入[搬瓦工](https://bandwagonhost.com/aff.php?aff=31008)首页,选择合适的VP。
![image](http://oi68.tinypic.com/148pssh.jpg)
本文选取了性价比最高的$19.99，点击进入订单页面。
### 优惠购买
在订单页面优惠码输入框中输入优惠码```BWH1ZBPVK```进行验证，验证成功后可在订单详情页中看到优惠信息。
![image](http://oi64.tinypic.com/2d8527p.jpg)
### 确认&支付
选择支付宝付款方式，支付成功后户会收到[搬瓦工](https://bandwagonhost.com/aff.php?aff=31008)订单详情。

## 第2步：配置服务器
进入[搬瓦工](https://bandwagonhost.com/aff.php?aff=31008)我的服务器列表页面，点击进入管理页面，找到服务器ip和登录端口。
![image](http://oi63.tinypic.com/whzkvq.jpg)
### 远程登录
打开终端，输入```ssh [ip] -p[port] -lroot```，输入登录密码登录。
### 安装ss
安装ss前需要先安装python和pip，之后通过pip安装ss。
下面介绍Linux下的服务安装。

#### Linux

Debian / Ubuntu:

```
apt-get install python-pip
pip install shadowsocks
```

CentOS:

```
yum install python-setuptools && easy_install pip
pip install shadowsocks
```

### 配置ss
ss启动时可通过命令参数或配置文件，本文采用配置文件的方式，好处就是修改方便。
创建/etc/shadowsocks.json文件，例如

```
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
```

其中主要配置```server```,```server_port```,```password```字段，其中server为上步购买的服务器ip地址，````server_port```可选择一个大于1024的端口，```password```填入连接密码，后面需要用到。
### 启动ss
```
nohup ssserver -c /etc/shadowsocks.json &
```
执行
```
ps -ef | grep ssserver
```
若结果中含有类似
```
/usr/bin/python /usr/bin/ssserver -c /etc/shadowsocks.json
```
输出，则表示服务启动成功。

## 第3步：配置客户端

### 下载客户端
[Windows](https://github.com/shadowsocks/shadowsocks-windows/releases/download/4.0.8/Shadowsocks-4.0.8.zip)   
[Mac](https://github.com/shadowsocks/ShadowsocksX-NG/releases/download/v1.7.1/ShadowsocksX-NG.1.7.1.zip)    
[Android](https://play.google.com/store/apps/details?id=com.github.shadowsocks)   
[iOS](https://itunes.apple.com/us/app/wingy-http-s-socks5-proxy-utility/id1178584911)   


### 配置客户端
运行客户端，找到新增服务器配置：
![image](http://oi63.tinypic.com/2cr269l.jpg)

地址一行填入服务器ip和端口号;

密码一行填入上步配置的连接密码;

加密方法选择和上步配置中保持一致;

配置完成后点击添加即可。

## 第4步：连接测试

访问下被屏蔽网站，如能访问，则表示成功；如不行，则需要确认下客户端代理功能是否打开哦~

## 参考
1. [ShadowSocks服务安装官方说明](https://github.com/shadowsocks/shadowsocks/blob/master/README.md)

2. [ShadowSocks配置文件说明](https://github.com/shadowsocks/shadowsocks/wiki/Configuration-via-Config-File)

3. [ShadowSocks客户端下载地址](https://shadowsocks.org/en/download/clients.html)



