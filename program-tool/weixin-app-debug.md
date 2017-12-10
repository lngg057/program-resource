# 微信小程序调试技巧

## 编辑快捷键
|功能| 快捷键 |
|-|-|
|多行编辑 | `CTRL+F`，`ALT+ENTER` |
|快速查找文件 | `CTRL+P` |
|快速定位编辑过的文件 | `CTRL+E` |

## 调试器面板介绍
* 调试器 Console：输入和调试代码，比起在debug里面查看变量方便很多
* 调试器 Wxml：可以直接查看wxml 转化后的界面，与chrome里面查看html的DOM模型一样
* 调试器 Source：查看源码，下断点，调试
* 调试器 AppData：查看数据非常方便，比如定义的userInfo、motto等信息
* 调试器 Storage：查看本地存储，配合清缓存调试
* 调试器 Network：查看网络调用，与后台通信时用到
* 调试器 Sensor：模拟地理位置和重力感应，高级功能（不大常用:P）

## console.log

```javascript
  getUserInfo: function(e) {
    console.log(e)
```

这是很重要的调试技巧，上面的代码把 `UserInfo` 在Console面板中打印了出来

* Source面板下断点
* 执行 `console.log(e)` 或者 直接在Console面板下输入 `console.log(e)` 回车，都可以看到返回的用户信息 