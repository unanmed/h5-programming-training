## task1 调用函数

请你调用给出的函数来处理`input`，并使用`console.log`将其结果输出

```js init
var x = input;

function root(m) {
    function qpow(a, b, p) {
        let res = 1;
        while(b) {
            if (b&1) res = res*a % p;
            a = a*a % p, b >>= 1;
        }
        return res;
    }
    for (let i = 2; i < m; i++) {
        let x = m-1;
        const mx = Math.sqrt(m);
        const has = (() => {
            for (let k = 2; k < mx; k++) {
                if (x % k === 0) {
                    if (qpow(i, (m-1)/k,m) === 1) return false;
                    while (x % k === 0) x /= k;
                }
            }
            return true;
        })();
        if (has && (x === 1 || qpow(i,(m-1)/x,m) > 1)) return i;
    }
    return -1;
}
```

```js input
[ 1800, 1801, 1 ];
```

```js judger
function root(m) {
    function qpow(a, b, p) {
        let res = 1;
        while(b) {
            if (b&1) res = res*a % p;
            a = a*a % p, b >>= 1;
        }
        return res;
    }
    for (let i = 2; i < m; i++) {
        let x = m-1;
        const mx = Math.sqrt(m);
        const has = (() => {
            for (let k = 2; k < mx; k++) {
                if (x % k === 0) {
                    if (qpow(i, (m-1)/k,m) === 1) return false;
                    while (x % k === 0) x /= k;
                }
            }
            return true;
        })();
        if (has && (x === 1 || qpow(i,(m-1)/x,m) > 1)) return i;
    }
    return -1;
}

assert(output.length === 1, "输出数量有误");
assert(root(input) === JSON.parse(output[0]), "答案错误");
```

## task2 hello, world改

编写一个名为`helloWorld`的函数，使其返回值为`"hello, world"`

```js init
```

```js input
[ null ];
```

```js judger
assert(helloWorld() === "hello, world", "返回值错误");
```

## task3 判断素数

编写一个名为`primalityTest`的函数，使其能接收一个数字参数，并且判断该参数是否是素数，返回判断结果

```js init
```

```js input
[ 3, 1, 9, 23, 4234, 88123, 100003 ];
```

```js judger
function _primalityTest(x) {
    if (x === 1) return false;
    for (let i = 2; i * i <= x; i++) {
        if (x % i === 0 && x !== i) {
            return false;
        }
    }
    return true;
}
assert(_primalityTest(input) === primalityTest(input), "判断错误");
```

## task4 max

编写一个名为`max`的函数，使其能接收任意多个数字参数，返回其中最大的一个数字

```js init
```

```js input
[ [3], [2, 1], [9, 23, 4234, 88123, 100003], [1,3,-3,31,43,-123123,44434,0,21,-1.5, 5e8] ];
```

```js judger
assert(Math.max.apply(null, input) === max.apply(null, input), "判断错误");
```

## task5 神必数列

设某个数列的递推公式为 `f(x) = f(x-1) - f(x-2) + f(x-3) * 2` 且 `f(0) = 1`, `f(1) = 1`, `f(2) = 1`, 请编写一个名为`solution`的函数，使其能接收一个数字`x`，返回`f(x)`的值

```js init
/**
 * @param {number} x 项数
 * @return {number} f(x)的值
 */
function solution(x) {

}
```

```js input
[ 1, 3, 9, 12, 17, 23 ];
```

```js judger
function judge(x) {
    if (x <= 2) return 1;
    return judge(x-1) - judge(x-2) + judge(x-3) * 2;
}
assert(judge(input) === solution(input), "答案错误");
```
