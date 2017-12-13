# X天小程序开发速度入门--第22天

今天学习基础内容 rich-text。学习的方式，先把控件基本用法掌握，然后修改官方示例，练习CSS样式，更新到小程序的 Demo 项目。

## rich-text基本结构

```xml
<rich-text nodes="{{nodes}}" bindtap="tap"></rich-text>
```

上面的代码定义了一个rich-text. 内容采用 node 定义, 后台 data:nodes 定义如下:

```javascript
nodes: [{
      name: 'div',
      attrs: {
        class: 'div_class',
        style: 'line-height: 60px; color: red;'
      },
      children: [{
        type: 'text',
        text: 'Hello&nbsp;World!'
      }]
    }]
```

上面定义了一个 html div 元素

* 行高 60px
* 颜色 red
* 文本内容 Hello World!

## node 结构说明
node 分为两类:

* html元素: 支持 image, h, table(thead, tr, td), ul/ol, blockquote, code等
   * 每种元素支持的属性在 [rich-text文档](https://mp.weixin.qq.com/debug/wxadoc/dev/component/rich-text.html) 中有定义
* text节点: 显示内容

### node定义

```javascript
nodes: [{
      name: 'HTML标签',
      attrs: {
        class: '指定的样式',
        attribute: 'value' // 在文档中支持的标签属性
      },
      children: [{
      	// 这里可以嵌套定义标签, 比如 div里嵌套div, 循环
      	// 也可以用 text 节点结束
      }]
    }]
```

### text节点

```javascript
children: [{
    type: 'text',
    text: 'Hello&nbsp;World!'
  }]
```

在节点定义的最后一层, 叶子节点, 指定类型后, 写上文字 `type:text`

### 节点与html关系
举例

```javascript
    olnodes: [
      {
        name: "ol",
        attrs: {
          class: 'ol_class',
          start: '1',
          type: 'A'
        },
        children: [
          {
            name: "li",
            children: [
              {
                type: "text",
                text: '行1'
              }
            ]
          },
          {
            name: "li",
            children: [
              {
                type: "text",
                text: '行2'
              }
            ]
          }]
```

上面这段节点定义, 与下面的html等价

```html
<ol start="1" type="A">
	<li>行1</li>
	<li>行2</li>
</ol>
```
