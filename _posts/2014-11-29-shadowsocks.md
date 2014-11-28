---
layout: post
title: Shadowsocks
---

## Server

### Prepare

    $ su
    $ yum update
    $ yum grouplist
    $ yum groupinfo 'Development Tools'
    $ yum groupinstall "Development Tools"

### Python

Install

    $ yum install python-setuptools supervisor
    $ easy_install pip
    $ python --version
    $ pip install shadowsocks

Configuration

Run Server

Stop Server

### Node.js

Install

    $ yum install nodejs npm
    $ npm --version
    $ npm install -g shadowsocks

Configuration

    $ mkdir shadowsocks
    $ vim shadowsocks/config.json

`config.json`

```json
{
    "server": "0.0.0.0",
    "server_port": 8388,    // server port
    "local_port": 1080,     // local port
    "password": "s**",
    "timeout": 600,         // in seconds
    "method": "aes-256-cfb" // envryption method, "bf-cfb", "aes-256-cfb", "des-cfb", "rc4", etc. Default is "table"
```

Run Server

    $ cd shadowsocks
    $ nohup ssserver > log &
    $ exit

Stop Server

    $ ps -l
    $ kill -15 ${PID}

## Client

### Windows

### Android

