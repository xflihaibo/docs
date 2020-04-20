# CSS

<div align="center">
  <img src="./web/img/css.jpg" width="200" alt="logo" align="center">
</div>

层叠样式表是一种用来为结构化文档（如 HTML 文档或 XML 应用）添加样式（字体、间距和颜色等）的计算机语言，由 W3C 定义和维护。当前最新版本是 CSS2.1，为 W3C 的推荐标准。CSS3 现在已被大部分现代浏览器支持，而下一版的 CSS4 仍在开发中

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

## BFC (块级格式化上下文：block formatting context)

-   内部的 Box 会在垂直方向上一个接一个放置。
-   Box 垂直方向的距离由 margin 决定，属于同一个 BFC 的两个相邻 Box 的 margin 会发生重叠。
-   每个元素的 margin box 的左边，与包含块 border box 的左边相接触。
-   BFC 的区域不会与 float box 重叠。
-   BFC 是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。
-   计算 BFC 的高度时，浮动元素也会参与计算。

#### 触发 BFC 的条件

-   根元素，即 html
-   float 的值不为 none
-   overflow 的值不为 visible（
-   display 的值为 inline-block、table-cell、table-caption, grid
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

## flex

### centent 容器

flex-direction:决定主轴方向，项目排列的方向 row, row-reverse,column,column-reverse
flex-warp:项目排列是否换行 nowarp, warp, warp-reverse

justify-content:定义容器在主轴的对齐方式 flex-start, flex-end,center,space-between,span-around
align-items:项目在 y 轴的对齐方式（单行） flex-start, flex-end,center, baseline,stretch
align-content:项目在 y 轴的对齐方式（多行） flex-start, flex-end,center, baseline,stretch

### item 子元素

order ：项目排列顺序，数值越小越靠前
flex： 定义缩放比例
align-item：单个项目在 y 轴对齐方式 flex-start, flex-end,center, baseline,stretch

## grid 布局

### centent 容器

1. grid-template-colums： 行大小（px, 百分比，auto， fr）
2. grid-template-rows: 列大小
3. grid-template-areas:网络区域

#### 内容对齐方式：

1. justify-itmes :start , end , center , stretch;
2. align-itmes :start , end , center , stretch;
3. place-items: justify-itmes ,align-itmes 缩写

#### 容器对齐方式：

1. justify-itmes:start , end , center , stretch, space-between , space-around , space-evenly;

#### 间隙

1. grid-column-gap：
2. grid-row-gap：
3. grid-gap

### itme 子元素

#### 子元素区域

grid-area:'map'

#### 子元素对齐方式

align-self:start , end , center , stretch;
justify-self:start , end , center , stretch;

## css 分层理论

