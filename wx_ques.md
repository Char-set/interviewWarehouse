1.小程序的相关文件类型有哪些？

    Wxml：构建页面结构

    Wxss：定义样式

    Js：处理逻辑，网络请求

    Json：小程序或页面的配置文件，配置一些页面或者小程序属性，如页面标题

2.简述微信小程序原理

    小程序采用JavaScript、Wxml、Wxss三种技术开发，本质是一个单页面应用，所有的页面渲染和事件处理
    都在一个页面中进行，但又可以调用微信客户端调用系统原生的很多接口。小程序是数据驱动的架构模式，
    它的UI和数据是分离的，页面上所有的变化，都需要通过改变数据来实现。

    小程序分为webview和appService两个部分。webview负责UI的展现，appService负责逻辑处理、接口调用。
    它们在两个进程中运行，通过微信的JSBridge桥梁进行通信。

3.小程序的双向绑定怎么实现的

    小程序的数据改动，例如this.data.title = ‘改变title’，是不会自动同步到wxml上的，必须通过
    this.setData({
        title: ‘改变title’’
    })
    来同步到wxml上

4.小程序的wxss和css有哪些不一样的地方

    两者大部分都一样，小程序新增了尺寸单位rpx

5.小程序页面间有哪些传递数据的方法

（1）：通过全局变量，在app.js中定义变量globalData，下一个页面通过getApp().globalData 获取

（2）：在跳转的时候，通过在url上设置参数，下一个页面在onload生命周期中，通过参数options获取

6.小程序的生命周期

    onLaunch，onShow，onHide，onError

    页面生命周期：onLoad，onShow，onReady，onHide，onUnload

7.微信小程序的优劣势

    优势：兼容性较好，不需要下载安装，开发成本较低

    劣势：依赖微信，入口较深，官方限制较多（小程序大小，页面最多同时打开10个）

8.bindtap和catchtap的区别是什么

    两者都可以捕获用户用户的点击事件。

    不同点：catchtap会阻止事件向上冒泡，bindtap不会

9.简述下 wx.navigateTo(), wx.redirectTo(), wx.switchTab(), wx.navigateBack(), wx.reLaunch()的区别

    wx.navigateTo()：保留当前页面，跳转到应用内的某个页面。但是不能跳到 tabbar 页面
    wx.redirectTo()：关闭当前页面，跳转到应用内的某个页面。但是不允许跳转到 tabbar 页面
    wx.switchTab()：跳转到 abBar 页面，并关闭其他所有非 tabBar 页面
    wx.navigateBack()关闭当前页面，返回上一页面或多级页面。可通过 getCurrentPages() 获取当前的页面栈，决定需要返回几层
    wx.reLaunch()：关闭所有页面，打开到应用内的某个页面

10.wxs了解么，主要用来干什么


11.小程序常见bug

    1.域名必须是 HTTPS 
    2. input 组件 placeholder 字体颜色 
    3. wx.navigateTo 无法跳转到带 tabbar 的页面 
    4. tabbar 在切换时页面数据无法刷新 
    5.如何去掉自定义 button 灰色的圆角边框 
    6.input textarea 是 APP 的原生组件，z-index 层级最高 
    7.一段文字如何换行 
    8.设置最外层标签的 margin-bottom 在 IOS 下不生效 
    9.小程序中 canvas 的图片不支持 base64 格式 
    10.回到页面顶部 
    11.wx.setStorageSync 和 wx.getStorageSync 报错问题 
    12.如何获取微信群名称？ 
    13.new Date 跨平台兼容性问题 
    14.wx.getSystemInfoSync 获取 windowHeight 不准确 
    15.图片本地资源名称，尽量使用小写命名