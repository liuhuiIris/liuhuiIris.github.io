---
title: hexo换电脑
date: 2017-05-29 23:03:01
tags:
---

# 1. 源代码上云端

将源代码上传到github上
``` bash
$ git remote add origin git@github.com:liuhuiIris/liuhuiIris.github.io.git
```
    

如果提示错误 ****.git
``` bash
$ git init
```    


接下来就是常规的git操作
``` bash
$ git checkout -b hexo
$ git add .
$ git ci -m '随便写点什么'
$ git push   <<如果首次创建，根据提示输入命令
```
# 2. 在新电脑上配置hexo

将代码clone下来，master上是部署的博客，hexo分支上是我们的源代码，切到源代码分支
``` bash
$ 1、git clone git@github.com:liuhuiIris/liuhuiIris.github.io.git
$ git checkout hexo
$ sudo npm install hexo -g
$ npm install hexo --save
$ npm install

```
    
# 3. 继续愉快的写博客吧
``` bash
$ hexo new blockName
$ hexo g
$ hexo s
$ hexo d
```

# 4. 不成功？

1、服务提示 no index.html

检查thmes文件是否缺失，重新配置下主题，再次编译

2、 重新部署hexo不需要hexo init

如果运行了hexo init也没关系，重新配置 _config.yml文件
``` bash
    deploy:
      type: git
      repository: git@github.com:liuhuiIris/liuhuiIris.github.io.git
      branch: master
```
