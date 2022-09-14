# 第三章 第三节 CSS入门

## CSS 概述

CSS 是什么？首先我们望文生义一波，CSS 是 Cascading Style Sheets 简单机翻可以认为是层叠样式表，简单来说，这是一种用于控制 html 样式的语言。

一个简单的CSS语句如下：

```css
#app {
    color: red;
}
```

其中 `#app` 是CSS的选择器 (Selector) ，选择器用于指向一个或多个HTML元素，而 `{}` 包裹的 `color: red;` 则是实际要添加给元素的样式。（也就是说，HTML的样式是以元素为单位的

## 如何添加CSS

添加CSS与添加js类似，一个简单的方法是以`<style>`标签引入，像这样：

```html
<style>
    #app {
        color: red;
    }
</style>
```

另一种则是编写一个单独的文件（以.css 作为后缀名），随后引入到html中

```html
<link type="text/css" href="css文件的地址" rel="stylesheet">
```

## 选择器

作为CSS学习的第一步，我们先来看下选择器的语法

### 标签选择器

最朴素的选择器是标签选择器，这个选择器可以选中所有同种标签，例如说 `p` 能匹配所有的

```html
<p></p>
```

浏览器正是使用这个选择器给各种标签附加默认样式的

### ID选择器

一种常用的选择器是ID选择器，它的语法形如 `#ID`，它能匹配对应id的元素，例如说`#game-draw`能匹配

```html
<div id="game-draw"></div>
```

> 1. 通常来说，id应该是唯一的
> 2. css 的命名规则与js不同，对于多个单词的情况，会使用横杠分割，而非驼峰

#### `试一试`

阅读样板的`index.html` 尝试将状态栏中的攻击力数值设置为红色。

提示，这个数值对应的标签是：

```html
<p class='statusLabel statusText' id='atk'></p>
```

### 类选择器

如果你有选择多个元素的需求，就需要类选择器了，类选择器的语法形如 `.class`，它能匹配所有拥有对应类的元素，例如说`.game-canvas` 能匹配

```html
<canvas class="game-canvas"></canvas>
```

更进一步的，一个标签的 class 属性中可以包含多个类，多个类用空格分割，类选择器可以选中所有拥有指定类的标签，例如说上面的选择器可以选中下面这个标签。

```html
<canvas class="game-canvas active"></canvas>
```

#### `试一试`

阅读样板的`index.html` 尝试将状态栏中的所有数值设置为蓝色。

### 多个选择器

你可以组合上面这三个选择器，

### 父选择器

例如说，`#app div` 可以匹配

```html
<div id="app">
    <div></div>
    <a></a>
</div>
```

### 

### 通配选择器

你可以使用通配

### 伪类选择器

伪类是一个令人摸不着头脑的词汇，这个选择器的实际用途是用于选择处于特定状态的元素，例如说 `:hover` 选择器可以匹配鼠标悬停于其上的元素。`:hover` 选择器可以匹配

```

```

#### `试一试`

阅读样板的`index.html` 尝试使状态栏中的数值在被悬停时表现为蓝色。

## 常用属性概述

CSS属性众多，同时难度较低，因此以下仅仅列出一些常用属性，并梳理基本的规则。要想用好CSS，还是需要长期积累学习。

### 干预表现的属性

所谓干预表现，指的是这个属性只影响标签本身的显示，对于其他元素则没有影响，这一类的属性往往是继承的

#### 文本相关的属性

一个最常用的属性是 `color`，css 内置了一系列颜色名，除此之外，你也可以使用十六进制颜色码或者`rgb` / `rgba` 函数来指定颜色，像这样

```css
* {
    color: red;
    color: #000000;
    color: rgb(0, 0, 0);
    color: rgba(0, 0, 0, 0.5);
}
```

另一个值得一提的是 `font` 系列，这个系列用于控制文本的字体，它包括以下一组属性：

```css
* {
    /** 字体样式 普通(normal) - 斜体(italic) */
    font-style: normal;
    /** 字体变体，包括连字符之类的设定，不常用 */
    font-variant: normal;
    /** 字体粗细 */
    font-weight: bold;
    /** 字体大小 */
    font-size: 14px;
    /** 行高 */
    line-height: 2;
    /** 字体族 */
    font-family: Consolas, monospace;
}
```

特别的，你可以使用 `font` 简写属性来替代所有这些属性，具体来说，你可以直接在font属性里按照上面列出的顺序填每个属性的值，如果不需要设置某个属性，则可直接留空，特别的，`font-size` 和 `font-family` 必须填写：

```css
* {
    font: bold 14px Consolas;
}
```

#### 背景

css 提供了一系列用于控制背景的属性：

```css
* {
    background-clip
    background-color
    background-image
    background-origin
    background-position
    background-size
    background-repeat
    background-attachment
}
```

#### 其他

以下列出一些可能有用的属性，你可以在 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS) 上查阅它们

`opacity` 属性可以控制元素的透明度，其值为 0 ~ 1
`curosr` 属性可以控制鼠标在元素上时的指针形式
`box-shadow` 属性可以控制元素的阴影效果

### 干预布局的属性

#### position

#### 盒模型



#### display
