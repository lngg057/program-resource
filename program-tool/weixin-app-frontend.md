# 通过微信小程序学习前端技术

## JavaScript在小程序开发中的应用

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
