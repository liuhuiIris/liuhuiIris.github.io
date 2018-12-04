---
title: Clamav病毒防护软件安装
date: 2018-12-04 10:05:17
tags: security
---

参考网站：http://www.clamav.net/documents/installing-clamav#rhel

# 1. On CentOS:
```shell
# yum install -y epel-release

# yum install -y clamav 
```

On Community Enterprise Operating System (CentOS) the clamav package requires the Extra Packages for Enterprise Linux (EPEL) repository. On RedHat Enterprise Linux (RHEL) the EPEL release package has to be installed either manually or through RHN.

# 2. Run command to test
```shell
# clamscan /tmp
```

# 3. Questions
If there are some errors like this:
```bash
"LibClamAV Error: cli_loaddbdir(): No supported database files found in /var/lib/clamav

ERROR: Can't open file or directory"
```

You need to install some package to /var/lib/clamav

```shell
# cd /var/lib/clamav

# wget db.local.clamav.net/main.cvd

# wget db.local.clamav.net/daily.cvd

# wget db.local.clamav.net/bytecode.cvd
```

And then run the command again to test
```shell
# clamscan /tmp
```

# 4. Done
You can see the message, then done!
```shell
[root@znywhost clamav]# clamscan /tmp

/tmp/cloudwiz-user-stdout---supervisor-ks4Nv4.log: OK
/tmp/mysql-stdout---supervisor-9nkIv0.log: OK
/tmp/mysql-stderr---supervisor-DPkog8.log: OK
/tmp/opentsdb-stdout---supervisor-Pe5q7f.log.1: OK
/tmp/opentsdb-stdout---supervisor-Pe5q7f.log: OK
/tmp/umanager-stderr---supervisor-mgzixe.log: OK
/tmp/permission-stdout---supervisor-Y2Bhvy.log: OK
/tmp/webfront-stderr---supervisor-IN1WLq.log: OK
/tmp/kafka-stdout---supervisor-AdqhYG.log: OK
/tmp/umanager-stdout---supervisor-cxCgc_.log: OK
/tmp/zookeeper-stdout---supervisor-bZQngQ.log: OK

----------- SCAN SUMMARY -----------
Known viruses: 6727830
Engine version: 0.100.2
Scanned directories: 1
Scanned files: 11
Infected files: 0
Data scanned: 48.80 MB
Data read: 166.54 MB (ratio 0.29:1)
Time: 34.632 sec (0 m 34 s)
```