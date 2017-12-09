# X天小程序开发速度入门(UI)--第9天

> 今天开始练习基础组件，以登录注册功能为例，练习`view` `input` `navigator`组件
> 了解如何引入 [weui-wxss 微信样式](https://github.com/weui/weui-wxss)

## 开发步骤
### 新建项目

1 打开开发工具，新建项目
2 新建  weixin-app-tutorialx  目录
   * 项目目录指到 {你的目录}/weixin-app-tutorialx
   * AppID 暂不指定
   * 项目名称 tutorialx
3 新增页面
   * Pages 目录右键，新建目录，register
   * register 目录右键，新建Page，register
   * app.json 中 "pages" 数组增加 "pages/register/register"

### 引入微信样式
[weui-wxss 微信样式](https://github.com/weui/weui-wxss)

* 下载zip文件
* 或 github clone 项目到本地
* dist 目录下 style 文件夹 拷贝到 weixin-app-tutorialx  目录
* app.wxss 开头加入 `@import 'style/weui.wxss';` 
   * 全局引入 weui 样式（后面的页面会引用到）

### 编写登录界面
登录界面包含：

* 标题：主标题与副标题，用 view 组件
* 输入：用户名及密码输入，用 view+input
* 登录按钮：button
* 底部：链接（登录|注册）

注册界面包含：

* 标题：主标题与副标题，用 view 组件
* 输入：手机号及验证码输入，用 view+input+view
* 注册按钮：button
* 底部：链接（登录|注册）

### 用法说明
在 wxml 中，view 起的作用很大

* 作为 container 容器，包含其他组件，view 也可以嵌套 view
* 本身可以作为文字显示
   * 开始以为 "用户名" 这样的内容用的是 label 组件，后来发现，view + 样式(weui-label) 就可以解决
   * "获取验证码" 也可以是这么处理，用 weui-vcode-btn 样式
* button 按钮，样式定义为 weui-btn， type 定义为 primary，就可以达成微信中常见的（单行）按钮
* 底部通常会给出链接和版权信息
   * 通过 view + 样式来实现
   * 链接采用 navigator 组件，在 url 中指定链接
      * 这里跳转到页面，url 的做法是 `url="../register/register"`

## 总结
* 常用组件 view 作为容器和组织内容需要熟练掌握
* 引入 weui 的样式可以方便地达成微信风格样式
* 不同的小程序外观千差万别，主要就是 WXSS 样式，可以多搜集和学习