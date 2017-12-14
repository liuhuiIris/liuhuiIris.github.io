---
title: centos6添加node系统server
date: 2017-12-14 20:35:39
tags: centos server
---

文章来源: [CentOS5.6下离线部署NodeJS环境和工程代码，并添加forever的开机自启动服务](http://www.alliedjeep.com/127869.htm)

# 1. centos6 启动/关闭服务
```bash
service server start/stop/restart
```

# 2. 添加node server
这段脚本含义有心情再补充了。。。
```bash
# sdu_server 是为自定义服务起的名字,可任意
vim /etc/init.d/sdu_server

#!/bin/bash
# chkconfig:345 99 01 这一串不知道干嘛
# description: 图书查询服务
# 启动服务的脚本路径 /opt/project/sdulibrary/library_db
# 使用node forever 管理node server
DIR='/opt/project/sdulibrary/library_db'

function start_app {
  forever start -a "$DIR/getlist.js"
}
function stop_app {
  forever stop "$DIR/getlist.js"
}

case $1 in
  start)
    start_app ;;
  stop)
    stop_app ;;
  restart)
    stop_app
    start_app
    ;;
  *)
  echo "usage: clearstonecc {start|stop}" ;;
esac
exit 0
```

# 3. 启动自定义服务

```bash
service sdu_server start
```
