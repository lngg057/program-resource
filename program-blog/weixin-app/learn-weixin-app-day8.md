# X天小程序开发速度入门(UI)--第8天

*如果把Web比作汽车，那么浏览器的核心就是引擎。HTML中的各种标签，就是车厢里的各种零件，仪表盘、座椅、车窗等等。CSS就是内饰装修，各种风格随意挑选。JavaScript就是各种自动控制。在没有自动装置的年代，车窗是靠摇的，车门使用钥匙锁的。有了JavaScript，自动升降，一键启动成为可能。*

*小程序也是一款车，它是小型移动版Web程序。由于规格限制，很多内容进行了定制。HTML变成了WXML，CSS变成了WXSS，当然JavaScript还是一样，只是支持的接口有限。*

> 接下来的7天把[小程序组件](https://mp.weixin.qq.com/debug/wxadoc/dev/component/)操练一遍，了解一下车内主要零件的使用方法。
> 对了，你就是那个汽车设计师。

## 背景
小程序与常规浏览器有什么不同？

* iOS：小程序的 javascript 运行在 JavaScriptCore 中，由 WKWebView 来渲染，环境有 iOS8、iOS9、iOS10
* Android：小程序的 javascript 通过 X5 JSCore 解析，由 X5 基于 Mobile Chrome 53/57 内核来渲染
* 开发工具上：小程序的 javascript 运行在 nwjs 中，由 Chrome Webview 来渲染

参考 [小程序文档的说明](https://mp.weixin.qq.com/debug/wxadoc/dev/devtools/details.html#运行环境差异)。

也就是说，小程序代码会在不同环境下会采用不同的引擎，展示效果可能也会有差异。

## 小程序组件
小程序提供了基础组件和自定义组件

### 基础组件
分为7大类

* 视图容器(View Container)
* 基础内容(Basic Content)
* 表单(Form)
* 导航(Navigation)
* 多媒体(Media)
* 地图(Map)
* 画布(Canvas)
* 客服会话

可以通过组合这些基础组件进行快速开发。

### 自定义组件
自定义组件是页面内的功能模块抽象成，可不同的页面中重复使用；也可以是复杂的页面拆分出的多个低耦合的模块。

自定义组件在使用时与基础组件非常相似。

**注意：** 从小程序基础库版本 1.6.3 开始。如果需要使用相关特性，请确认在项目选项中已勾选“预览/上传时使用新特性”。

## WeUI练习
在腾讯官方github有微[信小程序WXSS的组件演示](https://github.com/Tencent/weui-wxss)

操练的方式：

1 按照说明把项目在开发工具中运行起来
2 结合效果，理解各参数的功能，整理成知识结构，便于开发参考
3 总结

## 小程序页面
所有组件都是在页面中展示，了解页面的生命周期（[图片](https://mp.weixin.qq.com/debug/wxadoc/dev/image/mina-lifecycle.png?t=20171116)）、跳转（路由）也是很关键的，包括跳转的触发条件、跳转、传参、页面栈(结果)等。

## 扩展阅读
* [webkit](https://baike.baidu.com/item/webkit/1467841?fr=aladdin)：Mac OS X 系统引擎框架，源自KDE
* [X5 JSCore](https://baike.baidu.com/item/X5%E5%86%85%E6%A0%B8/14083554?fr=aladdin)：腾讯基于webkit改造的渲染引擎
* Mobile Chrome：谷歌Chrome移动版
* [NW.js](https://nwjs.io/)：曾经叫 node-webkit，可以从DOM里直接调用所有 Node.js 模块

