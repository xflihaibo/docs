# chrome 相关

# 快捷键

### 打开最近关闭状态

mac: Cmd+Opt+I
windows: Ctrl+Shift+I

### 快速查看 Dom 或样式

mac: Cmd+Opt+C
windows: Ctrl+Shift+C

## console

console.warn("凡人你居然敢窥视我"); //警告
console.error("天兵天将，把这个凡人给我打入地狱");//错误
console.clear()//清理控制台
console.table()//方法将它以一个漂亮的表格的形式打印出来
console.time("神机妙算"); console.timeEnd("神机妙算"); //性能测试
console.log('%c 你%c 说%c 什么%c?', 'background: #000; color: #fff','color: blue','color: red; border-bottom: 1px solid red','background: blue; color: #fff; border-radius: 50%;');

```js
//赋值给 window
window.log = console.log;
log('123');
window.log = () => {};
```

## 异步 console

console.table(await navigator.getBattery())
await navigator.storage.estimate() // 占用数 和 空闲数

## 通过'h'来隐藏

> 你可以通过简单的按一下'h'来隐藏你在元素面板中选择的元素。再次按下'h'可以使它出现。这在某些的时候是很有用的，例如你想截图，

## 使用 control!(按钮)

如果你只是想移动你当前选中的元素，在 DOM 结构中往上一点或者往下一点，而不是拖动和放置，你同样可以使用[ctrl] + [⬆] / [ctrl] + [⬇] ([⌘] + [⬆] /[⌘] + [⬇] on Mac).

## 使用 Command (命令) 菜单

> 有一些 Chrome 调试工具的功能被深深的隐藏在特别的面板中，菜单中等等。并且有一些甚至隐藏在这些地方之下。这也是为什么 Command 菜单
> 在 Chrome 的调试打开的情况下 按下 [ Ctrl]+[Shift]+[P] (or [⌘]+[Shift]+[P] on Mac)
> $0 是对我们当前选中的 html 节点的引用。 $1 是对上一次我们选择的节点的引用，$2 是对在那之前选择的节点的引用，等等。一直到 $4

## 截屏，大小通吃

> 如果你想对一个特别的 DOM 节点进行截图，选中那个节点，打开 Command 菜单并且寻找节点截图的命令。
> 更有用的是什么呢，你同样可以用这种方式全屏截图 - 使用 Capture full size screenshot

## 快速切换主题

> 在 Commands 菜单中寻找与 theme 相关的选项，以实现在明亮&暗黑两种主题之间的切换。

## 给 logs 加上时间戳

> 在 Commands 菜单中寻找 timestamps 开启 timestamps.你可以在设置(在调试工具中的

## 断点调试

与其在你的源码的不同地方去添加 console.log / console.table / console.time 等等，不如你直接使用条件判断来将它们“连接”到 Source 面板中。它们不会停止，而是会一直执行，并且当你不再需要它们的时候，有一个地方(Breakpoints section)会完美列出它们。你可以点两下鼠标把所有的都移除，它们就像一堆忍者一样消失
[断点调试](../img/chrome01.gif)

## npm 包

> 有时你只是想玩玩新出的 npm 包，现在不用再大费周章去建一个项目测试了，只需要在 Chrome 插件:Console Importer 的帮助之下，快速的在 console 中引入和测试一些 npm 库
> 运行 $i('lodash') \_.VERSION

> 只需按下 "眼睛" 符号，你就可以在那里定义任何 JavaScript 表达式。 它会不断更新，所以表达的结果将永远，存在 :-) document.querySelectorAll('h1').length

## 请求

> Request initiator 显示了调用堆栈信息 将鼠标悬停在显示的 initiator（例如 外部库）上，你将看到完整的调用堆栈，包括你的文件：
> 重新发送 XHR 的请求 Replay XHR
