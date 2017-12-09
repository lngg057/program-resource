# X天小程序开发速度入门(UI)--第11天

> 早睡早起身体好，改为白天更新了
> 第11天继续[微信小程序把玩系列](http://blog.csdn.net/u014360817/article/category/6433383/)
> 应用生命周期 与 页面生命周期

## 应用生命周期
app.js 中把 quickstart 代码注释掉，输入 app 再 `TAB`

```javascript
App({

  /**
   * 当小程序初始化完成时，会触发 onLaunch（全局只触发一次）
   */
  onLaunch: function () {
    console.log("程序启动我会调用");
  },

  /**
   * 当小程序启动，或从后台进入前台显示，会触发 onShow
   */
  onShow: function (options) {
    console.log("程序启动完我会调用");
  },

  /**
   * 当小程序从前台进入后台，会触发 onHide
   */
  onHide: function () {
    console.log("程序进入后台我会调用");
  },

  /**
   * 当小程序发生脚本错误，或者 api 调用失败时，会触发 onError 并带上错误信息
   */
  onError: function (msg) {
    console.log("程序报错我会调用");
  }
})
```

保存，自动重新编译，`onLaunch`, `onShow`, `onError` 都会调用。

把默认代码注释掉，index 页面获取用户信息会报错，触发 `onError`。 

```
WAService.js:3 thirdScriptError
Cannot read property 'userInfo' of undefined;at pages/index/index page lifeCycleMethod onLoad function
TypeError: Cannot read property 'userInfo' of undefined
```

## 页面生命周期
index.js 中把 quickstart 代码注释掉，输入 page 再 `TAB`

```javascript
Page({

  /**
   * 页面的初始数据
   */
  data: {

  },

  bindViewTap: function () {
    // wx.navigateTo({
    //   url: '../logs/logs'
    // })

    wx.reLaunch({
      url: '../logs/logs'
    })
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    console.log("index --- onLoad");
  },

  /**
   * 生命周期函数--监听页面初次渲染完成
   */
  onReady: function () {
    console.log("index --- onReady");
  },

  /**
   * 生命周期函数--监听页面显示
   */
  onShow: function () {
    console.log("index --- onShow");
  },

  /**
   * 生命周期函数--监听页面隐藏
   */
  onHide: function () {
    console.log("index --- onHide");
  },

  /**
   * 生命周期函数--监听页面卸载
   */
  onUnload: function () {
    console.log("index --- onUnload");
  },

  /**
   * 页面相关事件处理函数--监听用户下拉动作
   */
  onPullDownRefresh: function () {
    console.log("index --- onPullDownRefresh");
  },

  /**
   * 页面上拉触底事件的处理函数
   */
  onReachBottom: function () {
    console.log("index --- onReachBottom");
  },

  /**
   * 用户点击右上角分享
   */
  onShareAppMessage: function () {
    console.log("index --- onShareAppMessage");
  }
  
})
```

* 正常情况会调用 `onLoad`, `onReady`, `onShow`
* 点击页面
   * `bindViewTap` 如果调用的是 wx.navigateTo，页面会隐藏 `onHide`
   * `bindViewTap` 如果调用的是 wx.reLaunch，页面会销毁 `onUnload`
* 下拉到页面底部会调用 `onReachBottom`
* 小程序右上角点击分享转发会调用 `onShareAppMessage`
* 页面下拉需要在 app.json 中配置：`enablePullDownRefresh` 启用

```json
  "window": {
    "backgroundTextStyle": "light",
    "navigationBarBackgroundColor": "#ff000",
    "navigationBarTitleText": "微信小程序",
    "navigationBarTextStyle": "black",
    "enablePullDownRefresh": true
  },
```
