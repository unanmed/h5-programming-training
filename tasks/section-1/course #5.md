# task1 冒泡排序

冒泡排序是一种朴素的排序方法

具体来说，冒泡排序主要依靠"冒泡"这个操作来进行排序，冒泡是指，顺序遍历待排序的数组，对于每个元素，比较它和它后一个元素的大小，若相邻的元素为逆序，则交换这两个元素，然后再检查下一个元素。举个例子，`[ 1, 5, 4, 2, 3 ]`在进行一次冒泡后会变成`[ 1, 4, 2, 3, 5 ]`

不难证明(这个词是重点，要背诵)，对于长度为`n`的数组，进行`n`次这样的操作之后，一定会变成有序数列，请编写一个函数`solution`，用以计算当给定的待排序数组被进行`x`次操作后得到的数组

本题中排序按照从小到大的顺序进行，保证传入一定是`number`数组

```js init
/**
 * @param {number[]} array 要排序的数组
 * @param {number} x 进行冒泡的次数
 * @return {number[]} 进行x次排序之后的数组
 */
function solution(array, x) {

}

console.log(solution(input[0], input[1]));
```

```js input
[
    [ [ 1, 5, 4, 2, 3 ], 1 ],
    [ [ 1, 1, 8, 9, 123, 43, 12, 5, 4, 2, 3 ], 2 ],
    [ [ 1, 1, 8, 9, 123, 43, 12, 5, 4, 2, 3 ], 4 ],
    [ [ 9, 8, 7, 6, 5, 4, 3, 2, 1 ], 0 ],
    [ [ 9, 8, 7, 6, 5, 4, 3, 2, 1 ], 6 ],
    [ [ 9, 8, 7, 6, 5, 4, 3, 2, 1 ], 18 ],
    [ [ 9, 8, 7, 6, 5, 4, 3, 2, 1 ], 38 ],
    [ [ 9, 8, 7, 6, 5, 4, 3, 2, 1 ], 105 ],
    [ [ 2, 1, 1 ], 1 ],
    [ [], 1 ],
]
```

```js judger
function equal(a, b) {
    return JSON.stringify(a) === JSON.stringify(b);
}

function judge(array, x) {
    function bubble() {
        for (let i = 0; i < array.length-1; i++) {
            if (array[i] > array[i+1]) {
                const temp = array[i];
                array[i] = array[i+1];
                array[i+1] = temp;
            }
        }
    }
    for (let i = 0; i < x; i++) bubble();
    return array;
}

const [ array, x ] = input;
assert(equal(solution(array.concat(), x), judge(array.concat(), x)));
```

# task2 作弊

我们将在下一节课之后展开阶段性的大检测（是真的），然而，神必的大脑升级人并没有认真学习，而是在设法与人py，具体来说，他总是有办法在评测之前得到正确答案，因此，他可以临场构造出可以返回正确答案的程序，，，不过，他是如此的懒惰以至于他不想自己写这个程序，因此，他希望你写一个函数`solution`，接收一个评测函数`judge`，以及他py得到的答案`answer`，然后，向`judge`内传入一个能返回正确答案的函数（听着有点套娃

```js init
/**
 * @template T
 * @param {(solution: () => T) => void} judge 评测函数
 * @param {T} answer 答案
 */
function solution(judge, answer) {

}

solution((answer) => {
    console.log(answer());
}, input)
```

```js input
[ "hello,world", 123, null, [ 5 ] ]
```

```js judger
escape = true;
solution((answer) => {
    assert(answer() === input, "回答错误");
    escape = false;
}, input);
assert(!escape, "没有做出回答")
```

# task3 函数合成

在函数式编程中，利用函数合成来复用逻辑非常流行，请你编写一个函数`solution`，其接收两个判断函数（即接收一个值，并返回一个布尔值的函数），并返回一个新的判断函数，使其为这两个函数的与函数（也就是说，只有当两个判断函数都返回true时才返回true，否则返回false

```js init
/**
 * @template T
 * @param {(value: T) => boolean} fa 判断函数a
 * @param {(value: T) => boolean} fb 判断函数b
 * 
 * @return {(value: T) => boolean}
 */
function solution(fa, fb) {

}

console.log(solution((v) => true, (v) => false)(null));
```

```js input
[ [ 0.3, 0.5 ], [ 0.8, 0.7 ], [ 0.3, 0.1 ], [ 0.1, 0.9 ], [ 0, 1 ], [ 1, 1 ], [ 0.15, 0.35] ]
```

