---
title: sass安装配置
date: 2016-11-10 19:46:22
tags: sass 环境配置
---

 1. 安装Ruby
------

	因为sass依赖于ruby环境，所以装sass之前先确认装了ruby。先导官网下载个ruby
下载地址：[官网](http://rubyinstaller.org/downloads)
下载地址：[中文网](http://www.ruby-lang.org/zh_cn/downloads/)

	在安装的时候，请勾选Add Ruby executables to your PATH这个选项，添加环境变量，不然以后使用编译软件的时候会提示找不到ruby环境
!["sass"](https://liuhuiiris.github.io/img/sass/ruby.png)

2. sass安装
---------

	安装完ruby之后，在开始菜单中，找到刚才我们安装的ruby，打开Start Command Prompt with Ruby
!["sass"](https://liuhuiiris.github.io/img/sass/ruby-cmd.png)

	在任意位置新建文件夹，如sass-test
	在命令窗口中找到该文件夹如：
!["sass"](https://liuhuiiris.github.io/img/sass/sass-test.png)

	查看文件源
!["sass"](https://liuhuiiris.github.io/img/sass/gem-sources.png)

	国外网站可能会访问不到，因此更改为国内源：
!["sass"](https://liuhuiiris.github.io/img/sass/1.png)

	下载sass，gem install sass ,如果出现下图，则安装成功
!["sass"](https://liuhuiiris.github.io/img/sass/2.png)

3. 简单使用sass
-----------
!["sass"](https://liuhuiiris.github.io/img/sass/3.png)

	具体命令语法，可参考：
	http://www.w3cplus.com/sassguide/syntax.html
	http://www.ruanyifeng.com/blog/2012/06/sass.html
	

4. HBuilder配置
-------------

	工具->预编译器配置->.sass,.scss->编辑
	
	命令参数：--style=compact --sourcemap=none --no-cache %FileName% %FileBaseName%.css
!["sass"](https://liuhuiiris.github.io/img/sass/4.png)

5. sublime配置
------------

	关于sass 3.3.0更新说明——3.3.0
sublime相关插件为：[scss语法高亮](https://github.com/MarioRicalde/SCSS.tmbundle)，[sass语法高亮](https://github.com/nathos/sass-textmate-bundle)，[编译](https://github.com/jaumefontal/SASS-Build-SublimeText2)，[保存即编译](https://github.com/alexnj/SublimeOnSaveBuild)，[格式化](https://github.com/badsyntax/SassBeautify)

	打开Sublime->Preferences->Browse Packages…
	将上述插件下载并解压至该文件夹下，重启Sublime
	
	检查是否安装成功
	Ctrl+Shift+P    -> List Packages 可以找到下述插件
!["sass"](https://liuhuiiris.github.io/img/sass/5.png)

6. 使用Sublime Sass
-----------------

	创建scss文件，实时编译Ctrl+b
	如果不想生成.map文件，找到插件目录
	打开Sublime->Preferences->Browse Packages…
	找到该文件
!["sass"](https://liuhuiiris.github.io/img/sass/6.png)

	记事本打开
!["sass"](https://liuhuiiris.github.io/img/sass/7.png)

	加上“--sourcemap=none”或者其他参数配置
!["sass"](https://liuhuiiris.github.io/img/sass/8.png)

	大功告成！
