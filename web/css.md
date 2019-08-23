# CSS

## hover link active, visite 定义顺序

?> link > visite > hover > active

## 盒子模型

#### 标准的 CSS 的盒子模型？与低版本 IE 的盒子模型有什么不同的

-   标准盒子模型：宽度=内容的宽度（content）+ border + padding + margin
-   低版本 IE 盒子模型：宽度=内容宽度（content+border+padding）+ margin

#### box-sizing 属性

-   用来控制元素的盒子模型的解析模式，默认为 content-box
-   context-box：W3C 的标准盒子模型，设置元素的 height/width 属性指的是 content 部分的高/宽
-   border-box：IE 传统盒子模型。设置元素的 height/width 属性指的是 border + padding + content 部分的高/宽

## BFC

#### BFC (块级格式化上下文：block formatting context)的理解

-   内部的 Box 会在垂直方向上一个接一个放置。
-   Box 垂直方向的距离由 margin 决定，属于同一个 BFC 的两个相邻 Box 的 margin 会发生重叠。
-   每个元素的 margin box 的左边，与包含块 border box 的左边相接触。
-   BFC 的区域不会与 float box 重叠。
-   BFC 是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。
-   计算 BFC 的高度时，浮动元素也会参与计算。

##### 触发 BFC 的条件

-   根元素，即 html
-   float 的值不为 none（默认）
-   overflow 的值不为 visible（默认）
-   display 的值为 inline-block、table-cell、table-caption
-   position 的值为 absolute 或 fixed

### BFC 解决的相关问题

#### li 与 li 之间有看不见的空白间隔是什么原因引起的？有什么解决办法？

-   行框的排列会受到中间空白（回车空格）等的影响，因为空格也属于字符,这些空白也会被应用样式，占据空间，所以会有间隔，把字符大小设为 0，就没有空格了。
-   也可以将<li>代码全部写在一排
-   浮动 li 中 float：left
-   在 ul 中用 font-size：0（谷歌不支持）；可以使用 letter-space：-2px

#### 垂直 margin 重叠问题

🤔 这里提到 margin，就不得不提一下 margin 的这一特性——垂直重叠。如 p 标签 的垂直 margin 是 16px，那么两个 p 标签之间纵向的距离是多少？按常理来说应该是 16 + 16 = 32px，但是答案仍然是 16px。

!> 因为垂直的 margin 是会重叠的，如果两者不一样大的话，大的会把小的“吃掉"

## css 分层理论

### oocss

[OOCSS](https://github.com/stubbornella/oocss/wiki) 面向对象的 CSS 有个特点就是结构和皮肤是分开的, 减少对 HTML 结构的依赖,强调重复使用 class，而应该避免使用 id 作为 CSS 的选择器

### SMACSS

[SMACSS](http://smacss.com/) 像 OOCSS 一样以减少重复样式为基础。然而 SMACSS 使用一套五个层次来划分 CSS 给项目带来更结构化的方法

-   Base (基本):用来重置元素的基本样式(颜色、排版、外距和内距等)
-   Layout（布局）:布局是一个网站的基本，无论是左右还是居中，甚至其他什么布局，要实现页面的基本浏览功能，布局必不可少
-   Module (模块):模块是独立的，可重用的组件
-   State (状态):状态经常和 JavaScript 放在一起使用，它是一种用来标识页面状态
-   Theme (皮肤):主题就是皮肤，和 OOCSS 的分离皮肤与结构不谋而合,这样的话更换加载的 theme 文件即可将皮肤更换

### Bem

[bem](http://getbem.com/naming/) 最流行的命名规则之一就是 BEM（block：块，Element：元素，Modifier：修饰符）。通过给每个元素添加它的父级 block 模块作为前缀，使得目标的安全性变得更加简单了。BEM 还有助于消除页面和 body 类对嵌套或者附加样式依赖。

```css
.block {
}
.block__element {
}
.block--theme {
}
```

### Suit

[suit](https://suitcss.github.io/) 起源于 bem，但是它对组件名使用驼峰式和连字号把组件从他们的修饰和子孙后代中区分出来

```css
.MyComponent {
}
.MyComponent.is-animating {
}
.MyComponent--modifier {
}

.MyComponent-part {
}
.MyComponent-anotherPart {
}
```

### 常用的 CSS 库

#### reset.css

> [reset.css](https://meyerweb.com/eric/tools/css/reset/)杀伤力也较大，会把我们想要的不想要的都给设置一个初始样式做了一个统一回归

#### normalize.css

> [normalize](http://necolas.github.io/normalize.css/)它只给 body 设置了 padding:0;margin:0;它做的是保证每个浏览器显示效果统一，相当于一种补充，但是有些默认的还没置掉，支队 body 做了重置

#### neat.css

> [neat.css](http://thx.github.io/cube/)它是基于 normalize 和 reset 结合的,解决低级浏览器 Bug（这是 normalize 的优点）,统一效果，但不盲目重置为 0,向后兼容

### cssnext

> [cssnext](https://cssnext.github.io) 把 新 CSS 规范转换成兼容性更强的 CSS，

```css
:root {
    --mainColor: #12345678;
}

body {
    background: var(--mainColor);
}
```

## FPS

多数显示器默认频率是 60Hz，即 1 秒刷新 60 次，所以理论上最小间隔为 1/60＊1000ms ＝ 16.7ms。
requestAnimationFrame
