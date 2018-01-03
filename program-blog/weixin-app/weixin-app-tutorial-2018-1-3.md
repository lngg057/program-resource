# 如何快速、便捷开发小程序

> [视频地址][0]

<!-- toc -->
* [1. 小程序核心架构剖析](#1-小程序核心架构剖析)
   * [1.1 小程序与h5的区别](#11-小程序与h5的区别)
   * [1.2 小程序是如何实现的](#12-小程序是如何实现的)
   * [1.3 小程序核心框架](#13-小程序核心框架)
   * [1.4 各模块之间如何通信](#14-各模块之间如何通信)
* [2. 新版小程序开发工具介绍](#2-新版小程序开发工具介绍)
   * [2.1 做一个微信小程序要准备什么](#21-做一个微信小程序要准备什么)
   * [2.2 新版开发工具改进](#22-新版开发工具改进)
   * [2.3 wafer 2.0](#23-wafer-20)
* [3. 小程序云上开发实践](#3-小程序云上开发实践)

<!-- end toc -->

## 1. 小程序核心架构剖析
### 1.1 小程序与h5的区别
#### 1.1.1 相同点与不同点
* 共同点: 都可以在微信里传播, 跨平台
* 不同点:
   * 小程序是封闭的, 只能在微信里使用
   * 相对h5有更快速体验

#### 1.1.2 小程序为什么比h5快
* 安装包缓存: 一次性把所有资源下载下来
   * **不能超过2M**
* 预加载多个webview: A页面切换到B页面, 不是产生一个新的webview, 而是把预先生成好的页面展现出来
   * 页面层级限制, **不能超过5个**
* 页面加载优化

### 1.2 小程序是如何实现的
#### 1.2.1 最简单的小程序结构
![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/1.png)

* 必须的
   * app.js
   * app.json
   * config.js
* 功能都是在pages里实现
* 开发过程中基础库在util中实现

#### 1.2.2 编译之后的小程序
![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/2.png)

多出的文件:

* WAService.js 逻辑控制的API: 提供给程序调用的接口以及基础库
* WAWebview.js 小程序界面展现: 组件
* WAConsole.js 调试控制单: 开发调试中的工具
* app-config.js 配置文件
* app-service.js 业务逻辑
* page-frame.html 页面框架
* pages 页面样式和模板

![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/3.png)

1. WXML经过WCC编译成JS, 注入Page-frame
2. WXSS通过WCSC编译成JS, 放到 Page下
3. JS文件会统一放到 app-service 部分
4. json配置文件会统一打包放到 app-config 文件里面去

### 1.3 小程序核心框架
![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/4.png)

分为3个大块:

* AppView视图层: 整个页面的展现
* AppService逻辑层: 业务逻辑
   * 点击按钮的功能
   * 与后台交互的逻辑
* 微信Native: 比如扫描二维码, 硬件接口, 发起网络轻蹭

#### Page-frame.html
![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/5.png)

小程序是使用WebView来实现, 把文件都编译成Html, JS文件都包装到 Page-frame.html 里面来.

#### WAWebview.js
![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/6.png)

涉及展现相关, 比如 select, video组件都是在这里定义和使用.

* Component: 小程序组件
* WX.API: 私有, 不对外开放
* Render: 展现相关控制
* Event: 事件
* WxJSBridge: 调用远程Native方法
* Reporter: Report方法

#### WAService.js
![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/7.png)

涉及业务逻辑的相关处理

* Module: Module定义
* Global API: 全局方法, 比如 app(), 或者 new Page(), 或者onXX() 事件
* WX.API: API, 比如 Wx.Login()
* WxJSBridge: 与微信Native通信
* Reporter: Report方法

### 1.4 各模块之间如何通信
#### 1.4.1 界面和业务逻辑之间的事件交互
![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/8.png)

举例, 当点击一个登陆操作:

1. View(登陆按钮)
2. publish 消息给JSBridge
3. JSBridge通过WebView调用Native方法
4. Native通过JSCore传递给JSBridge
5. JSBridge传递给Service

Service会处理登陆的业务逻辑, 处理完毕后:

1. Service处理完毕
2. publish 消息给JSBridge
3. JSBridge通过JSCore传递给Native
4. Native通过WebView, 把展示的结果通过JSBridge告诉View
5. View进行登陆结果展示

**时序图**

![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/9.png)

#### 1.4.2 小程序调用原生方法的数据流
![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/10.png)

举例, 用户点击了扫描二维码按钮:

1. View打开扫描二维码
2. 产生消息到JSBridge
3. 经过Webview到Native
4. Native把产生的结果经过WebView传递给JSBridge
5. JSBridge返回的结果在View中展示

在Service中调用Native方法:

1. Service产生消息到JSBridge
2. JSBridge通过JSCore把消息传递给Native
3. Native把产生的结果通过JSCore传递给JSBridge
4. JSBridge把结果返回到Service

#### 1.4.3 Native回调小程序
Native在处理过程中需要把消息通知给服务

![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/10.png)

举例, 微信关闭或隐藏掉, 会发布 on时间, onLoad等

1. Native会通知WebView
2. WebView通过JSBridge产生on事件
3. 传递给View

在Service中:

1. Native会通知JSCore
2. JSCore通过JSBridge产生on事件
3. 传递给Service

## 2. 新版小程序开发工具介绍
### 2.1 做一个微信小程序要准备什么
![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/12.png)

**前端展现只是很小的一部分, 真正复杂的是在后台的服务**

* 域名: 买一个域名
* 证书: 申请证书, HTTPS请求
* 服务器
* 数据库
* 发布
* 调试

**存在问题**

![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/13.png)

### 2.2 新版开发工具改进
![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/14.png)

**一键生成的部署**

1. 一键自动配置可运行后台环境: 自动分配域名, 证书, 临时服务器, 数据库
2. 后台代码编写: Server目录, 支持node.js, php
3. 一键上传代码自动部署: 上传代码, 自动重启
4. 远程调试: Node.js版本可以远程调试

### 2.3 wafer 2.0
小程序开发解决方案sdk与技术支持

![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/15.png)

* 登录
* 图片上传
* 数据库操作
* 信道服务
* 图片识别
* 音频识别
* 语音识别
* ...

## 3. 小程序云上开发实践
![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/16.png)

自己实现Websocket需要考虑的问题

![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/17.png)

小程序Websocket解决方案

![](http://oiitmli7b.bkt.clouddn.com/wxapp/course/18.png)

小程序能力 demo

其他服务与接口

* Websocket服务: web端长连接服务, 应用于实时场景
   * 游戏
   * 聊天
   * 其他实时服务
* 图片识别(鉴黄, OCR, 人脸识别)
* 语音识别(语音识别, 声纹识别, 语音合成)
   * 语音转文字
   * 关键词检索
   * 静音检测
   * 语序检测
   * 情绪识别
* 视频, 直播, 云通信等

[0]: https://cloud.tencent.com/act/course/detail/288?fromSource=gwzcw.700614.700614.700614