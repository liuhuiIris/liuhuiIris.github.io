---
title: windows下的Nginx
date: 2017-01-09 20:49:01
tags: 代理
---

# 1. 简介

    Nginx ("engine x") 是一个高性能的HTTP和反向代理服务器，也是一个IMAP/POP3/SMTP服务器。
    Nginx是由Igor Sysoev为俄罗斯访问量第二的Rambler.ru站点开发的，第一个公开版本0.1.0发布于2004年10月4日。
    其将源代码以类BSD许可证的形式发布，因它的稳定性、丰富的功能集、示例配置文件和低系统资源的消耗而闻名。
    2011年6月1日，nginx 1.0.4发布。

    Nginx是一款轻量级的Web 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器，并在一个BSD-like 协议下发行。
    由俄罗斯的程序设计师Igor Sysoev所开发，供俄国大型的入口网站及搜索引擎Rambler（俄文：Рамблер）使用。
    其特点是占有内存少，并发能力强，事实上nginx的并发能力确实在同类型的网页服务器中表现较好，
    中国大陆使用nginx网站用户有：百度、京东、新浪、网易、腾讯、淘宝等。

# 2. windows下安装Nginx
[Nginx官网安装](http://nginx.org/)

    --->选择合适的版本安装
    --->解压到自定义的路径下

# 3. 配置环境变量
    系统path--->添加自定义的路径

# 4. 相关命令
    nginx   默认端口号为80，若被占用，可改配置或关闭占用的进程
    nginx -s reload|reopen|stop|quit  #重新加载配置|重启|停止|退出 nginx

# 5. 预览
    在浏览器中访问本地ip即可

# 6. 关闭占用端口号80进程的方法
    命令行查找占用80端口的进程  netstat -ano|findstr 80
    找到相应的pid
    打开任务管理器（快捷键 Ctrl+Shift+Esc）
    根据pid,关闭进程

    通常占用80端口的程序有：迅雷、IIS。
    可去IIS管理其中修改网站端口号或者关闭网站。

# 7. 乱乱配置反向代理
    /****************** nginx.conf ***********************/
    
    #user  nobody;
    # user root owner;
    worker_processes  1;

    #error_log  logs/error.log;
    #error_log  logs/error.log  notice;
    #error_log  logs/error.log  info;

    #pid        logs/nginx.pid;

    events {
        worker_connections  1024;
    }


    http {
        include       mime.types;
        default_type  application/octet-stream;

        #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
        #                  '$status $body_bytes_sent "$http_referer" '
        #                  '"$http_user_agent" "$http_x_forwarded_for"';

        #access_log  logs/access.log  main;

        sendfile        on;
        #tcp_nopush     on;

        #keepalive_timeout  0;
        keepalive_timeout  65;

        #gzip  on;
        include D:/nginx-1.10.2/conf.d/*.conf;

    }









