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

一个标准的`html`文档如下所示，在其开头的是一个特别的标签`<!DOCTYPE html>`，表示这是一个`html`文件，然后，整个`html`文件的根标签是`html`，其下有两个标签`<head>`和`<body>`，各自用于容纳不同的标签，`<head>`中的标签用于表示页面本身的属性和资源，`<body>`中的标签则实际显示在页面中

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

## \<title>

`title`标签决定了页面的标题，它往往被放置于`head`中，其用法如下所示

```html
<head>
    <title>混沌幻想3 - h5魔塔</title>  
</head>
```

## \<script>

`script`标签被用于嵌入`javascript`脚本，你可以在其中直接编写js代码，例如说：

```html
<script>
    console.log("hello, world");
</script>
```

也可以从指定位置引入一个js文件

```html
<script src="/assets/promise.min.js"></script>
```

## \<div>

```html
<div>1</div>
<div>2</div>
```

## \<span>

```html
<span>1</span>
<span>2</span>
```

## \<img>

```html
<img src="/assets/toWish.jpg" />
```

## \<input>



## \<audio>



# 开发者工具
