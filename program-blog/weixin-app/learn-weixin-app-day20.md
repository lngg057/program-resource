# X天小程序开发速度入门--第20天

今天学习基础内容 icon。学习的方式，先把控件基本用法掌握，然后修改官方示例，练习CSS样式，更新到小程序的 Demo 项目。

## Demo说明

在官网例子基础上，实现 icon 的 type,size,color效果展示。同时进行以下扩展：

* 在icon下面增加对应的属性
* 根据内容进行宽度调整，即 wx:for 循环中，依据 wx:for-index 的值调整列宽

## 增加内容

```xml
<block wx:for="{{iconSize}}">
    <icon type="success" size="{{item}}"/>
  </block>
```

在原来的基础上，把内容显示出来。icon 外增加一个 view，同时加入内容显示，如下：

```xml
    <view class="group-item" style="width:30%;">
      <icon type="success" size="{{item}}" />
      <view style='inline-block'>{{item}}</view>
    </view>
```

## 定立样式

这里定义了 group-item 样式，确保每个示例能够保持在同一行，而不是分行显示。

```css
.group-item{
  display: inline-block;
}
```

## 根据 for-index 调整样式
有些样式的内容比较长，需要把宽度调整得多一些。

```xml
  <block wx:for="{{iconType}}" wx:for-index="idx" style='display:flex;'>
    <view class="group-item" wx:if="{{(idx-1) % 3 == 0}}" style="width:40%;">
      <icon type="{{item}}" size="30" />
      <view>{{item}}</view>
    </view>
    <view class="group-item" wx:else style="width:30%;">
      <icon type="{{item}}" size="30" />
      <view>{{item}}</view>
    </view>
  </block>
```

说明：

* 首先指定index名称，`wx:for-index="index"`
* 判断第二列 `wx:if="{{(idx-1) % 3 == 0}}"`，定立样式 `style="width:40%;"`
* 非第二列 `wx:else`, 定立样式 `style="width:30%;"`
