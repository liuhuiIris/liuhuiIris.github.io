---
title: mysql数据库密码安全策略
date: 2018-11-30 12:00:17
tags: security mysql
---

# 1.安全审计要求

由于安全审计要求，建议设置数据库密码复杂策略，启用密码复杂度验证函数，至少满足锁定时间大于3分钟，最长使用天数小于180天，可重用次数小于5次）；更改弱口令用户的密码，长度至少八位，由字母、数字或特殊字符混合组成，禁止用户名和口令相同

# 2.mysql5.6 参考文档

连接限制:

https://dev.mysql.com/doc/refman/5.6/en/connection-control.html

密码复杂度设置：

https://dev.mysql.com/doc/refman/5.6/en/validate-password.html 

my.cnf文件说明：

https://dev.mysql.com/doc/refman/5.6/en/option-files.html

可通过以下命令查看部分参数内容

```bash
ps aux | grep mysql

liuhui           15695   1.2  0.0  2443044    820 s000  S+   11:47上午   0:00.00 grep --color=auto --exclude-dir=.bzr --exclude-dir=CVS --exclude-dir=.git --exclude-dir=.hg --exclude-dir=.svn mysql
_mysql           96213   0.0  0.0  2831668   1364   ??  Ss   三02下午   0:10.16 /usr/local/mysql/bin/mysqld --user=_mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data --plugin-dir=/usr/local/mysql/lib/plugin --log-error=/usr/local/mysql/data/mysqld.local.err --pid-file=/usr/local/mysql/data/mysqld.local.pid
```
案例如下：
> 注意可能有些配置在用户机器上不生效，导致mysql无法正常启动

> 此时注释掉相关报错参数，重启mysql

> 改为通过官网中命令形式进行设置
```bash
[liuhui@cloudwiz] $ vi /etc/my.cnf

[base]
basedir = /usr/local/mysql
datadir = /usr/local/mysql/data
port = 3306
socket = /tmp/mysql.sock
log_error = /usr/local/mysql/data/mysqld.local.err
pid-file = /usr/local/mysql/data/mysqld.local.pid
user = mysql

sql_mode = NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES

[client]
port = 3306
socket = /tmp/mysql.sock

[mysqld]
# localhost work, but costumer's host dosen't work, and I don't know why
default_password_lifetime = 180

# load plugin of validate_password.so
plugin-load=validate_password.so
validate_password_length = 8
validate_password_policy = 1
validate-password=FORCE_PLUS_PERMANENT

# load plugin of connetion_control.so
 plugin-load-add = connection_control.so
# force enable plugin
# connection-control = FORCE_PLUS_PREMANENT
# connection-control-failed-login-attempts = FORCE_PLUS_PREMANENT
# connection_control_failed_connections_threshold = 3
# connection_control_max_connection_delay = 2147483647
# connection_control_min_connection_delay = 10000
```

# 3.mysql 5.6 与 5.7的区别

mysql5.6的不会对之前创建的用户造成影响，不改密码也OK

mysql5.7的会检测之前的用户，如果密码强度不够，会强制要求修改密码
