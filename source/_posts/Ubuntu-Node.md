---
title: Ubuntu-Node
date: 2017-06-14 18:14:07
tags: Ubuntu
---

# 1. Nodejs

Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。

Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效。 

Node.js 的包管理器 npm，是全球最大的开源库生态系统。

# 2. 安装node,顺便装了npm
``` bash
$ sudo apt install nodejs-legacy
$ sudo apt install npm
```

安装完成后,查看版本号

``` bash
$ node -v
$ npm -v
```

# 3. hello world
```bash
$ node
console.log("Hello World!");
```

# 4. nodejs 卸载
``` bash
$ sudo apt-get remove nodejs
```
