[![Logo](/logo.png)](https://github.com/ConardLi/30-seconds-of-code-Zh-CN)

## 目录

* [`ary`](#ary)
* [`call`](#call)
* [`collectInto`](#collectinto)
* [`flip`](#flip)
* [`over`](#over)
* [`overArgs`](#overargs)
* [`pipeAsyncFunctions`](#pipeasyncfunctions)
* [`pipeFunctions`](#pipefunctions)
* [`promisify`](#promisify)
* [`rearg`](#rearg)
* [`spreadOver`](#spreadover)
* [`unary`](#unary)


## 🔌 Adapter

### ary

创建一个可以接收n个参数的函数, 忽略其他额外的参数。

调用提供的函数`fn`,参数最多为n个, 使用 `Array.prototype.slice(0,n)` 和展开操作符 (`...`)。

```js
const ary = (fn, n) => (...args) => fn(...args.slice(0, n));
```


示例

```js
const firstTwoMax = ary(Math.max, 2);
[[2, 6, 'a'], [8, 4, 6], [10]].map(x => firstTwoMax(...x)); // [6, 8, 10]
```





### call

给定一个key和一组参数，给定一个上下文时调用它们。主要用于合并。

使用闭包调用上下文中key对应的值，即带有存储参数的函数。

```js
const call = (key, ...args) => context => context[key](...args);
```


示例

```js
Promise.resolve([1, 2, 3])
  .then(call('map', x => 2 * x))
  .then(console.log); // [ 2, 4, 6 ]
const map = call.bind(null, 'map');
Promise.resolve([1, 2, 3])
  .then(map(x => 2 * x))
  .then(console.log); // [ 2, 4, 6 ]
```



### collectInto

将一个接收数组参数的函数改变为可变参数的函数。

给定一个函数，返回一个闭包，该闭包将所有输入收集到一个数组接受函数中。

```js
const collectInto = fn => (...args) => fn(args);
```


示例

```js
const Pall = collectInto(Promise.all.bind(Promise));
let p1 = Promise.resolve(1);
let p2 = Promise.resolve(2);
let p3 = new Promise(resolve => setTimeout(resolve, 2000, 3));
Pall(p1, p2, p3).then(console.log); // [1, 2, 3] (after about 2 seconds)
```





### flip

Flip以一个函数作为参数，然后把第一个参数作为最后一个参数。

返回一个可变参数的闭包，在应用其他参数前，先把第一个以外的其他参数作为第一个参数。


```js
const flip = fn => (first, ...rest) => fn(...rest, first);
```


示例

```js
let a = { name: 'John Smith' };
let b = {};
const mergeFrom = flip(Object.assign);
let mergePerson = mergeFrom.bind(null, a);
mergePerson(b); // == b
b = {};
Object.assign(b, a); // == b
```





### over

创建一个函数，这个函数可以调用每一个被传入的并且才有参数的函数，然后返回结果。

使用 `Array.prototype.map()` 和 `Function.prototype.apply()`将每个函数应用给定的参数。

```js
const over = (...fns) => (...args) => fns.map(fn => fn.apply(null, args));
```


示例

```js
const minMax = over(Math.min, Math.max);
minMax(1, 2, 3, 4, 5); // [1,5]
```





### overArgs

创建一个函数，它可以调用提供的被转换参数的函数。

使用`Array.prototype.map()`将`transforms`应用于`args`，并结合扩展运算符(`…`)将转换后的参数传递给`fn`。

```js
const overArgs = (fn, transforms) => (...args) => fn(...args.map((val, i) => transforms[i](val)));
```


示例

```js
const square = n => n * n;
const double = n => n * 2;
const fn = overArgs((x, y) => [x, y], [square, double]);
fn(9, 3); // [81, 6]
```





### pipeAsyncFunctions

为异步函数执行从左到右的函数组合。

在扩展操作符(`…`)中使用`Array.prototype.reduce() `来使用`Promise.then()`执行从左到右的函数组合。
这些函数可以返回简单值、`Promise`的组合，也可以定义为通过`await`返回的`async`值。
所有函数必须是一元的。
```js
const pipeAsyncFunctions = (...fns) => arg => fns.reduce((p, f) => p.then(f), Promise.resolve(arg));
```

> arr.reduce(callback[, initialValue])

```
callback
执行数组中每个值的函数，包含四个参数：
    accumulator
    累计器累计回调的返回值; 它是上一次调用回调时返回的累积值，或initialValue（见于下方）。
    currentValue
    数组中正在处理的元素。
    currentIndex可选
    数组中正在处理的当前元素的索引。 如果提供了initialValue，则起始索引号为0，否则为1。
    array可选
    调用reduce()的数组
initialValue可选
作为第一次调用 callback函数时的第一个参数的值。 如果没有提供初始值，则将使用数组中的第一个元素。 在没有初始值的空数组上调用 reduce 将报错。
```


示例

```js

const sum = pipeAsyncFunctions(
  x => x + 1,
  x => new Promise(resolve => setTimeout(() => resolve(x + 2), 1000)),
  x => x + 3,
  async x => (await x) + 4
);
(async() => {
  console.log(await sum(5)); // 15 (after one second)
})();
```


### pipeFunctions

执行从左到右的函数组合。

在展开操作符(`…`)中使用`Array.prototype.reduce()`来执行从左到右的函数组合。
第一个(最左边的)函数可以接受一个或多个参数; 其余的函数必须是一元的。

```js
const pipeFunctions = (...fns) => fns.reduce((f, g) => (...args) => g(f(...args)));
```


示例

```js
const add5 = x => x + 5;
const multiply = (x, y) => x * y;
const multiplyAndAdd5 = pipeFunctions(multiply, add5);
multiplyAndAdd5(5, 2); // 15
```


### promisify

把一个异步函数转换成返回promise的。

使用局部套用返回一个函数，该函数返回一个调用原始函数的`Promise`。
使用的`...`操作符来传入所有参数。


```js
const promisify = func => (...args) =>
  new Promise((resolve, reject) =>
    func(...args, (err, result) => (err ? reject(err) : resolve(result)))
  );
```


示例

```js
const delay = promisify((d, cb) => setTimeout(cb, d));
delay(2000).then(() => console.log('Hi!')); // Promise resolves after 2s
```





### rearg


创建一个调用提供的函数的函数，该函数的参数按照指定的索引排列。

利用 `Array.prototype.map()` 根据 `indexes` 和展开操作符 (`...`) 对参数进行重新排序，将转换后的参数传递给 `fn`.

```js
const rearg = (fn, indexes) => (...args) => fn(...indexes.map(i => args[i]));
```


示例

```js
var rearged = rearg(
  function(a, b, c) {
    return [a, b, c];
  },
  [2, 0, 1]
);
rearged('b', 'c', 'a'); // ['a', 'b', 'c']
```



### spreadOver

接受一个可变参数函数并返回一个闭包，该闭包接受一个参数数组以映射到函数的输入。

使用闭包和扩展操作符(`…`)将参数数组映射到函数的输入。

```js
const spreadOver = fn => argsArr => fn(...argsArr);
```


示例

```js
const arrayMax = spreadOver(Math.max);
arrayMax([1, 2, 3]); // 3
```

### unary

创建一个最多接受一个参数的函数，忽略任何其他参数。

只把第一个参数传递给要调用的函数`fn`。

```js
const unary = fn => val => fn(val);
```

示例

```js
['6', '8', '10'].map(unary(parseInt)); // [6, 8, 10]
```

---
