# X天小程序开发速度入门(UI)--第12天

> 周末了，一个好天气
> 第12天继续[微信小程序把玩系列](http://blog.csdn.net/u014360817/article/category/6433383/)
> 模块化与数据绑定

## 模块化
解决 Javascript 代码的引入，quick start 案例中有 util.js 里面提供了日期格式化代码

练习的时候加入新的文件 mylog.js 把打印日志 console.log 做一下封装。

1 点 utils 目录
2 新建 mylog.js
3 创建 mylog 函数并导出
4 在 index.js 里引入 mylog.js，把 console.log 替换成 logger.log
5 查看结果

**mylog.js**

```javascript
const mylog = msg => {
  console.log("[mylog]" + msg);
}

// mylog = msg => {
//   console.log("[mylog1]" + msg);
// }

module.exports = {
  log: mylog
}
```

这里加入了 const，在 mylog.js 里不能修改，取消注释的代码会报告下面错误

`SyntaxError: unknown: "mylog" is read-only`

**index.js**

```javascript
// 引入
const logger = require('../../utils/mylog.js')

// 调用
Page({
...
  onLoad: function (options) {
    logger.log("index --- onLoad");
  },
...
})
```

输出：`[mylog]index --- onLoad`

## 数据绑定
在 WXML 中通过 `{{ }}` 把 `Page({ data:{...} })` 中定义的数据在界面中展示出来。

1 点 page 目录
2 新建 data 目录及 data 页面(开发工具会创建 data.js, data.json, data.wxml, data.wxss)
3 在 data 目录新建 objectCombine.wxml 用来定义 WXML 模板
4 编写代码如下
5 查看结果

### 如何分析
在调试器，Wxml面板里，可以看到即时生成的结果

```xml
<page>
<view>Hello WeApp</view>
<viewid="item-0">组件属性</view>
<view>控制属性</view>
<view>三元运算符</view>
<view>我是运算结果---3 + 3 + d</view>
<view>Hello 顺子</view>
<view>数组元素: </view>
<view> For:0, Bar:1 </view>
<view> a:1, b:2,c:3, d:4,e:5 </view>
<view> foo:my-foo, bar:my-bar </view>
</page>
```

更直观的，可以在调试器，AppData 面板里直接修改数据查看效果。

### 关于template
[官网的模板说明](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/view/wxml/template.html)内容是全的，但是对于 `is` 引用模板，没有给出 `objectCombine` 的定义。

这里自己写了 objectCombine.wxss 作为示例，从 template `data` 属性里的数据进行了展示。

### 完整的示例

**data/data.js**

```javascript
Page({
  data: {

    //内容绑定
    message: 'Hello WeApp',

    //组件属性绑定
    id: 0,

    //控制属性绑定
    condition: true,

    //三元运算
    flag: false,

    //算数运算
    a: 1,
    b: 2,
    c: 3,

    //逻辑判断
    length: 5,

    //字符串运算
    name: '顺子',

    //数组组合
    zero: 0,

    //对象

    x: 0,
    y: 1,

    //对象展开
    obj1: {
      a: 1,
      b: 2
    },
    obj2: {
      c: 3,
      d: 4
    },
    p: 5,

    //对象key和value形同时
    foo: 'my-foo',
    bar: 'my-bar'
  }
})
```

**data/data.wxml**

```xml
<import src="objectCombine.wxml"/>

<!--数据绑定使用对象---内容-->
<view>{{message}}</view>

<!--数据绑定使用对象---组件属性---需要在双引号之内-->
<view id="item-{{id}}">组件属性</view>

<!--数据绑定使用对象---控制属性---需要在双引号之内-->
<view wx:if="{{condition}}">控制属性</view>

<!--数据绑定使用对象---三元运算-->
<view hidden="{{flag ? true : false}}">三元运算符</view>

<!--数据绑定使用对象---算数运算-->
<view>我是运算结果---{{a + b}} + {{c}} + d</view>

<!--数据绑定使用对象---逻辑判断-->
<view wx:if="{{length > 5}}">asdf</view>

<!--数据绑定使用对象---字符串运算-->
<view>{{"Hello " + name}}</view>

<!--数据绑定使用对象---数组组合-->
<view wx:key="{{[zero, 1, 2, 3, 4, 5, 6]}}">数组元素: {{item}}</view>

<!--数据绑定使用对象---对象-->
<template is="objectCombine1" data="{{for: x, bar: y}}"></template>

<!--数据绑定使用对象---扩展运算符对象 ...  将一个对象展开-->
<template is="objectCombine2" data="{{...obj1, ...obj2, e: 5}}"></template>
<!-- <template is="objectCombine2" data="{{e: 5}}"></template> -->
<!-- <template is="objectCombine2" data="{{obj1, obj2, e: 5}}"></template> -->

<!--数据绑定使用对象---对象的key和value相同时-->
 <template is="objectCombine3" data="{{foo, bar}}"></template> 
```

**objectCombine.wxml**

```xml
<template name="objectCombine1">
  <view>
    For:{{for}}, Bar:{{bar}}
  </view>
</template>

<template name="objectCombine2">
  <view>
    a:{{a}}, b:{{b}},c:{{c}}, d:{{d}},e:{{e}}
  </view>
</template>

<template name="objectCombine3">
  <view>
    foo:{{foo}}, bar:{{bar}}
  </view>
</template>
```
