---
title: Mac环境中Jenkins的停止和启动命令
date: 2017-11-21 21:56:08
tags: Jenkins
---

> 文章来源: [李小西033](http://blog.csdn.net/lissdy/article/details/51326559)

# 1. 启动

```bash
sudo launchctl load /Library/LaunchDaemons/org.jenkins-ci.plist
```

# 2. 停止

```bash
sudo launchctl unload /Library/LaunchDaemons/org.jenkins-ci.plist
```

