## http 相关

## DNS 预解析

nginx 请求资源合并
多个 cdn 域名

#### HTTP 协议 TCP 三次握手四次挥手 http2.0 https

> HTTP 协议（HyperText Transfer Protocol，超文本传输协议）是用于从 WWW 服务器传输超文本到本地浏览器的传送协议。它可以使浏览器更加高效，使网络传输减少。
> 它不仅保证计算机正确快速地传输超文本文档，还确定传输文档中的哪一部分，以及哪部分内容首先显示(如文本先于图形)等;Http 协议是建立在 TCP 协议基础之上的应用层;当浏览器需要从服务器获取网页数据的时候，会发出一次 Http 请求。
> TCP 协议对应于传输层，而 HTTP 协议对应于传输层协议, 通常用 IP 地址+端口号描述通信双方、server 服务的提供方,client 服务的使用方;
> 超文本传输安全协议（英语：Hyper Text Transfer Protocol over Secure Socket Layer，缩写 HTTPS。也被称为 HTTP over TLS，HTTP over SSL 或 HTTP Secure）。 上面说到的加密协议叫 SSL，应用层（安全层） 传输层 网络层 数据链路层

#### 输入网址浏览器做了哪些

> -   DNS 解析
> -   浏览器向服务器发送 http 请求
> -   服务器向浏览器发送 html 响应
> -   浏览器接收 html 响应
> -   浏览器处理 html 相应
> -   继续处理其他请求

#### 浏览器做那些

> -   HTML 代码转化成 DOM
> -   CSS 代码转化成 CSSOM（CSS Object Model）
> -   结合 DOM 和 CSSOM，生成一棵渲染树（包含每个节点的视觉信息）
> -   生成布局（layout），即将所有渲染树的所有节点进行平面合成
> -   将布局绘制（paint）在屏幕上

#### 影响 http 的因素：

> -   1.带宽
> -   2.延迟 浏览器阻塞 一个浏览器对于同一个域名只能有四个链接（不同的浏览器不一样），如果超过了会被阻塞
> -   3.dns 查询：浏览器建立链接是需要知道服务器 IP 地址的，DNS 用来将域名解析为 ip 地址，可以通过刷新 DNS 缓存来加快速度
> -   4.建立链接：http 协议是基于 TCP 的，即使网络，浏览器再快也得进行三次握手，在高延迟的网络环境下影响比较明显

#### http 缺陷

> -   1.  耗时：每次传输都要建立链接
> -   2.不安全：http 是明文传输的，只要在路由器或者交换机上面截取，所有东西（账户，密码）都是可见的、采用 wireshark 抓包
> -   3.header 内 SPDY 容太大：通常用户的请求 header 变化的概率很小，但是每次请求都要携带大量的 header 信息，导致传输成本增加
> -   4.keepalive 压力太大：持久连接虽然有优点，但同时也会给服务器造成大量的性能压力，特别是传输图片的时候

#### SPDY

是 Google 开发的基于 TCP 的应用层协议，用以最小化网络延迟，提升网络速度，优化用户的网络使用体验。SPDY 并不是一种用于替代 HTTP 的协议，而是对 HTTP 协议的增强。新协议的功能包括数据流的多路复用、请求优先级以及 HTTP 报头压缩。

#### SPDY：综合了 HTTPS 和 HTTP 两者优点

> 1.降低延迟：才用多路复用降低延迟 2.请求优先级：给 request 设置优先级，这样子重要的请求就会优先得到响应 3.头部压缩 4.服务端推送 ：比如我要请求一个 style.css 的文件，在客户端接收到这个数据的同时，服务器会把 style.js 文件推送给客户端，在客户端再来请求这个文件的时候，就可以直接从缓存中去取了

#### tcp 请求的三次握手：

> 1.客户端向服务器发起 SYN 报文：嘿，哥们，在不，我要和你通信一下？ 2.服务器接收到请求报文之后，回复 SYN+ACK 报文，并未这次连接分配资源：嘿，小弟弟，我收到你的请求了，我这边 ok 了， 3.客户端接收到服务器的确认报文之后再一次发送 ACK 报文给服务器：嘿哥们，我也准备好了；ok 这就是三次握手

