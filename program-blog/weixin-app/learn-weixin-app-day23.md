# X天小程序开发速度入门--第23天

今天学习基础内容 progress。学习的方式，先把控件基本用法掌握，然后修改官方示例，练习CSS样式，更新到小程序的 Demo 项目。

## Demo说明
在官网例子基础上，实现 progress 的 percent, show, stroke-width, color, activeColor, backgroundColor, active, active-mode 效果展示。同时进行以下扩展：

* 刷进度: 点击按钮进度加10, 进度满后重头刷
* 定时刷新: 点击按钮定时器1s刷一次, 点暂停停止定时器

## 定义后台数据

```javascript
  data: {
    p1: 20,
    p2: 40,
    p3: 60,
    p4: 80,
    intervalID: 0,
    timerButton: '定时刷新'
  },
```

说明, 这里定义的 p1, p2, p3, p4 是4个进度条的进度值; intervalID 定时器 ID; timerButton 定时刷新按钮标题.

## 刷进度

```xml
<button class='weui-btn' bindtap='refresh'>刷进度</button>
```

后台刷新按钮

```javascript
  refresh: function () {
    var self = this;
    this.setData({
      p1: pValue(self.data.p1 + 10),
      ...
    });
  },
```

`setData` 设置进度条1的进度值, 这里需要注意这个 `self` 用法. 直接在 `setData` 里面是不能用 `this.data`, 否则报告异常.

```javascript
function pValue(value) {
  return value >= 100 ? 0 : value;
}
```

`pValue` 方法对进度进行处理, 到 100 重头计数.

## 定时刷新

用 `interval` 方法,

```javascript
timerHandle: function () {
    var self = this;
    if (self.data.intervalID == 0) {
      self.setData({
        intervalID: setInterval(function () { // intervalID 保存interval ID，点击暂停时 clearInterval 清除
          self.setData({
            p1: pValue(self.data.p1 + 10),
            p2: pValue(self.data.p2 + 10),
            p3: pValue(self.data.p3 + 10),
            p4: pValue(self.data.p4 + 10),
          });
        }, 1000),
        timerButton: '暂停'
      })
    }
    else {
      clearInterval(self.data.intervalID);
      self.setData({
        intervalID: 0,
        timerButton: '定时刷新'
      })
    }
  },
```

说明, 这里面常见的错误, 会做这样的事情

```javascript
self.data.intervalID = 123;
```

在小程序里面, 记得一定要 `this.setData` 或者是在函数里面 `self.setData `.

