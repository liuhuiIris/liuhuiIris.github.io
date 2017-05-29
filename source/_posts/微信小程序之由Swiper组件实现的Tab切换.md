---
title: 微信小程序之由Swiper组件实现的Tab切换
date: 2017-01-06 16:38:38
tags: 微信小程序
---

1.效果图---样式将就下
----------------------------------
!["wx_tab"](https://liuhuiiris.github.io/img/wx_tab/tab1.PNG)
!["wx_tab"](https://liuhuiiris.github.io/img/wx_tab/tab2.PNG)
!["wx_tab"](https://liuhuiiris.github.io/img/wx_tab/tab3.PNG)

2.上代码
----------------------------------
		/************************ tab.js ***************************/
		Page({
		    data: { 
		        views: [ 
		            'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg', 
		            'http://img06.tooopen.com/images/20160818/tooopen_sy_175866434296.jpg', 
		            'http://img06.tooopen.com/images/20160818/tooopen_sy_175833047715.jpg' 
		        ]
		    }
		})

		/************************ tab.wxml ***************************/
		<swiper indicator-dots="true">
		    <block wx:for="{{views}}">
		        <swiper-item>
		            <view class="slide-view">
		                <image src="{{item}}" />
		            </view>
		        </swiper-item>
		    </block>
		</swiper>

		/************************ tab.wxss ***************************/
		@charset "UTF-8";
		page {
		  display: block;
		  min-height: 100%;
		  background-color: red; }

		swiper-item {
		  min-height: 100%;
		  margin-top: 88rpx; }

		.slide-view {
		  width: 100%; }

		page {
		  background: #eeeeee; }

		page .wx-swiper-dots.wx-swiper-dots-horizontal {
		  top: 0; }

		page .wx-swiper-dot {
		  width: 252rpx;
		  display: inline-flex;
		  height: 88rpx;
		  line-height: 80rpx;
		  vertical-align: sub;
		  background: #fff;
		  border-bottom: 5rpx solid transparent; }
		  page .wx-swiper-dot:nth-child(1)::before {
		    content: '消息'; }
		  page .wx-swiper-dot:nth-child(2)::before {
		    content: '通讯录'; }
		  page .wx-swiper-dot:nth-child(3)::before {
		    content: '发现'; }

		page .wx-swiper-dot-active {
		  border-color: #00bbfc; }

		page .wx-swiper-dot::before {
		  flex-grow: 1; }

		page .wx-swiper-dot-active::before {
		  color: #00bbfc;
		  flex-grow: 1; }
