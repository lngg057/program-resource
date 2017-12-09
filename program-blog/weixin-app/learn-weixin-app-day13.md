# X天小程序开发速度入门(UI)--第13天

> 周一了，一周新的开始
> 第13天继续[微信小程序把玩系列](http://blog.csdn.net/u014360817/article/category/6433383/)
> view组件

## view组件
### 新建 view 页面
1 点 page 目录
2 新建 view 目录及 view 页面(开发工具会创建 view.js, view.json, view.wxml, view.wxss)
3 修改 view.wxml, view.wxss
4 编写代码如下
5 查看结果

这里说是学习view组件，其实主要还是了解在view中如何使用 flex布局。flex布局不是小程序独有的，在css规范中就有说明，除了今天的案例，还可以在[SS3 Flexbox 演示](http://www.css88.com/demo/flexbox-playground/)更直观地理解。[W3C flexbox规范](https://www.w3.org/TR/css-flexbox-1/)里给出了算法说明与示例。

### 引入微信样式
[微信小程序把玩系列](http://blog.csdn.net/u014360817/article/category/6433383/) 里面样式表没有完整的定义，这里做了补充：

* 下载zip文件
* 或 github clone 项目到本地
* dist 目录下 style 文件夹 拷贝到 weixin-app-tutorialx  目录
* app.wxss 开头加入 `@import 'style/weui.wxss';` 
   * 全局引入 weui 样式（后面的页面会引用到）
* 引入[weui-wxss 微信样式](https://github.com/weui/weui-wxss)：看到 `__` 的样式差不多都是微信样式
* 定义了`section` 和 `section__title`

可以通过调试器，Wxml面板，选择对应的元素。在右侧的 styles 栏目中会列出当前有效的样式。通过这个可以查看错误，也可以手动修改样式查看效果。

## 示例说明
例子的结构如下：

```xml
<page>
	<view class="page">
		<view class="page__hd">
			<text class="page__title">...</text>
			<text class="page__desc">...</text>
		</view>
		<view class="page__bd">
			<view class="section">...</view>
			<view class="section">...</view>
			<view class="section">...</view>
			<view class="section">...</view>
			<view class="section">...</view>
			<view class="section">...</view>
			<view class="section">...</view>
			<view class="section">...</view>
			<view class="section">...</view>
		</view>
	</view>
</page>
```

每个 section 是一个示例，里面定义 3个 100x100 的view，标记不同颜色，用来演示布局

```xml
<view class="flex-wrp" style="flex-direction:row;">
	<view class="flex-item" style="background: red"></view>
	<view class="flex-item" style="background: green"></view>
	<view class="flex-item" style="background: blue"></view>
</view>
```

## 完整代码

**app.wxss**

```css
@import 'style/weui.wxss';

page{
    background-color: #F8F8F8;
    font-size: 16px;
    font-family: -apple-system-font,Helvetica Neue,Helvetica,sans-serif;
}
.page__hd {
    padding: 40px;
}
.page__bd {
    padding-bottom: 40px;
}
.page__bd_spacing {
    padding-left: 15px;
    padding-right: 15px;
}

.page__ft{
    padding-bottom: 10px;
    text-align: center;
}

.page__title {
    text-align: left;
    font-size: 20px;
    font-weight: 400;
}

.page__desc {
    margin-top: 5px;
    color: #888888;
    text-align: left;
    font-size: 14px;
}

.section {
    padding-top: 10px;
}

.section__title {
    text-align: left;
    font-size: 16px;
    font-weight: 200;
    background-color: #F0F8F8;
}
```

**pages/view/view.wxss**

```css
.flex-wrp{
    height: 100px;
    display:flex;
    background-color: #FFFFFF;
}
.flex-item{
    width: 100px;
    height: 100px;
}
```

**pages/view/view.wxml**

```css
<view class="page">
    <view class="page__hd">
        <text class="page__title">view</text>
        <text class="page__desc">弹性框模型分为弹性容器以及弹性项目。当组件的display为flex或inline-flex时，该组件则为弹性容器，弹性容器的子组件为弹性项目。</text>
    </view>
    <view class="page__bd">
        <view class="section">
            <view class="section__title">flex-direction: row</view>
            <view class="flex-wrp" style="flex-direction:row;">
                <view class="flex-item" style="background: red"></view>
                <view class="flex-item" style="background: green"></view>
                <view class="flex-item" style="background: blue"></view>
            </view>
        </view>
        <view class="section">
            <view class="section__title">flex-direction: column</view>
            <view class="flex-wrp" style="height: 300px;flex-direction:column;">
                <view class="flex-item" style="background: red"></view>
                <view class="flex-item" style="background: green"></view>
                <view class="flex-item" style="background: blue"></view>
            </view>
        </view>
        <view class="section">
            <view class="section__title">justify-content: flex-start</view>
            <view class="flex-wrp" style="flex-direction:row;justify-content: flex-start;">
                <view class="flex-item" style="background: red"></view>
                <view class="flex-item" style="background: green"></view>
                <view class="flex-item" style="background: blue"></view>
            </view>
        </view>
        <view class="section">
            <view class="section__title">justify-content: flex-end</view>
            <view class="flex-wrp" style="flex-direction:row;justify-content: flex-end;">
                <view class="flex-item" style="background: red"></view>
                <view class="flex-item" style="background: green"></view>
                <view class="flex-item" style="background: blue"></view>
            </view>
        </view>
        <view class="section">
            <view class="section__title">justify-content: center</view>
            <view class="flex-wrp" style="flex-direction:row;justify-content: center;">
                <view class="flex-item" style="background: red"></view>
                <view class="flex-item" style="background: green"></view>
                <view class="flex-item" style="background: blue"></view>
            </view>
        </view>
        <view class="section">
            <view class="section__title">justify-content: space-between</view>
            <view class="flex-wrp" style="flex-direction:row;justify-content: space-between;">
                <view class="flex-item" style="background: red"></view>
                <view class="flex-item" style="background: green"></view>
                <view class="flex-item" style="background: blue"></view>
            </view>
        </view>
        <view class="section">
            <view class="section__title">justify-content: space-around</view>
            <view class="flex-wrp" style="flex-direction:row;justify-content: space-around;">
                <view class="flex-item" style="background: red"></view>
                <view class="flex-item" style="background: green"></view>
                <view class="flex-item" style="background: blue"></view>
            </view>
        </view>
        <view class="section">
            <view class="section__title">align-items: flex-end</view>
            <view class="flex-wrp" style="height: 200px;flex-direction:row;justify-content: center;align-items: flex-end">
                <view class="flex-item" style="background: red"></view>
                <view class="flex-item" style="background: green"></view>
                <view class="flex-item" style="background: blue"></view>
            </view>
        </view>
        <view class="section">
            <view class="section__title">align-items: center</view>
            <view class="flex-wrp" style="height: 200px;flex-direction:row;justify-content: center;align-items: center">
                <view class="flex-item" style="background: red"></view>
                <view class="flex-item" style="background: green"></view>
                <view class="flex-item" style="background: blue"></view>
            </view>
        </view>
    </view>
</view>
```

## flow布局属性说明
* 父级 Flex 属性 – flex container
   * flex-direction
      * row
      * row-reverse
      * column
      * column-reverse
   * flex-wrap
      * nowrap
      * wrap
      * wrap-reverse
   * justify-content
      * flex-start
      * flex-end
      * center
      * space-between
      * space-around
   * align-items
      * stretch
      * flex-start
      * flex-end
      * center
      * baseline
   * align-content
      * stretch
      * flex-start
      * flex-end
      * center
      * space-between
      * space-around
* 子元素 Flex 属性 – flex items
   * order
   * flex-grow
   * flex-shrink
   * flex-basis
   * align-self
      * auto
      * flex-start
      * flex-end
      * center
      * baseline