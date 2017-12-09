# X天小程序开发速度入门(UI)--第14天

> 17年11月28日停更了一天，练习了搜索技术
> 第14天继续[微信小程序把玩系列](http://blog.csdn.net/u014360817/article/category/6433383/)
> scroll-view组件

## scroll-view组件
### 新建 scroll-view 页面
1 点 page 目录
2 新建 scroll-view 目录及 scroll-view 页面(开发工具会创建 scroll-view.js, scroll-view.json, scroll-view.wxml, scroll-view.wxss)
3 修改 scroll-view.wxml, scroll-view.wxss
4 编写代码如下
5 查看结果

### 示例说明
调试器，Wxml面板，查看 scroll-view 结构：

```xml
<scroll-view scroll-y="" style="height: 300px" scroll-top="1" scroll-left="0">
	<view style="background: red; width: 100px; height: 100px"></view>
	<view style="background: green; width: 100px; height: 100px"></view>
	<view style="background: blue; width: 100px; height: 100px"></view>
	<view style="background: yellow; width: 100px; height: 100px"></view>
</scroll-view>
```

垂直滚动区域定义了4个 100x100px 的区域，当 scroll-view 的高度(300px) 小于这4个 view 的高度和(400px)时，会出现垂直滚动条。

**不设置 height 属性**或者**height 的值大于400px**都不会出现滚动效果。

### 滚动事件
在 scroll-view.wxml 中绑定滚动事件

```xml
<scroll-view id="id-scroll-y" scroll-y="true" scroll-top="300" style="height: 300px" bindscroll="bindScroll">
```

在 scroll-view.js 中定义 `bindScroll` 方法，输出 scroll 事件

```javascript
/**
* 绑定滚动事件
*/
bindScroll: function (event) {
	console.log(event);
}
```

垂直滚动后，可以看到滚动的具体信息 detail，包括位移(deltaX, deltaY)、滚动区域的高度(scrollHeight )、左边位置(scrollLeft)、顶部位置(scrollTop)、滚动区域宽度(scrollHeight)

```
{type: "scroll", timeStamp: 274, target: {…}, currentTarget: {…}, detail: {…}}
currentTarget : {id: "id-scroll-y", offsetLeft: 0, offsetTop: 0, dataset: {…}}
	detail : 
	deltaX : 0 
	deltaY : -100 
	scrollHeight : 400 
	scrollLeft : 0 
	scrollTop : 100 
	scrollWidth : 375 
__proto__ : Object
```

结果中 detail 说明：

* deltaY：向下滚动**正数**，向上滚动**负数**
* scrollHeight：滚动区域内容的高度，这里是 4x100=400px
* scrollTop：向下滚动**增加**，向上滚动**减小**，到顶部为0
* scrollWidth：手机屏幕宽度，这里是 iPhone5 定义为375px

### 滚动到顶部
在 scroll-view.wxml 中绑定滚动到顶部事件

```xml
<scroll-view id="id-scroll-y" scroll-y="true" scroll-top="300" style="height: 250px" bindscroll="bindScroll" bindscrolltoupper="bindScrollToUpper">
```

在 scroll-view.js 中定义 `bindScrollToUpper` 方法，输出 **滚动到顶部**

```javascript
  /**
   * 绑定滚动到顶部事件
   */
  bindScrollToUpper: function (event) {
    console.log("滚动到顶部");
  }
```

### 完整代码
**pages/scroll-view/scroll-view.wxml**

```xml
<scroll-view id="id-scroll-y" scroll-y="true" scroll-top="300" style="height: 250px" bindscroll="bindScroll" bindscrolltoupper="bindScrollToUpper">
    <view style="background: red; width: 100px; height: 100px" ></view>
    <view style="background: green; width: 100px; height: 100px"></view>
    <view style="background: blue; width: 100px; height: 100px"></view>
     <view style="background: yellow; width: 100px; height: 100px"></view> 
</scroll-view>

<!--水平滚动-->
<scroll-view scroll-x="true" style=" white-space: nowrap; display: flex" >
<!--  display: inline-block-->
  <view style="background: red; width: 200px; height: 100px; display: inline-block" ></view>
  <view style="background: green; width: 200px; height: 100px; display: inline-block"></view>
  <view style="background: blue; width: 200px; height: 100px; display: inline-block"></view>
  <view style="background: yellow; width: 200px; height: 100px; display: inline-block"></view>
</scroll-view>
```

**pages/scroll-view/scroll-view.js**

```javascript
Page({

  /**
   * 页面的初始数据
   */
  data: {

  },

  /**
   * 绑定滚动事件
   */
  bindScroll: function (event) {
    console.log(event);
  },

  /**
   * 绑定滚动到顶部事件
   */
  bindScrollToUpper: function (event) {
    console.log("滚动到顶部");
  }
})
```

## 总结
通过 `console.log(object)` 输出事件，可以方便地了解到 scroll-view 组件的事件详情。

类似地，可以操练 scroll-view 控件的各种事件，属性设置，从而在实际项目中进行对应的处置。举例，滚动到底部，自动加载列表。
