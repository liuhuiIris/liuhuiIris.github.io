---
title: rsyslog收集日志
date: 2018-11-30 14:33:53
tags: linux rsyslog
---

> 以日志服务器为10.44.85.15为例，日志源机器为10.44.85.16

# 1. 在10.44.85.16上修改/etc/rsyslog.conf

```bash
$ModLoad imuxsock # provides support for local system logging (e.g. via logger command)
# $ModLoad imjournal # provides access to the systemd journal

 File to store the position in the journal
$IMJournalStateFile imjournal.state


#### RULES ####

# Log all kernel messages to the console.
# Logging much else clutters up the screen.
#kern.*                                                 /dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none;cron.none                /var/log/messages

# The authpriv file has restricted access.
authpriv.*                                              /var/log/secure

# Log all the mail messages in one place.
mail.*                                                  -/var/log/maillog


# Log cron stuff
cron.*                                                  /var/log/cron

# Everybody gets emergency messages
*.emerg                                                 :omusrmsg:*

# Save news errors of level crit and higher in a special file.
uucp,news.crit                                          /var/log/spooler

# Save boot messages also to boot.log
local7.*                                                /var/log/boot.log

# 将自定义服务日志发送至日志服务器
$ModLoad imfile
$InputFilePollInterval 10

$InputFileName         /var/log/webfront/webfront.log      #要监控的日志文件路径
$InputFileTag          webfront-info:                      # 定义文件标签 ，注意最后是冒号：
$InputFileStateFile    state-webfront-info                 #定义状态文件
$InputRunFileMonitor                                       #激活读取，可以设置多组日志读取，每组结束时设置本参数

# ### begin forwarding rule ###
# The statement between the begin ... end define a SINGLE forwarding
# rule. They belong together, do NOT split them. If you create multiple
# forwarding rules, duplicate the whole block!
# Remote Logging (we use TCP for reliable delivery)
#
# An on-disk queue is created for this action. If the remote host is
# down, messages are spooled to disk and sent when it is up again.
#$ActionQueueFileName fwdRule1 # unique name prefix for spool files
#$ActionQueueMaxDiskSpace 1g   # 1gb space limit (use as much as possible)
#$ActionQueueSaveOnShutdown on # save messages to disk on shutdown
#$ActionQueueType LinkedList   # run asynchronously
#$ActionResumeRetryCount -1    # infinite retries if host is down
# remote host is: name/ip:port, e.g. 192.168.0.1:514, port optional
#*.* @@remote-host:514
*.* @@10.44.85.15:514
# ### end of the forwarding rule ###

```

> 一般默认配置即为发送系统日志，可以不做修改，注意最后
> *.* @@remote-host:514 修改为目标日志服务器ip

# 2. 重启rsyslog

方法1：

```bash
/etc/init.d/rsyslog restart #修改配置文件后一定要重启rsyslog服务

/etc/init.d/rsyslog status  #可查看服务状态
```

方法2：
```bash
service rsyslog restart #修改配置文件后一定要重启rsyslog服务

service rsyslog status  #查看服务状态
```

# 3. 在10.44.85.15上修改/etc/rsyslog.conf

```conf
$ModLoad imuxsock
$ModLoad imjournal
$ModLoad immark
$ModLoad imudp
$UDPServerRun 514
$ModLoad imtcp
$InputTCPServerRun 514
$WorkDirectory /var/lib/rsyslog
$AllowedSender tcp, 10.44.85.0/24
$ActionFileDefaultTemplate RSYSLOG_TraditionalFileFormat
$template Remote,"/var/log/%fromhost-ip%/%fromhost-ip%_%$YEAR%-%$MONTH%-%$DAY%.log"
:fromhost-ip, !isequal, "127.0.0.1" ?Remote
$IncludeConfig /etc/rsyslog.d/*.conf
$OmitLocalLogging on
$IMJournalStateFile imjournal.state

*.info;mail.none;authpriv.none;cron.none	/var/log/rsyslog
authpriv.*					/var/log/secure
mail.*						-/var/log/maillog
cron.*						/var/log/corn
*.emerg						:omusrmsg:*
uucp,news.crit					/var/log/spooler
local7.*					/var/log/boot.log
```

# 4. 重启rsyslog

方法1：

```bash
/etc/init.d/rsyslog restart #修改配置文件后一定要重启rsyslog服务

/etc/init.d/rsyslog status  #可查看服务状态
```

方法2：
```bash
service rsyslog restart #修改配置文件后一定要重启rsyslog服务

service rsyslog status  #查看服务状态
```

# 5. 检验日志收集

在日志服务器10.44.85.15上查看通过rsyslog收集的10.44.85.16的日志

日志路径：
```
cd /var/log/10.44.85.16/
```
