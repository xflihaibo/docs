## 微信小程序

NW.js，实现的微信开发者工具

#### 微信调试 查看 wxml

微信开发者工具--->调试----->调试微信开发者工具

```shell
document.getElementsByTagName('webview')[0].showDevTools(true,null)
```

#### 微信调试版本信息

```shell
openVendor()
```

wcc:wcc 可执行程序，用于将 wxml 内容转换为 js(html) 内容 wcc xxx.wxml
执行 js \$gwx (path ,global) path ：名称

wcsc:wcsc 可执行程序，用于将 wxss 内容转换为视图可使用 js(css) 内容 wcsc xxx.wxss
DevToolProtector：

## 消息通信

webView.js 视图层 基础库
foundtion 基础库 （发布订阅 通信桥梁 ready 事件）
WeixinJSBridge：微信与网页的通信  
 on:监听原声方法调用，
publish:发布消息到对应视图层到逻辑层，
invoke:调用原生方法，
subscribe:监听对接的视图层或者逻辑层底发生的消息
exparser: wx-view 组件系统 实现了一整套的组建模型 shadowDOM 相似

wAServer.js 逻辑层 基础库
生命周期，APP/page， 路由 ，
foundtion 基础库 （发布订阅 通信桥梁 ready 事件）
WeixinJSBridge：微信与网页的通信  
 on:监听原声方法调用，
publish:发布消息到对应视图层到逻辑层，
invoke:调用原生方法，

wcc--wxml--js(html) (\$gwx) -->生成虚拟 dom 函数--dom--exparser--webView
wcsc-- wxss-- js(css)--setCssHead--head--webview

DSL:自定义语法规则

词法分析：，
语法分析：

## 框架对比

预编译：抽象语法树（词法分析，语法解析）--AST(描述代码内容) --代码改变(wepy)
缺点：需要提前定义分装规则，兼容处理

半编译半运行时框架：（myvue）

运行时框架：
