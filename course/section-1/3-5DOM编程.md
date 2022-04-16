# 第三章 第五节 DOM 编程

> 阅读本节前，你需要有HTML和CSS的一些基础知识
> 本教程的这些章节暂时摸了
> 你可以从菜鸟教程的[HTML教程](https://www.runoob.com/html/html-tutorial.html) 和[CSS教程](https://www.runoob.com/css/css-tutorial.html)学到对应的知识

## DOM 对象

DOM 的全称是 document object model (文档对象模型)，一个常见的称呼是 DOM 树。因为页面的 DOM 是以树的形式存在的。

> 这里的树指的是计算机科学中的一种数据结构，即一个节点有一个或多个子节点，像树一样分叉，直至叶节点。

DOM 是浏览器对页面元素进行的映射，用以提供用JS操作页面元素的能力。大多数标签被映射为一个 HTMLElement 对象，这是本节课讲解的重点

## 获取 DOM

页面的 DOM 树被存放在 document 对象中，如果要获得一个 dom 对象，最简单的选择是访问 `document.body` ，这个对象代表页面的 `<body>` 元素

要获取页面 DOM 树上指定的元素，你可以考虑使用 getElement 系列方法

首先是 `document.getElementById` ，这个方法允许你获得id为指定值的元素，特别的，在有多个id相同的元素的情况下，只会获取第一个元素，因此应该尽量避免id重复，以免发生意料外的情况。

```html
<div id="timer"></div>
```

```js
document.getElementById("timer"); // <div id="timer"></div>
```

如果你需要获取一系列的元素，可以考虑使用 `document.getElementsByClassName` 
，这个方法能获取拥有指定 `class` 的元素

```html
<div class="timer"></div>
<div class="timer"></div>
```

```js
document.getElementsByClassName("timer"); // HTMLCollection(2)
```

特别的，这个元素的返回值并不是数组，而是一个类数组 HTMLCollection，这个类数组的内容会动态的变化，如果你向页面上新增一个拥有这个类的元素，那么类数组中也同样会新增这个元素。

类似的， `document.getElementsByTagName` 方法提供获取所有某种标签的元素的方法。

这组方法拥有很好的性能，但是设计上并不便于使用，流行一时的DOM操作库jquery设计了一组使用css选择器获取元素的方法，后来它们被吸收为浏览器的标准方法。

你可以用 `document.querySelector` 获取第一个符合选择器的元素

```html
<div></div>
<div class="timer"></div>
```

```js
document.querySelector("div.timer"); // <div class="timer"></div>
```

```html
<div></div>
<div class="timer"></div>
```
`document.querySelectorAll` 则能让你获取所有符合要求的元素

```js
document.querySelectorAll("div.timer"); // NodeList(1)
```

与 `document.getElementsByClassName` 类似，这个方法返回的也是一个类数组，但是这个类数组并不会动态变化（奇怪的设计

> 如果你还没有学习过css选择器，可以看看[这个](https://www.w3school.com.cn/cssref/css_selectors.asp)

## 操作 DOM

HTMLElement 是页面元素的直接映射，因此对 HTMLElement 的任何操作都会简单的反馈到页面元素上

### 修改 DOM 属性

一般的，HTMLElement 对象的属性由标签属性映射而来，因此你可以直接这么操作：

```html
<a id="a"></a>
```

```js
document.getElementById("a").href = "https://h5mota.com"
```

得到的标签与 `<a id="a" href="https://h5mota.com"></a>` 是等价的

特别的，`style` 和 `class` 属性有不同的操作方法

`style` 属性被映射为一个对象，因此你可以直接操作每一个具体的属性，而不是输入一个字符串

```html
<a id="a"></a>
```

```js
document.getElementById("a").style.color = "#aaa";
```

`class` 属性则提供了一个额外的属性 `classList`，这个对象提供了一组操作class列表的方法，你可以用 `contains` 方法判断元素是否具有某个类名，用 `add` 方法添加新的类名，用 `remove` 方法去掉指定的类名，用 `toggle` 方法切换一个类名是否存在

```html
<div class="a"></div>
```

```js
var elm = document.querySelector("div.a");
elm.classList.contains("a"); // true
elm.classList.remove("a");
elm.classList.contains("a"); // false
elm.classList.add("b");
elm.classList.contains("b"); // true
elm.classList.toggle("b");
elm.classList.contains("b"); // false
```

除了与标签的属性对应的属性外，HTMLElement还提供一个特别的属性 `innerHTML`，这个属性对应标签的所有子标签，一旦进行修改，浏览器就会重新分析子节点

```html
<div id="app"><a></a></div>
```

```js
document.getElementById("app").innerHTML = "<b></b>";
// <div id="app"><b></b></div>
```

这个属性有种种妙用，但是有的时候它显得太过强大，例如说，当我们想用这个属性显示用户发言时，用户可能在发言中夹带html代码，一些有意构造的代码能破坏网页结构，甚至能窃取用户信息（网站就曾经被invgod这么搞过）

作为替代，你可以使用 innerText 属性，这个属性的修改仅限于文本，不会进行html的解析

如果需要像 style 那样获取子节点，可以访问 `children` 属性，这是一个包含了所有子节点的类数组，除此之外， `nextSibling` 属性代表元素的上一个元素，`previousSibling` 则代表下一个元素，`parent` 代表元素的父节点。

### 创建 DOM

你可以自己创建 HTMLElement ，浏览器提供了 `document.createElement` 方法来完成这个任务，提供标签名，这个方法就会创建一个对应的标签

```js
document.createElement("a"); // <a></a>
```

除此以外，一些标签还拥有专门的对象，例如说 Image (对应`<img>`) Audio (对应`<audio>`)，可以直接通过实例化对象的方式声明元素

### 操作 DOM 树

声明的元素并不会直接在页面上显示，实际上，只有当一个元素连接到 DOM 树时，它才会被实际显示，HTMLElement 提供了 `appendChild` 方法，用于将一个元素添加为它的子节点。

```html
<div id="a"><a></a></div>
```

```js
var b = document.createElement("b");
document.getElementById("a").appendChild(b); // <div id="a"><a></a><b></b></div>
```

这个方法添加的元素会被追加到子节点的末尾，如果想要将元素插入到指定位置，需要使用`insertBefore` 方法

```html
<div id="a"><a></a></div>
```

```js
var a = document.querySelector("a");
var b = document.createElement("b");
document.getElementById("a").insertBefore(b, a); // <div id="a"><b></b><a></a></div>
```

对应的，你可以用 `removeChild` 方法将一个指定的子节点从 dom 树上移除

```html
<div id="a"><a></a></div>
```

```js
var a = document.querySelector("a");
document.getElementById("a").removeChild(a); // <div id="a"></div>
```

使用`remove`方法则可以移除元素本身

```html
<div id="a"><a></a></div>
```

```js
var a = document.querySelector("a");
a.remove(); // <div id="a"></div>
```

## DOM 事件系统

除了显示以外，DOM 还提供了一些交互的能力，这通过事件系统进行，当用户进行特定的操作时，会触发对应的事件，对应的事件监听器会被调用，进行响应。

### DOM 0 事件系统

DOM 0 事件系统是一组标签属性，属性值会被当作js代码，在被触发时执行。

一个简单的例子如下，onclick 会在元素被点击时执行。

```html
<div onclick="log()"></div>
```

```js
function log() {
    console.log("click");
}
```

你也可以以操作 DOM 的方式来设置监听器，这种情况下，浏览器还会向函数中传入一个参数 Event对象，包括事件相关的信息，不同的事件中，Event 内的信息也不同

```html
<a id="a"></a>
```

```js
var a = document.getElementById("a");
a.onclick = (e) => {
    console.log(e); // 点击事件的参数中会包括点击位置
}
```

除了信息以外，

你可以从[mdn](https://developer.mozilla.org/zh-CN/docs/Web/API/GlobalEventHandlers)获取所有可用的事件，以下列出常用的事件：

加载:

`onload` 图像 / 音频等加载完成的事件

输入：

`oninput` 输入内容的事件

`onchange` 内容改变的事件

`onkeydown` 按下按键的事件

鼠标：

`onclick` 点击元素的事件

`onmousemove` 鼠标移动的事件

`oncontextmenu` 右键点击的事件

窗口事件

`onresize` 窗口大小改变的事件

### DOM 2 事件系统

DOM 0 事件系统已经可以完成交互方面的简单需求，但是如果需要设置多个监听器，就需要 DOM 2 事件系统，这套事件系统使用 `addEventLister` 方法来添加事件

```html
<a id="a"></a>
```

```js
var a = document.getElementById("a");
a.addEventListener("click", (e) => {
    console.log(e); // 与上方写法等价
});
```

这套系统实现了dom 0 事件系统拥有的所有事件，只需要去掉 dom 0 事件系统属性开头的on，即可获得对应的事件名

你可以在[mdn](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener) 学习更多用法，并查看所有[Event类型](https://developer.mozilla.org/zh-CN/docs/Web/API/Event)
