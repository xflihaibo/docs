# AB 压力测试

ab 是 apache 自带的压力测试工具。ab 非常实用，它不仅可以对 apache 服务器进行网站访问压力测试，也可以对或其它类型的服务器进行压力测试。比如 nginx、tomcat、IIS 等

## AB 的原理

ab 的原理：ab 命令会创建多个并发访问线程，模拟多个访问者同时对某一 URL 地址进行访问。它的测试目标是基于 URL 的，因此，它既可以用来测试 apache 的负载压力，也可以测试 nginx、lighthttp、tomcat、IIS 等其它 Web 服务器的压力。
ab 命令对发出负载的计算机要求很低，它既不会占用很高 CPU，也不会占用很多内存。但却会给目标服务器造成巨大的负载，其原理类似 CC 攻击。自己测试使用也需要注意，否则一次上太多的负载。可能造成目标服务器资源耗完，严重时甚至导致死机

## 性能指标

吞吐率（Requests per second）
概念：服务器并发处理能力的量化描述，单位是 reqs/s，指的是某个并发用户数下单位时间内处理的请求数。某个并发用户数下单位时间内能处理的最大请求数，称之为最大吞吐率。
计算公式：总请求数 / 处理完成这些请求数所花费的时间，即
Request per second = Complete requests / Time taken for tests

并发连接数（The number of concurrent connections）
概念：某个时刻服务器所接受的请求数目，简单的讲，就是一个会话。

并发用户数（The number of concurrent users，Concurrency Level）
概念：要注意区分这个概念和并发连接数之间的区别，一个用户可能同时会产生多个会话，也即连接数。

用户平均请求等待时间（Time per request）
计算公式：处理完成所有请求数所花费的时间/ （总请求数 / 并发用户数），即
Time per request = Time taken for tests /（ Complete requests / Concurrency Level）

服务器平均请求等待时间（Time per request: across all concurrent requests）
计算公式：处理完成所有请求数所花费的时间 / 总请求数，即
Time taken for / testsComplete requests
可以看到，它是吞吐率的倒数。
同时，它也=用户平均请求等待时间/并发用户数，即
Time per request / Concurrency Level

## 安装

```shell
 yum -y install httpd-tools
 ab -V 查看版本
```

## 参数

1.  -n 即 requests，用于指定压力测试总共的执行次数。
1.  -c 即 concurrency，用于指定压力测试的并发数。
1.  -t 即 timelimit，等待响应的最大时间(单位：秒)。
1.  -b 即 windowsize，TCP 发送/接收的缓冲大小(单位：字节)。
1.  -p 即 postfile，发送 POST 请求时需要上传的文件，此外还必须设置-T 参数。
1.  -u 即 putfile，发送 PUT 请求时需要上传的文件，此外还必须设置-T 参数。
1.  -T 即 content-type，用于设置 Content-Type 请求头信息，例如：application/x-www-form-urlencoded，默认值为 text/plain。
1.  -v 即 verbosity，指定打印帮助信息的冗余级别。
1.  -w 以 HTML 表格形式打印结果。
1.  -i 使用 HEAD 请求代替 GET 请求。
1.  -x 插入字符串作为 table 标签的属性。
1.  -y 插入字符串作为 tr 标签的属性。
1.  -z 插入字符串作为 td 标签的属性。
1.  -C 添加 cookie 信息，例如："Apache=1234"(可以重复该参数选项以添加多个)。
1.  -H 添加任意的请求头，例如："Accept-Encoding: gzip"，请求头将会添加在现有的多个请求头之后(可以重复该参数选项以添加多个)。
1.  -A 添加一个基本的网络认证信息，用户名和密码之间用英文冒号隔开。
1.  -P 添加一个基本的代理认证信息，用户名和密码之间用英文冒号隔开。
1.  -X 指定使用的代理服务器和端口号，例如:"126.10.10.3:88"。
1.  -V 打印版本号并退出。
1.  -k 使用 HTTP 的 KeepAlive 特性。
1.  -d 不显示百分比。
1.  -S 不显示预估和警告信息。
1.  -g 输出结果信息到 gnuplot 格式的文件中。
1.  -e 输出结果信息到 CSV 格式的文件中。
1.  -r 指定接收到错误信息时不退出程序。
1.  -h 显示用法信息，其实就是 ab -help。

## 方式

```shell
//测试GET 接口，需要cookie
ab -n 5000 -c 500 -C uin=7000000；session=99999999 url

//测试POST接口，需要JSON格式请求体
ab -n 5000 -c 300 -p post.txt -T 'application/json' url
//其中，-p 表示需要携带的请求体，一般是.txt格式文件，文件内容如下：{"toBank":"123456"}; -T 表示请求体格式，一般为’application/json’
```

## 其他测试

[loadtest](https://github.com/alexfernandez/loadtest)
