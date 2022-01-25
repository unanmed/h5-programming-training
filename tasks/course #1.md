# #1 基础语法

## task1 hello, world

输出 `hello, world` 是程序员学习一门新编程语言时会做的第一个操作，现在，你需要使用codelab来进行这一操作，请在右侧编辑器中编写代码，完成后点击下方的 `运行` 按钮。

提示：使用 `console.log` 来做输出

```js init
```

```js input
[ null ];
```

```js judger
assert(output.length === 1);
assert(output[0] === "hello, world");
```

## task2 声明一个变量

请声明一个变量 `a`, 并使其值为 `5`

```js init
```

```js input
[ null ];
```

```js judger
assert(a === 5);
```

## task3 判断变量是否是字符串

请编写代码判断给出的变量是否是字符串，并将结果输出到变量`res`中

输入通过变量 input 给出

```js init
var res;
```

```js input
[ "h5mota.com", 114514, false ];
```

```js judger
if (typeof input === 'string') {
    assert(res === true);
} else {
    assert(res === false);
}
```

## task4 


