# X天小程序开发速度入门(UI)--第26天

做 button 按钮练习的时候， form 控件提交没有获得提交的内容，今天解决了。

* 在 form 中的元素都需要指定 `name` 属性。

微信支付是一个很重要的题目，form 组件里有一个 `report-submit` 属性，提交后返回 formId 用于发送模板消息。目前只支持小程序内有微信支付接口，在小程序后台定义[模板消息](https://mp.weixin.qq.com/debug/wxadoc/dev/api/notice.html)。

开发微信支付功能时练习。