---
title: hexo + gitment
date: 2018-12-04 18:18:53
tags: hexo
---

首先万分感谢踩坑小分队们！！！

陆陆续续、忐忐忑忑在工位上搞了一天gitment，终于成功搞定，完结撒花🌺 🌺 🌺

(希望领导们不会看到哈，我也是有认真完成本职工作的，认真脸*_*)

这里只想放大佬们的链接了

# 1. gitment 登录失败问题

首先大家都发现gitment 登录失败的问题，由此参考以下文章,并手动跑了原作者的Server，并替换为自己服务器地址

[gitment 登录失败问题](https://www.jianshu.com/p/f2f4c802914b)

虽然楼主注意到了文章中nginx等一系列猛如虎的操作，但还是偷懒只用了IP，结果可想而知，人家只认https...

以前楼主搞过域名解析乱七八糟的东西，也是同样的问题，到期了，于是打算偷懒找个现成的

# 2. gitment评论模块接入hexo

非常感谢以下文章作者，讲解很是详细，还给了解决跨域问题的例子，就是请大家留心下next版本即可，楼主今天刚升级next，版本有点对不上

[gitment评论模块接入hexo](https://www.wenjunjiang.win/2017/07/02/gitment%E8%AF%84%E8%AE%BA%E6%A8%A1%E5%9D%97%E6%8E%A5%E5%85%A5hexo/)

还有其中参数不是很对应,注意对应关系就好，没有对错之分

```
githubID:为github的用户名
repo:为博客的仓库
ClientID:为上一步获取的client ID
ClientSecret:为博客的仓库client secret
lazy:是否默认把评论框收起来

github_user: 
github_repo: 
client_id: 
client_secret: 
```

就在楼主满心欢喜以为大功告成的时候，发现了Error：validation failed的问题 凸(艹皿艹 )

# 3. 添加Gitment评论系统踩过的坑

感谢另一位踩坑小分队成员，几乎踩遍了 label 长度所有的坑，手动比心心❤️

[添加Gitment评论系统踩过的坑](http://xichen.pub/2018/01/31/2018-01-31-gitment/)

# 4. 作死的多个github账户问题

楼主当时因为入职，很作死地申请了个新的github账户，结果把浏览器这厮搞晕了，怎么都登录不上，New incognito Window 或者 登出用同一个账户登录就可以了

然后完美搞定，心累到不想放图-_-!!! 将就看吧
