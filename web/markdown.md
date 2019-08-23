# 欢迎使用马克飞象

@(示例笔记本)[马克飞象|帮助|Markdown]

**马克飞象**是一款专为印象笔记（Evernote）打造的 Markdown 编辑器，通过精心的设计与技术实现，配合印象笔记强大的存储和同步功能，带来前所未有的书写体验。特点概述：

-   **功能丰富** ：支持高亮代码块、_LaTeX_ 公式、流程图，本地图片以及附件上传，甚至截图粘贴，工作学习好帮手；
-   **得心应手** ：简洁高效的编辑器，提供[桌面客户端][1]以及[离线 Chrome App][2]，支持移动端 Web；
-   **深度整合** ：支持选择笔记本和添加标签，支持从印象笔记跳转编辑，轻松管理。

---

[TOC]

## Markdown 简介

> Markdown 是一种轻量级标记语言，它允许人们使用易读易写的纯文本格式编写文档，然后转换成格式丰富的 HTML 页面。 —— [维基百科](https://zh.wikipedia.org/wiki/Markdown)

正如您在阅读的这份文档，它使用简单的符号标识不同的标题，将某些文字标记为**粗体**或者*斜体*，创建一个[链接](http://www.example.com)或一个脚注[^demo]。下面列举了几个高级功能，更多语法请按`Cmd + /`查看帮助。

### 代码块

```python
@requires_authorization
def somefunc(param1='', param2=0):
    '''A docstring'''
    if param1 > param2: # interesting
        print 'Greater'
    return (param2 - param1 + 1) or None
class SomeClass:
    pass
>>> message = '''interpreter
... prompt'''
```

### LaTeX 公式

可以创建行内公式，例如 $\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$。或者块级公式：

$$ x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a} $$

### 表格

| Item     |    Value | Qty |
| :------- | -------: | :-: |
| Computer | 1600 USD |  5  |
| Phone    |   12 USD | 12  |
| Pipe     |    1 USD | 234 |

### 流程图

```flow
st=>start: Start
e=>end
op=>operation: My Operation
cond=>condition: Yes or No?

st->op->cond
cond(yes)->e
cond(no)->op
```

以及时序图:

```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```

> **提示：**想了解更多，请查看**流程图**[语法][3]以及**时序图**[语法][4]。

### 复选框

使用 `- [ ]` 和 `- [x]` 语法可以创建复选框，实现 todo-list 等功能。例如：

-   [x] 已完成事项
-   [x] 待办事项 1
-   [ ] 待办事项 2

> **注意：**目前支持尚不完全，在印象笔记中勾选复选框是无效、不能同步的，所以必须在**马克飞象**中修改 Markdown 原文才可生效。下个版本将会全面支持。

## 印象笔记相关

### 笔记本和标签

**马克飞象**增加了`@(笔记本)[标签A|标签B]`语法, 以选择笔记本和添加标签。 **绑定账号后**， 输入`(`自动会出现笔记本列表，请从中选择。

### 笔记标题

**马克飞象**会自动使用文档内出现的第一个标题作为笔记标题。例如本文，就是第一行的 `欢迎使用马克飞象`。

### 快捷编辑

保存在印象笔记中的笔记，右上角会有一个红色的编辑按钮，点击后会回到**马克飞象**中打开并编辑该笔记。

> **注意：** 目前用户在印象笔记中单方面做的任何修改，马克飞象是无法自动感知和更新的。所以请务必回到马克飞象编辑。

### 数据同步

**马克飞象**通过**将 Markdown 原文以隐藏内容保存在笔记中**的精妙设计，实现了对 Markdown 的存储和再次编辑。既解决了其他产品只是单向导出 HTML 的单薄，又规避了服务端存储 Markdown 带来的隐私安全问题。这样，服务端仅作为对印象笔记 API 调用和数据转换之用。

> **隐私声明：用户所有的笔记数据，均保存在印象笔记中。马克飞象不存储用户的任何笔记数据。**

### 离线存储

**马克飞象**使用浏览器离线存储将内容实时保存在本地，不必担心网络断掉或浏览器崩溃。为了节省空间和避免冲突，已同步至印象笔记并且不再修改的笔记将删除部分本地缓存，不过依然可以随时通过`文档管理`打开。

> **注意：** 虽然浏览器存储大部分时候都比较可靠，但印象笔记作为专业云存储，更值得信赖。以防万一，**请务必经常及时同步到印象笔记**。

## 编辑器相关

### 设置

右侧系统菜单（快捷键`Cmd + M`）的`设置`中，提供了界面字体、字号、自定义 CSS、vim/emacs 键盘模式等高级选项。

### 快捷键

帮助 `Cmd + /`
同步文档 `Cmd + S`
创建文档 `Cmd + Opt + N`
最大化编辑器 `Cmd + Enter`
预览文档 `Cmd + Opt + Enter`
文档管理 `Cmd + O`
系统菜单 `Cmd + M`

## 文档成熟的框架

docz https://www.docz.site/
vuepress：https://vuepress.vuejs.org/zh/
docsify: https://vuepress.vuejs.org/zh/
storybook :https://storybook.js.org/