```js judger
const fa = (v) => input[0] > v; 
const fb = (v) => input[1] < v;

const target = Math.random();
assert(solution(fa, fb)(target) === (fa(target) && fb(target)));
```

# task4 约瑟夫环

约瑟夫环是一个经典的编程问题

据说著名犹太历史学家Josephus有过以下的故事：在罗马人占领乔塔帕特后，39 个犹太人与Josephus及他的朋友躲到一个洞中，39个犹太人决定宁愿死也不要被敌人抓到，于是决定了一个自杀方式，41个人排成一个圆圈，由第1个人开始报数，每报数到第3人该人就必须自杀，然后再由下一个重新报数，直到所有人都自杀身亡为止。Josephus要他的朋友先假装遵从，他将朋友与自己安排在第16个与第31个位置，于是逃过了这场死亡游戏。

请编写一个函数`solution`，用以计算当有`n`人参加，报到`m`的人自杀的情况下，最后一个自杀的人的初始序号（这样当你参加这个游戏的时候，就总是能逃过一劫了

测试数据保证`n > 1`, `m >= 1`

```js init
/**
 * @param {number} n 总人数
 * @param {number} m 报到m的人自杀 
 * @return {number} 一个数字，代表最后一个自杀的人的初始序号
 */
function solution(n, m) {

}

console.log(solution(input[0], input[1]));
```

```js input
[ [ 41, 3 ], [ 5, 3 ], [ 12, 77 ], [ 100, 2 ], [ 19, 3 ], [ 100, 101 ], [ 3, 1 ] ]
```

```js judger
function judge(n, m) {
    const loop = new Array(n).fill(true);
    let killed = 0, nw = -1;
    function getNext() {
        nw = loop.indexOf(true, nw+1);
        if (nw === -1) nw = loop.indexOf(true);
        return nw;
    }
    while (killed < n-1) {
        for (let count = 1; count <= m ; count++) {
            getNext();
        }
        loop[nw] = false;
        killed++;
    }
    return getNext()+1;
}
const [ n, m ] = input;
assert(judge(n, m) === solution(n, m));
```

# task5 敏感词

众所周知，经常有神必人往网站上发奇怪的言论，现在希望你开发一个程序用以和谐用户的发言

具体来说，你需要编写一个名为`solution`的函数，它可以接受一个发言数组，每个数组由一个字符串数组组成，代表玩家的发言，一个敏感词列表，以及一个预定的和谐词，对于每个发言，你需要将其中所有的敏感词用和谐词来代替，特别的，如果一个发言中有5个及以上的词汇被和谐，或者全是敏感词，则将此发言从列表中删除，在处理完成后，请返回发言数组

```js init
/**
 * @template T
 * @param {string[][]} comments 发言列表
 * @param {string[]} censorlist 敏感词列表
 * @param {string} 和谐词
 * 
 * @return {(value: T) => boolean}
 */
function solution(comments, censorlist, word) {

}

console.log(solution(input[0], input[1], input[2]));
```

```js input
[
    [ 
        [
            [ "LHJNB" ], [ "太难了" ], [ "太难了", "太难了", "太难了", "太难了", "太难了", "能不能简单点" ], [ "太难了", "能不能简单点" ]
        ],
        [ "太难了" ],
        "H5NB"
    ],
    [ 
        [
            [ "H5NB", "LHJNB" ], [ "H5SB" ], [ "H5SB", "LHJNB" ], [ "H5SB" ], [ "114514", "1919810" ],
        ],
        [ "H5SB" ],
        "H5NB"
    ],
    [ 
        [
            [ "H5NB", "LHJNB" ], [ "H5SB" ], [ "H5SB", "LHJNB" ], [ "H5SB" ], [ "114514", "1919810" ], [ "H5", "H5", "H6", "H6", "H6" ], [ "H5", "H5", "H6", "H6", "H6", "H7" ], 
        ],
        [ "H5", "h6" ],
        "H5NB"
    ],
    [ 
        [
            [ "H5NB", "LHJNB" ], [ "H5SB" ], [ "H5SB", "LHJNB" ], [ "H5SB" ], [ "114514", "1919810" ], [ "H5", "H5", "H6", "H6", "H6" ], [ "H5", "H5", "H6", "H6", "H6", "H7" ], [ "H5NB" ], [ "H5NB", "H5NB", "H5NB", "H5NB", "H5NB", "H5NB", "H5NB", "H6NB" ]
        ],
        [ "H5", "h6" ],
        "H5NB"
    ],
]
```