[OOCSS](https://github.com/stubbornella/oocss/wiki) 其实这个东西早在 2008 年被提出,是一种新 CSS 的写法，“Object Oriented”直译就是面向对象，对于这个词，大家并不陌生，但是加上一个 CSS 也就是说 Object Oriented CSS，对于这个还是第一次见过，被叫作 OOCSS(面向对象的 CSS),

什么是面向对象的 CSS(OOCSS)“面向对象的编程”的概念,开发商之间普遍存在的,他成为任何现代编程语言的一种基本形式,数据的抽象化、模块化和继承等特点在编写代码中得到了大规模的应用。面向对象的 CSS 是一种容易重用的一种 CSS 规则,也是 OOP 的概念,从而降低了页面的加载时间,

### oocss 基本原则

1.  面向对象的 CSS 是一种容易重用的一种 CSS 规则,也是 OOP 的概念,从而降低了页面的加载时间,提高了页面的性能。
    这里关键的一点就是如何在页面中识别,创建和模块化可重用的对象,并在页面中任何需要的地方重用,并扩展其附加功能。
2.  在这里我们所说的对象其实很简单,就是指基本的 HTML 标签和 CSS 样式规则。
3.  现在最关键的,也是最具有挑战性的一点就是确定“对象”,并给这个对象创建 CSS 样式规则。
    这样一来,大家对 OOCSS 心中就有一个清晰的概念性存在了,其实 OOCSS 不是一个框架,也不是一种技术,更不是一种新的语言,他只不过是一种方法,一种书写方法,换句话说 OOCSS 其核心就是用最简单的方式编写最整洁,最于净的 CSS 代码,从而使代码更具重用性,可维护性和可扩展性。

### 举个 🌰 栗子:

传统 CSS 写法:

```code
<div class="nav"></div>

.nav {
    background: blue;
    border: 1px solid #ccc;
    margin: 5px 10px 10px;
    width: 25%;
}
```

OOCSS 写法:(样式拆分到每一个组件上)

```code
<div class="nav bgBlue solidGray mts mlm mrm mbm"></div>

.nav {width: 25%;}
.bgBlue {background:blue}
.solidGray {border: 1px solid #ccc}
.mts {margin-top: 5px}
.mrm {margin-right: 10px}
.mbm {margin-bottom: 10px}
.mlm {margin-left: 10px}
```

### 面向对象的 CSS 有两个原则:

1.  **独立的结构和样式:**就是把布局样式和设计样式独立出来。实现这一点最好的方式就是使用网格布局系统。
2.  **独立的容器和内容:**所指的是把内容从容器中分离出来,换过句话说任何对象(容器),应该适应接受任何形式的内容。

!> 综合上述,OOCSS 最关键的一点就是:提高他的灵活性和可重用性。这个也是 OOCSS 最重要的一点。

### 使用面向对象的 CSS 的理由

我们为什么要使用 OOCSS 来编写我们的样式呢?

1.  将我们的 CSS 样式更具有重用性
2.  另外也使用我们的样式变得更小
3.  第三个好处就是我们可以容易的改变一个网站的设计

如何使用面向对象的 CSS? 以下几点是创建 OOCSS 的关键部分

2.  独立的容器和内容;并且避免样式来依赖位置 把容器和内容独立出来,这样的好处是,样式组件插入到任何容器中都可以.
3.  独立的结构和样式;在给这个刚创建的对象写样式时,需要把样式和其结构独立出来。
4.  使用类名为扩展基本对象 通过对基础对象扩展类名,从而达到基础对象的可重用性。
5.  坚持以语义类来命名类名 始终坚持以逻辑和语义来给元素定义类名才是王道。
6.  创建一个组件库; 定义一个组件库中定义一个基础类,我们不应该给样式创建类似于“border,width,height,background”等样式规则,不然在不同容器中使用就会发生杯具。
7.  找出所有可重用的组件,并给这个组件创建 HTML 和 CSS 样式规则。

### 面向对象的 CSS 的优点和缺点 OOCSS 的缺点

1.OOCSS 适合真正的大型网站开发,因为大型网站用到的可重用性组件特别的多,如果运用在小型项目中可能见不到什么成效。所以用不用 OOCSS 应该根据你的项目来决定。

2.  如果没用巧妙的使用,创建组件可能对于你来说是一堆没用的东西,成为一烂摊子,给你的维护带来意想不到的悲剧,说不定还是个维护的噩梦。
3.  最好给每一个组件备写一份说明文档,有助于调用与维护

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

[reset.css](https://meyerweb.com/eric/tools/css/reset/)杀伤力也较大，会把我们想要的不想要的都给设置一个初始样式做了一个统一回归

#### normalize.css

[normalize](http://necolas.github.io/normalize.css/)它只给 body 设置了 padding:0;margin:0;它做的是保证每个浏览器显示效果统一，相当于一种补充，但是有些默认的还没置掉，支队 body 做了重置

#### neat.css

[neat.css](http://thx.github.io/cube/)它是基于 normalize 和 reset 结合的,解决低级浏览器 Bug（这是 normalize 的优点）,统一效果，但不盲目重置为 0,向后兼容

### cssnext

[cssnext](https://cssnext.github.io) 把 新 CSS 规范转换成兼容性更强的 CSS，

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
