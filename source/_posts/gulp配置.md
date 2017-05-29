---
title: gulp配置
date: 2016-11-10 13:48:54
tags: gulp 环境配置
---

 1. 安装node,选择版本不多说
-----------------

	中文网 http://nodejs.cn/
	官网 http://www.nodejs.org/download/
	
	安装套路：选择安装路径，接受协议，各种下一步
	注意一点：一般勾选自动配置环境变量，不然要自己配置，默认给配置的话就方便多了。如果需要配置环境变量的话，加上nodejs的安装路径即可，比如说我的安装路径是D:\nodejs\，那么在path的变量值之后加上;D:\nodejs\即可
	

 2. gulp作用
------

	• 自动刷新页面
	• 自动编译scss
	• 自动合并文件
	• 自动压缩文件
	

3. gulp简单使用配置
-------------

	创建一个测试项目gulp
	• Ctrl+R -> cmd -> cd到gulp目录
	• npm install gulp
	• npm install gulp-connect
	• npm install gulp-ruby-sass
	• npm install gulp-uglify
	
	在项目文件下创建配置文件gulpfile.js
	文件内容：
	//加载模块
	
	var gulp = require("gulp");
	//合并文件
	//var concat = require("gulp-concat");
	//热部署（即时刷新）
	var connect = require("gulp-connect");
	//编译scss
	var sass = require("gulp-ruby-sass");
	//压缩文件
	var uglify = require("gulp-uglify");
	
	//定义个任务，处理html
	gulp.task("refreshHTML",function(){
		gulp.src("./*.html").pipe(connect.reload());
	});
	
	//监听任务
	gulp.task("watch",function(){
		//让connect启动一个服务器，这样它才能即时刷新浏览器
		connect.server({
			livereload:true
		});
		//检测文件的变化，执行相应的任务
		gulp.watch("./*.html",["refreshHTML"]);
	});
	
	/*******************我是文件结束线*******************************/
	

命令行中：
-----

	gulp watch 回车得到如下（如果提示不是内部命令什么鬼的，npm install -g gulp）
	
	得到localhost:8080地址，就可以实现实时更新啦，撒花完结！
	

附相关网站教程：
--------

	https://www.npmjs.com/
	http://www.open-open.com/lib/view/open1426232157888.html
	
	
