## task1 判断语句的基本使用

判断输入内容`input`是否为数字且大于5，是则将数字加上10之后再判断是否大于20，是则输出`true`，否则输出`false`，如果第一次判断为假，则直接输出`input`的值

```js init
var x = input
```

```js input
[1, 7, 'string', true, 6, Symbol('a')];
```

```js judger
assert(output.length === 1, '输出数目不对！！');
if (typeof input === 'number' && input > 5) {
    assert(output[0] === input + 10 > 20, ' [[input + 10]] 后的第二次判断错误！！');
} else assert(output[0] === input, '判断正确，应当执行else内的语句，但输出值与 [[input]] 不同');
```

## task2 循环的基本使用

请用循环输出一个直角边为输入值`input`的用`#`填充的等腰直角三角形，示例如下：

输入5，输出以下内容

\#

\##

\###

\####

\#####

```js init
var lines = input;
```

```js input
[6, 33, 86, 34, 56, 38];
```

```js judger
assert(output.length === input, '输出数量不对！！');
assert(output.every((v, i) => v.length === i + 1 && /^#+$/.test(v)));
```

## task3 开方运算

我们给出给 `m` 开 `n` 次方根的运算公式

`x = m / (n * x ** (n - 1)) + (n - 1) * x / n`

其中`x`的初始值是`m`。该公式运算次数越多，结果越准确。

下面，你需要对输入的数字开3次方，并输出运算10次以后的结果

```js init
var m = input;
var n = 3;
var x = m;
```

```js input
[3, 8, 6, 999, 1248162, 18412.123];
```

```js judger
let x = input;
for (let i = 0; i < 10; i++) {
    x = input / (3 * x ** 2) + 2 * x / 3;
}
assert(x === output[0] && output.length === 1);
```