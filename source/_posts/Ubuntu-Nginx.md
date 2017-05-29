---
title: 'Ubuntu--Nginx'
date: 2017-05-26 21:46:46
tags: Ubuntu
---

# 1. Ubuntu简介

在leader的‘淫威’之下，走上了linux的不归路，不负责任地选择了这么个操作系统。

言归正传，Ubuntu（友帮拓、优般图、乌班图）是一个以桌面应用为主的开源GNU/Linux操作系统，Ubuntu 是基于Debian GNU/Linux，支持x86、amd64（即x64）和ppc架构，由全球化的专业开发团队（Canonical Ltd）打造的。

# 2. Linux简单命令

修改默认用户名

    sudo vim /etc/hostname

修改密码

    sudo passwd root/username

# 3. Nginx

安装Nginx

    sudo apt-get install nginx

查看修改配置文件

    sudo vim /etc/nginx/sites-available/default

    server { 
      #80指端口号，可以修改为自己所需要的
      listen 80 default_server; 
      #还有这里 同样改为你想要的监听端口 
      listen [::]:80 default_server ipv6only=on; 

      ...
    }

查看nginx是否安装成功

    在浏览器中输入 localhost, 即可看到nginx默认欢迎页。撒花~~~

nginx常用命令

    nginx -s stop   >>关闭nginx
    nginx -s reload >>重读配置文件
