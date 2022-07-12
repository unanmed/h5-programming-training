# 第三章 第二节 HTML入门

`HTML5`这个词想必大家经常看见（这个网站上满地都是），不过，在`H5`上，会`HTML`的人少之又少，本节课我们会讲解有关`HTML`的基础知识

`HTML`的全称是超文本标记语言(HyperText Markup Language)，它并不是编程语言，而是一种声明式的语言，也就是说它没有顺序，只是一些内容。我们在网页上看到的所有东西，都是由html渲染出来的。

`HTML` 由一组标签组成，一个基础的标签形式如下

```html
<div prop="a">
    <!-- 子标签或者文本 -->
</div>
```

其中`<>`中的部分是标签体，最前面的一串字符是标签名（这里是`div`），在标签体中可以以`属性名="属性值"`的方式声明一系列的属性，特别的，也可以声明仅有属性名的属性。而`</>` 中的部分是闭合标签，与标签体一一匹配，两者之间的部分可以容纳子标签或者文本，这种结构在计算机中被称为`树`，因为它就像树一样，不断分叉。

一个标准的`html`文档如下所示，在其开头的是一个特别的标签`<!DOCTYPE html>`，表示这是一个`html`文件，然后，整个`html`文件的根标签是`<html>`，其下有两个标签`<head>`和`<body>`，各自用于容纳不同的标签，`<head>`中的标签用于表示页面本身的属性和资源，`<body>`中的标签则实际显示在页面中

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        
    </head>
    <body>
        
    </body>
</html>
```

接下来，我们会讲解一些简单的标签

## 显示类的标签

在 `<body>` 中，`html`提供了大量能实际渲染到页面上的元素，由于数量较多，这里不进行赘述，可以点击链接查看文档

布局类：
 - [<div>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/div) 块
 - [<span>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/span) 文本段

文本类：
 - [<p>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/p) 段落
 - [<h1>~<h6>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Heading_Elements) 标题

交互类：
 - [<a>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a) 链接
 - [<button>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/button) 按钮
 - [<input>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input) 输入框
 - [<textarea>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/textarea) 文本框

展示类：
 - [<img>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img) 图片

 - [<ul>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/ul) 无序列表
 - [<li>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/li) 列表项

 - [<table>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/table) 表格
 - [<thead>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/thead) 表头
 - [<tbody>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/tbody) 表体
 - [<tr>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/tr) 表格行
 - [<td>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/td) 表格单元

 - [<audio>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/audio) 音乐
 - [<video>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/video) 视频

## \<title>

`<title>`标签决定了页面的标题，它往往被放置于`<head>`中，其用法如下所示

```html
<head>
    <title>混沌幻想3 - h5魔塔</title>  
</head>
```

## \<script>

`<script>`标签被用于嵌入`javascript`脚本，你可以在其中直接编写js代码，例如说：

```html
<script>
    console.log("hello, world");
</script>
```

也可以从指定位置引入一个js文件

```html
<script src="/assets/promise.min.js"></script>
```

`<script>` 标签会阻塞 `html` 的解析，只有当一个脚本执行完，才会显示后续的元素，因此出于各自考虑，会将 `<script>` 标签放到文件的最后
