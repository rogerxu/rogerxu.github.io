---
layout: post
title: Shadowsocks
---

* [Official Site](http://shadowsocks.org/)
* [Wiki](https://github.com/shadowsocks/shadowsocks/wiki)

## Server

### Prepare

    $ su
    $ yum clean all
    $ yum update
    $ yum grouplist
    $ yum groupinfo "Development tools"
    $ yum groupinstall "Development tools"

### Python

#### Install

Install python-pip

    $ yum install python-setuptools
    $ easy_install pip

Install M2Crypto for encryption methods

    $ yum install swig
    $ yum install m2crypto
    $ yum install supervisor

Install gevent for better performance

    $ yum install python-devel
    $ yum install libevent
    $ easy_install greenlet
    $ pip install gevent

#### Upgrade

Make sure the old packages are uninstalled.

    $ yum update
    $ easy_install -U pip
    $ pip list -o
    $ pip install -U shadowsocks

#### Configuration

    $ mkdir shadowsocks
    $ vim shadowsocks/config.json

`config.json`

```json
{
    "server": "0.0.0.0",
    "server_port": 8388,            // server port
    "local_address": "127.0.0.1",   // local address
    "local_port": 1080,             // local port
    "password": "s**",
    "timeout": 300,                 // in seconds
    "method": "aes-256-cfb",        // encryption method, "rc4-md5", "aes-256-cfb" etc. Default is "table"
    "fast_open": false,             // If both of your server and client are deployed on Linux 3.7+, you can turn on fast_open for lower latency.
    "workers": 2
```
To run in the foreground

    $ ssserver -c /etc/shadowsocks/config.json

To run in the background

    $ ssserver -c /etc/shadowsocks/config.json -d start
    $ ssserver -c /etc/shadowsocks/config.json -d stop

#### Run Server

To run in the foreground

    $ ssserver -p 443 -k password -m aes-256-cfb

To run in the background

    $ sudo ssserver -p 443 -k password -m aes-256-cfb --user nobody --workers 2 -d start

To check the log

    $ sudo less /var/log/shadowsocks.log

### Stop Server

    $ sudo ssserver -d stop


### Node.js

Deprecated. The memory performance is not good.

#### Install

    $ yum install nodejs npm
    $ npm --version
    $ npm install -g shadowsocks

#### Configuration

    $ mkdir shadowsocks
    $ vim shadowsocks/config.json

#### Run Server

    $ cd shadowsocks
    $ nohup ssserver > log &
    $ exit

#### Stop Server

    $ ps -l
    $ kill -15 ${PID}


## Client

### Windows

shadowsocks-csharp

Windows 8 or above: `shadowsocks-win-dotnet4.0-2.3.zip`
Windows 7 or below: `shadowsocks-win-2.3.zip`

`gui-config.json`

```json
{
  "configs" : [
    {
      "server" : "45.62.103.223",
      "server_port" : 443,
      "password" : "savageboy",
      "method" : "aes-256-cfb",
      "remarks" : "Micro-64"
    }
  ],
  "index" : 0,
  "global" : false,
  "enabled" : true,
  "shareOverLan" : false,
  "isDefault" : false,
  "localPort" : 1080
}
```

### Android