```js judger
function equal(a, b) {
    return JSON.stringify(a) === JSON.stringify(b);
}
function copy(a) {
    return JSON.parse(JSON.stringify(a));
}

function judge(comments, censorlist, word) {
    return comments
        .map((e) => e.map(w => {
            if (censorlist.includes(w)) return null;
            return w;
        }))
        .filter((e) => {
            let count = 0;
            for (let w of e) {
                if (w === null) count++;
            }
            return count < 5 && count < e.length;
        })
        .map((e) => e.map(w => {
            if (w === null) return word;
            return w;
        }))
}

const [ comments, censorlist, word ] = input;

assert(equal(
    solution(copy(comments), copy(censorlist) , word),
    judge(copy(comments), copy(censorlist) , word),
));
```

# task6 数组运算

我们为数组定义了一系列新的运算方法

具体来说

`+` 数组串接, 将数组b加到数组a后方 `"+" [ 1 ] [ 1, 2 ] -> [ 1, 1, 2 ]`

`*` 数组乘法, 将数组a中的每个元素乘以数组b中的每个元素，变成一个二维数组 `"*" [ 1 ] [ 1, 2 ] -> [ [ 1, 2 ] ]`

`&` 数组求交，返回数组a和数组b中都出现过的元素 `"&" [ 1 ] [ 1, 2 ] -> [ 1 ]`

`|` 数组求并，返回数组a和数组b中出现过的所有元素 `"|" [ 1 ] [ 1, 2 ] -> [ 1, 2 ]`

请你编写一个函数，接收运算符和两个数组，并返回运算结果

保证数组a, b 都是 `number` 型数组

```js init
/**
 * @template T
 * @param {"+"|"*"|"&"|"|"} operator 操作符
 * @param {number[]} a 数组a
 * @param {number[]} b 数组b
 * 
 * @return {(value: T) => boolean}
 */
function solution(operator, a, b) {

}

console.log(solution(input[0], input[1], input[2]));
```

```js input
[
    [ "+", [ 1 ], [ 1, 2 ] ],
    [ "*", [ 1 ], [ 1, 2 ] ],
    [ "&", [ 1 ], [ 1, 2 ] ],
    [ "|", [ 1 ], [ 1, 2 ] ],
    [ "+", [ 1 ], [ 2 ] ],
    [ "*", [ 1 ], [ 2 ] ],
    [ "&", [ 1 ], [ 2 ] ],
    [ "|", [ 1 ], [ 2 ] ],
    [ "+", [ 1 ], [] ],
    [ "*", [ 1 ], [] ],
    [ "&", [ 1 ], [] ],
    [ "|", [ 1 ], [] ],
    [ "+", [ 1, 1, 2, 3 ], [ 2, 2, 3, 4 ] ],
    [ "*", [ 1, 1, 2, 3 ], [ 2, 2, 3, 4 ] ],
    [ "&", [ 1, 1, 2, 3 ], [ 2, 2, 3, 4 ] ],
    [ "|", [ 1, 1, 2, 3 ], [ 2, 2, 3, 4 ] ],
]
```

```js judger
function equal(a, b) {
    return JSON.stringify(a) === JSON.stringify(b);
}

function judge(operator, a, b) {
    const unique = (a) => {
        return a
            .sort((a, b) => a - b)
            .filter((e, i, arr) => {
                if (i === 0) return true;
                return arr[i] !== arr[i-1];
            });
    }
    switch(operator) {
        case "+": {
            return a.concat(b);
        }
        case "*": {
            return a.map(ae => b.map(be => ae * be));
        }
        case "&": {
            return unique(a).concat(unique(b))
                .sort((a, b) => a - b)
                .filter((e, i, arr) => {
                    if (i === 0) return false;
                    return arr[i] === arr[i-1];
                });
        }
        case "|": {
            return unique(a.concat(b));
        }
    }
}

const [ operator, a, b ] = input; 
if (["+", "*"].includes(operator)) {
    assert(
        equal(
            solution(operator, a.concat(), b.concat()),
            judge(operator, a.concat(), b.concat())
        )
    );
} else {
    assert(
        equal(
            solution(operator, a.concat(), b.concat()).sort((a, b) => a - b),
            judge(operator, a.concat(), b.concat()).sort((a, b) => a - b),
        )
    );
}
```
