# X天小程序开发速度入门--第21天

今天学习基础内容 text。学习的方式，先把控件基本用法掌握，然后修改官方示例，练习CSS样式，更新到小程序的 Demo 项目。

## Demo说明

在官网例子基础上，实现 text 的 selectable,space,decode效果展示。同时进行以下扩展：

* 为每个属性示例分栏目展示
* 将原来点击添加行，改为下拉添加行，点击删除，方便手机端操作


## 分栏目展示
```xml
<view class="group">
    <view class="title">标题</view>
    <text>内容</text>
  </view>
 ```

```css
.group {
  background-color:#ffffff
}

.title {
  background-color:#ffff00
}
```

## 改为下拉刷新
在页面的 json 文件中启用下拉刷新

```json
{
  "enablePullDownRefresh": true
}
```

在页面的 js 文件中处理 `onPullDownRefresh` 事件,

```javascript
onPullDownRefresh: function () {
    // 处理业务逻辑
    ...
    // 停止当前页面的下拉刷新
    wx.stopPullDownRefresh();
  },
```