#### tcp 断开的四次挥手

> 1.客户端发起中断请求，发送 FIN 报文给服务器：”嘿，哥们，我客户端没有数据给你了，要断开哦“ 2.服务器接收到客户端请求，立即发送 ACK 确认报文：“嘿，小弟弟，你的请求我收到了，但是我还没准备好，等我一下” 3.服务器确认数据发送完毕之后，再次发送 FIN 报文给客户端：“嘿，小弟弟，我这边数据发送完毕了，准备好关闭了哦” 4.客户端接收到服务器的关闭通知之后，发送 ACK 确认报文：“嘿，哥们，你关闭吧”
> 这样子之后，服务端收到确认报文，直接断开连接，客户端等待 2ms 之后依然没有收到回复，证明服务端已经关闭了，ok，这样子客户端也关闭了

#### http 协议

-   网络超文本协议传输
-   由 请求和响应组成
-   一次 http 操作称为一个事务
-   pequest-uri
-   cookie 服务器响应 http 设置的生成
-   cookie 浏览器通过 js 设置的

#### http2.0

-   使用二进制传输
-   报头压缩
-   多路复用 一个网络连接实现并行请求
-   服务器主动推送,减少请求延迟
-   流量控制 优先级设置

#### 常见 http 状态码

```javascript
     200 ok
     206 断点续传
     301 暂时本地重定向
     302 永久本地重定向
     304 本地缓存文件
     401 token 失效请求未经授权
     403  没有权限
     404  找不到文件
     405 请求方式错误 get post
     415 请求数据方式错误 json form
     500 server错误
     502 服务器挂了
     503 服务器不可用
     504 超时
```

#### 强缓存

> -   开启 expires
> -   expires 30d;
> -   add_header Cache-Control no-cache;
> -   Cache-Control 新版本

#### 协商缓存

-   开启 etag on 空间换时间 文件过大性能很差
-   last-modified if-modified-since

#### 跨域

img ,
script,
link,
jsonp ,
iframe,
postMessage,
webSocket、
http-proxy,
nginx,

```javascript
    A page
    let frame=document.getElementById('frame');
    frame.contentWindow.postMessage('hahha',"http://localhost:3000")
    B page
    window.onmessage=functiopn(e){
    consoel.log(e.data)
    e.source.postMessage('hehehh',e.origin)
    }
```

location.Hash、

```javascript
    c.html
    <script>
        console.log(location.hash)
        let iframe=docuemnt.createElement('iframe');
        ifrime.src="http://localhost:3000/b.html#hhehehe"
        document.body.appendChild('iframe')
    </script>
    b.html
     <script>
        window.parent.parent.location.hash=location.hash
     </script>

    A.html
    <iframe src="http://localhost:4000/c.html#hqhqh" id="iframe"></iframe>
    <script>
    let iframe =docuemnt.getElementById('iframe');
    window.onhashchange=function(){
        console.log.log(location.hash)
    }

    </script>
```

cors、

```javascript
setHeader('Access_Control_Allow-Origin', 'http://localhost:3000');
```

document.domain
//根域名相同

```javascript
a.html; //a.bb.com

    <script>
    document.domain=bb.com
        var a=109;
    </script>
b.html; b.bb.com
<
    <iframe src="http://a.bb.com/a.html" id="iframe" onload="load()"></iframe>
    <script>
    document.domain=bb.com
    function load(){
           let iframe =docuemnt.getElementById('iframe');
          iframe.contentWindow.a;
    }
    </script>
```

window.name

```javascript
    c.html
    <script>
        window.name="666";
    </script>
    A.html
    <iframe src="http://localhost:4000/c.html" id="iframe" onload="load()"></iframe>
    <script>
    function load(){
        let first =true;
           let iframe =docuemnt.getElementById('iframe');
        if(first){

             iframe.src='http:http://localhost:3000/b.html';
             first =false;
            }else{
                console.log(iframe.contentWindow.name)
            }
    }
    </script>
```

#### 埋点

> navigator.sendBeacon('a.html')
