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

输入通过变量 input 给出，直接使用即可

```js init
var res;
var x = input;
```

```js input
[ "h5mota.com", 114514, false ];
```

```js judger
assert(res === (typeof input === 'string'));
```

## task4 用三元表达式判断表达式是否为真

请用三元表达式判断给出的变量加上5以后是否大于10，将结果用console.log输出

如果大于10，输出yes，否则输出no

变量输入为`input`，可直接使用

```js init 
var num = input;
```

```js input
[3, 77, 5, 7, 0];
```

```js judger
assert(output.length === 1);
assert(output[0] === (input + 5 > 10 ? 'yes' : 'no'));
```

## task5 使用 和 或 非

请判断`input`是否满足以下条件
- 是数字且平方后大于50
- 是数字或者是布尔型
- 非input是false

将结果依次用console.log输出

```js init
var a = input;
```

```js input
[3, 7, false, 'js-training', 9, 'true', NaN, '', 0];
```

```js judger
assert(output.length === 3);
assert(output[0] === (typeof input === 'number' && input ** 2 > 50));
assert(output[1] === (typeof input === 'number' || typeof input === 'boolean'));
assert(output[2] === !input);
```