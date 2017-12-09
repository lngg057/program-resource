# 微信小程序

* [开发文档](#wxdoc)
    * [小程序API](#wxapi)
    * [MINA框架](#mina)
    * [WeUI组件](#weui)
* 教程
    * [官网简易教程](https://mp.weixin.qq.com/debug/wxadoc/dev/)
* [学习日志](#wxblog)
* 练习项目
* 相关技术
    * 前端
        * JavaScript
    * 后台
    * HTTP
    * 设计
    * 产品
    * 维护
* 其他资源
    * [官网](https://mp.weixin.qq.com/)
    * [微信开发者工具 ](https://mp.weixin.qq.com/debug/wxadoc/dev/devtools/download.html?t=1510576089)
        * [基础库](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/client-lib.html)
    * [微信开发者社区](https://developers.weixin.qq.com/home?token=137700584&lang=zh_CN)
    * 注意事项
        * [要求真机调试的功能](https://mp.weixin.qq.com/debug/wxadoc/dev/devtools/notsupport.html)
        * [不支持的ES6 API](https://mp.weixin.qq.com/debug/wxadoc/dev/devtools/details.html#客户端es6-api-支持情况)

<h2 id="wxdoc">开发文档</h2>

<h3>微信开发者文档</h3>

[文档主页](https://mp.weixin.qq.com/debug/wxadoc/dev/index.html)

* [微信开发者工具简介](https://mp.weixin.qq.com/debug/wxadoc/dev/devtools/devtools.html)

<h3 id="wxapi">小程序API</h3>

[API文档](https://mp.weixin.qq.com/debug/wxadoc/dev/api/)

* [网络](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-net)
* 媒体
    * [图片](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-img)
    * [录音及管理](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-record)
    * [音乐播放](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-audio)
    * [视频播放](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-video)
* [文件](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-file)
* [数据缓存](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-storage)
* [位置](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-location)
* [设备](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-device)
    * 系统信息
    * 网络状态
    * 加速度计
    * 罗盘
    * 拨打电话
    * 扫码
    * 剪切板
    * 蓝牙
    * iBeacon
    * 屏幕亮度
    * 用户截屏事件
    * 震动
    * 手机联系人
* [界面交互](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-react)
    * 交互反馈
    * 设置导航条
    * 设置置顶信息
    * 导航
    * 动画
    * 位置
    * 绘图
    * 下拉刷新
* [WXML节点信息](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-wxml)
* [第三方平台](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-third-platform)
* [开放接口](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-open-interface)
* [数据](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-data)
* [拓展接口](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-ext-interface)
* [调试接口](https://github.com/tangyouhua/wx-mini-rogram/blob/master/api/api.md#wxapi-debug-interface)

<h3 id="mina">小程序框架 MINA</h3>

[MINA主页](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/MINA.html)

* [app.json配置](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/config.html)
* [WXML标签语言](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/view/wxml/)
* [WXSS样式表](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/view/wxss.html) 
*  [事件](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/view/wxml/event.html)

<h3 id="weui">小程序UI组件-WeUI</h3>

[基础组件](https://mp.weixin.qq.com/debug/wxadoc/dev/component/)

<h2>微信开发者工具</h2>

<h3>调试</h3>

* 调试器 Console：输入和调试代码，比起在debug里面查看变量方便很多
* 调试器 Wxml：可以直接查看wxml 转化后的界面，与chrome里面查看html的DOM模型一样
* 调试器 Source：查看源码，下断点，调试
* 调试器 AppData：查看数据非常方便，比如定义的userInfo、motto等信息
* 调试器 Storage：查看本地存储，配合清缓存调试
* 调试器 Network：查看网络调用，与后台通信时用到
* 调试器 Sensor：模拟地理位置和重力感应，高级功能（不大常用:P）

<h2>相关技术</h2>

<h3>JavaScript在小程序开发中的用法</h3>

<h4>箭头函数</h4>

```
    wx.login({
      success: res => {
        // 发送 res.code 到后台换取 openId, sessionKey, unionId
      }
    })
```

这里面 `res => { }` 定义了一个匿名函数，ECMAScript 6支持这种写法，等同于

```
    wx.login({
      success: function(res)  {
        // 发送 res.code 到后台换取 openId, sessionKey, unionId
      }
    })
```

<h4>逻辑运算符 &#124;&#124;</h4>

```
var logs = wx.getStorageSync('logs') || []
```

1 在调试，Source面板下断点
2 在调试，Console面板下输入 `wx.getStorageSync('logs')`
    * 初次运行或者清除缓存后，会返回空数组
3 上面这句，在 `wx.getStorageSync('logs')` 返回 `undefined` 情况下，会返回一个空数组
    * `undefined`  在条件语句中判定为 `false`

**上面语句的含义**：返回 logs 非空数组（本地缓存），或者返回空数组

<h4>数组操作 unshift</h4>

```
  onLaunch: function () {
    // 展示本地存储能力
    var logs = wx.getStorageSync('logs') || []
    logs.unshift(Date.now())
    wx.setStorageSync('logs', logs)
```

* `unshift()`  方法可向数组的开头添加一个或更多元素，并返回新的长度
* 小程序初始化完成  `onLaunch` 事件发生，会记录当前日期到 logs 数组，存储到本地缓存

<h4>this对象</h4>

```
wx.getUserInfo({
    success: res => {
        // 可以将 res 发送给后台解码出 unionId
        this.globalData.userInfo = res.userInfo

        // 由于 getUserInfo 是网络请求，可能会在 Page.onLoad 之后才返回
        // 所以此处加入 callback 以防止这种情况
        if (this.userInfoReadyCallback) {
            this.userInfoReadyCallback(res)
        }
```
`this` 对象不同场合有各种不同的用法，上面的代码中，`this` 代表的是Global对象
* 在微信IDE中 `CTRL+SHIFT+F` 查找 `userInfoReadyCallback`，可以看到 index.js 中定义了这个函数
* 这段代码的目的，就是为了防止 Page.onLoad 比  `onLaunch` 事件中请求的用户信息成功之前已运行，此时app.globalInfo.userInfo的值是空的，所以还需要再重新对其进行赋值

<h4>全局变量</h4>

```
  globalData: {
    userInfo: null
  }
```
app.js 里定义了 `globalData` 全局变量，于是在各个地方都用到了，进行用户信息传递

理论上有两种方法可以查看  `globalData`  被调用的情况
* 右键菜单，查找所有引用：恩，没有用
*  `CTRL+SHIFT+F` 查找  `globalData`：可以看到，在 app.js 和 index.js 中分别进行了赋值和使用

<h4>console.log</h4>

```
  getUserInfo: function(e) {
    console.log(e)
```

这是很重要的调试技巧，上面的代码把 `UserInfo` 在Console面板中打印了出来

* Source面板下断点
* 执行 `console.log(e)` 或者 直接在Console面板下输入 `console.log(e)` 回车，都可以看到返回的用户信息 

<h2 id="wxblog">学习日志</h2>

* [X天小程序开发速度入门--第1天](../program-blog/weixin-app/learn-weixin-app-day1.md)
* [X天小程序开发速度入门--第2天](../program-blog/weixin-app/learn-weixin-app-day2.md)
* [X天小程序开发速度入门--第3天](../program-blog/weixin-app/learn-weixin-app-day3.md)
* [X天小程序开发速度入门--第4天](../program-blog/weixin-app/learn-weixin-app-day4.md)
* [X天小程序开发速度入门--第5天](../program-blog/weixin-app/learn-weixin-app-day5.md)
* [X天小程序开发速度入门--第6天](../program-blog/weixin-app/learn-weixin-app-day6.md)
* [X天小程序开发速度入门--第7天](../program-blog/weixin-app/learn-weixin-app-day7.md)
* [X天小程序开发速度入门--第8天](../program-blog/weixin-app/learn-weixin-app-day8.md)
* [X天小程序开发速度入门--第9天](../program-blog/weixin-app/learn-weixin-app-day9.md)
* [X天小程序开发速度入门--第10天](../program-blog/weixin-app/learn-weixin-app-day10.md)
* [X天小程序开发速度入门--第11天](../program-blog/weixin-app/learn-weixin-app-day11.md)
* [X天小程序开发速度入门--第12天](../program-blog/weixin-app/learn-weixin-app-day12.md)
* [X天小程序开发速度入门--第13天](../program-blog/weixin-app/learn-weixin-app-day13.md)
* [X天小程序开发速度入门--第14天](../program-blog/weixin-app/learn-weixin-app-day14.md)
* [X天小程序开发速度入门--第15天](../program-blog/weixin-app/learn-weixin-app-day15.md)
* [X天小程序开发速度入门--第16天](../program-blog/weixin-app/learn-weixin-app-day16.md)
* [X天小程序开发速度入门--第17天](../program-blog/weixin-app/learn-weixin-app-day17.md)
* [X天小程序开发速度入门--第18天](../program-blog/weixin-app/learn-weixin-app-day18.md)
* [X天小程序开发速度入门--第19天](../program-blog/weixin-app/learn-weixin-app-day19.md)
