[![Logo](/logo.png)](https://github.com/ConardLi/30-seconds-of-code-Zh-CN)

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

Creates a function that accepts up to `n` arguments, ignoring any additional arguments.

Call the provided function, `fn`, with up to `n` arguments, using `Array.prototype.slice(0,n)` and the spread operator (`...`).

```js
const ary = (fn, n) => (...args) => fn(...args.slice(0, n));
```

<details>
<summary>Examples</summary>

```js
const firstTwoMax = ary(Math.max, 2);
[[2, 6, 'a'], [8, 4, 6], [10]].map(x => firstTwoMax(...x)); // [6, 8, 10]
```

</details>

<br>[⬆ Back to top](#contents)

### call

Given a key and a set of arguments, call them when given a context. Primarily useful in composition.

Use a closure to call a stored key with stored arguments.

```js
const call = (key, ...args) => context => context[key](...args);
```

<details>
<summary>Examples</summary>

```js
Promise.resolve([1, 2, 3])
  .then(call('map', x => 2 * x))
  .then(console.log); // [ 2, 4, 6 ]
const map = call.bind(null, 'map');
Promise.resolve([1, 2, 3])
  .then(map(x => 2 * x))
  .then(console.log); // [ 2, 4, 6 ]
```

</details>

<br>[⬆ Back to top](#contents)

### collectInto

Changes a function that accepts an array into a variadic function.

Given a function, return a closure that collects all inputs into an array-accepting function.

```js
const collectInto = fn => (...args) => fn(args);
```

<details>
<summary>Examples</summary>

```js
const Pall = collectInto(Promise.all.bind(Promise));
let p1 = Promise.resolve(1);
let p2 = Promise.resolve(2);
let p3 = new Promise(resolve => setTimeout(resolve, 2000, 3));
Pall(p1, p2, p3).then(console.log); // [1, 2, 3] (after about 2 seconds)
```

</details>

<br>[⬆ Back to top](#contents)

### flip

Flip takes a function as an argument, then makes the first argument the last.

Return a closure that takes variadic inputs, and splices the last argument to make it the first argument before applying the rest.

```js
const flip = fn => (first, ...rest) => fn(...rest, first);
```

<details>
<summary>Examples</summary>

```js
let a = { name: 'John Smith' };
let b = {};
const mergeFrom = flip(Object.assign);
let mergePerson = mergeFrom.bind(null, a);
mergePerson(b); // == b
b = {};
Object.assign(b, a); // == b
```

</details>

<br>[⬆ Back to top](#contents)

### over

Creates a function that invokes each provided function with the arguments it receives and returns the results.

Use `Array.prototype.map()` and `Function.prototype.apply()` to apply each function to the given arguments.

```js
const over = (...fns) => (...args) => fns.map(fn => fn.apply(null, args));
```

<details>
<summary>Examples</summary>

```js
const minMax = over(Math.min, Math.max);
minMax(1, 2, 3, 4, 5); // [1,5]
```

</details>

<br>[⬆ Back to top](#contents)

### overArgs

Creates a function that invokes the provided function with its arguments transformed.

Use `Array.prototype.map()` to apply `transforms` to `args` in combination with the spread operator (`...`) to pass the transformed arguments to `fn`.

```js
const overArgs = (fn, transforms) => (...args) => fn(...args.map((val, i) => transforms[i](val)));
```

<details>
<summary>Examples</summary>

```js
const square = n => n * n;
const double = n => n * 2;
const fn = overArgs((x, y) => [x, y], [square, double]);
fn(9, 3); // [81, 6]
```

</details>

<br>[⬆ Back to top](#contents)

### pipeAsyncFunctions

Performs left-to-right function composition for asynchronous functions.

Use `Array.prototype.reduce()` with the spread operator (`...`) to perform left-to-right function composition using `Promise.then()`.
The functions can return a combination of: simple values, `Promise`'s, or they can be defined as `async` ones returning through `await`.
All functions must be unary.

```js
const pipeAsyncFunctions = (...fns) => arg => fns.reduce((p, f) => p.then(f), Promise.resolve(arg));
```

<details>
<summary>Examples</summary>

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

</details>

<br>[⬆ Back to top](#contents)

### pipeFunctions

Performs left-to-right function composition.

Use `Array.prototype.reduce()` with the spread operator (`...`) to perform left-to-right function composition.
The first (leftmost) function can accept one or more arguments; the remaining functions must be unary.

```js
const pipeFunctions = (...fns) => fns.reduce((f, g) => (...args) => g(f(...args)));
```

<details>
<summary>Examples</summary>

```js
const add5 = x => x + 5;
const multiply = (x, y) => x * y;
const multiplyAndAdd5 = pipeFunctions(multiply, add5);
multiplyAndAdd5(5, 2); // 15
```

</details>

<br>[⬆ Back to top](#contents)

### promisify

Converts an asynchronous function to return a promise.

Use currying to return a function returning a `Promise` that calls the original function.
Use the `...rest` operator to pass in all the parameters.

*In Node 8+, you can use [`util.promisify`](https://nodejs.org/api/util.html#util_util_promisify_original)*

```js
const promisify = func => (...args) =>
  new Promise((resolve, reject) =>
    func(...args, (err, result) => (err ? reject(err) : resolve(result)))
  );
```

<details>
<summary>Examples</summary>

```js
const delay = promisify((d, cb) => setTimeout(cb, d));
delay(2000).then(() => console.log('Hi!')); // // Promise resolves after 2s
```

</details>

<br>[⬆ Back to top](#contents)

### rearg

Creates a function that invokes the provided function with its arguments arranged according to the specified indexes.

Use `Array.prototype.map()` to reorder arguments based on `indexes` in combination with the spread operator (`...`) to pass the transformed arguments to `fn`.

```js
const rearg = (fn, indexes) => (...args) => fn(...indexes.map(i => args[i]));
```

<details>
<summary>Examples</summary>

```js
var rearged = rearg(
  function(a, b, c) {
    return [a, b, c];
  },
  [2, 0, 1]
);
rearged('b', 'c', 'a'); // ['a', 'b', 'c']
```

</details>

<br>[⬆ Back to top](#contents)

### spreadOver

Takes a variadic function and returns a closure that accepts an array of arguments to map to the inputs of the function.

Use closures and the spread operator (`...`) to map the array of arguments to the inputs of the function.

```js
const spreadOver = fn => argsArr => fn(...argsArr);
```

<details>
<summary>Examples</summary>

```js
const arrayMax = spreadOver(Math.max);
arrayMax([1, 2, 3]); // 3
```

</details>

<br>[⬆ Back to top](#contents)

### unary

Creates a function that accepts up to one argument, ignoring any additional arguments.

Call the provided function, `fn`, with just the first argument given.

```js
const unary = fn => val => fn(val);
```

<details>
<summary>Examples</summary>

```js
['6', '8', '10'].map(unary(parseInt)); // [6, 8, 10]
```

</details>

<br>[⬆ Back to top](#contents)


---
