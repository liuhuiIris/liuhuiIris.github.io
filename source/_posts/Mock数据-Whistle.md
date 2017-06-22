---
title: Mock数据-Whistle
date: 2017-06-22 19:17:48
tags: Mock
---

# 1.简介

whistle继承了Fiddler、Charle的一些优秀设计(如Fiddler请求数据的展示界面)，这两者分别是Windows、macOS平台的优秀代理工具。但whistle不是Fiddler、Charles的复制品，whistle有自己独特丰富的功能，如日志系统log、移动调试工具weinre、插件机制等。whistle也对操作请求和响应的方式做了改进，通过扩展系统hosts的配置方式及匹配方式，同时支持域名、正则和路径的匹配方式，让所有请求和响应的操作都可以通过类似hosts的配置方式实现，最新版whistle更是支持带端口号的host配置。不仅如此，开发者也可以通过whistle的插件扩展实现自身的个性化功能。实践证明这种方式使用起来方便，用户体验非常好。

# 2.安装启动

## 2.1 安装node
直接给链接好了,[node下载](https://nodejs.org/en/download/),不再赘述

## 2.2 安装Whistle
Node安装成功后，执行如下npm命令安装whistle （Mac或Linux的非root用户需要在命令行前面加sudo，如：sudo npm install -g whistle）

```bash
$ npm install -g whistle
```

安装完成后检查一下,如果正常显示帮助信息,则表示安装成功
```bash
$ w2 help

Usage: w2 <command> [options]

  Commands:

    run       Start a front service
    start     Start a background service
    stop      Stop current background service
    restart   Restart current background service
    help      Display help information

  Options:

    -h, --help                                      output usage information
    -d, --debug                                     debug mode
    -l, --localUIHost [hostname]                    local ui host(local.whistlejs.com by default)
    -n, --username [username]                       login username
    -w, --password [password]                       login password
    -S, --storage [newStorageDir]                   the new local storage directory
    -C, --copy [storageDir]                         copy storageDir to newStorageDir
    -p, --port [port]                               whistle port(8899 by default)
    -m, --middlewares [script path or module name]  express middlewares path(as: xx,yy/zz.js)
    -u, --uipath [script path]                      web ui plugin path
    -t, --timeout [ms]                              request timeout(36000 ms by default)
    -s, --sockets [number]                          max sockets(12 by default)
    -V, --version                                   output the version number
    -c, --command <command>                         command parameters ("node --harmony")
```

## 2.3 启动whistle
启动whistle:
```bash
w2 start
```
Note: 如果要防止其他人访问配置页面，可以在启动时加上登录用户名和密码 -n yourusername -w yourpassword。

重启whsitle:
```bash
$ w2 restart
```

停止whistle:
```bash
$ w2 stop
```

调试模式启动whistle(主要用于查看whistle的异常及插件开发):
```bash
$ w2 run
```

启动完whistle后，最后一步需要配置代理。

## 2.4 配置代理
**配置信息**

1) 代理服务器：127.0.0.1(如果部署在远程服务器或虚拟机上，改成对应服务器或虚拟机的ip即可)
2) 默认端口：8899(如果端口被占用，可以在启动是通过 -p 来指定新的端口，更多信息可以通过执行命令行 w2 help (v0.7.0及以上版本也可以使用w2 help) 查看)

**代理配置方式**

[安装Chrome插件](https://chrome.google.com/webstore/detail/whistle/bokhoonoeoodkdhbdhlgaodjdcnbcpdl)并启用

详细的不多说,就拿本地静态json作为mock数据吧,目前只测试过get请求,以后用到再补充
```bash
pattern resBody://filepath

e.g. http://192.168.1.205:5001/summary resBody:///Users/cloudwiz/Desktop/cloudw_project/data/summary.json

```
