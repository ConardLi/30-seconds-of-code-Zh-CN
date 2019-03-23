[![Logo](/logo.png)](https://github.com/ConardLi/30-seconds-of-code-Zh-CN)

## 目录


* [`all`](#all)
* [`allEqual`](#allequal)
* [`any`](#any)
* [`arrayToCSV`](#arraytocsv)
* [`bifurcate`](#bifurcate)
* [`bifurcateBy`](#bifurcateby)
* [`chunk`](#chunk)
* [`compact`](#compact)
* [`countBy`](#countby)
* [`countOccurrences`](#countoccurrences)
* [`deepFlatten`](#deepflatten)
* [`difference`](#difference)
* [`differenceBy`](#differenceby)
* [`differenceWith`](#differencewith)
* [`drop`](#drop)
* [`dropRight`](#dropright)
* [`dropRightWhile`](#droprightwhile)
* [`dropWhile`](#dropwhile)
* [`everyNth`](#everynth)
* [`filterFalsy`](#filterfalsy)
* [`filterNonUnique`](#filternonunique)
* [`filterNonUniqueBy`](#filternonuniqueby)
* [`findLast`](#findlast)
* [`findLastIndex`](#findlastindex)
* [`flatten`](#flatten)
* [`forEachRight`](#foreachright)
* [`groupBy`](#groupby)
* [`head`](#head)
* [`indexOfAll`](#indexofall)
* [`initial`](#initial)
* [`initialize2DArray`](#initialize2darray)
* [`initializeArrayWithRange`](#initializearraywithrange)
* [`initializeArrayWithRangeRight`](#initializearraywithrangeright)
* [`initializeArrayWithValues`](#initializearraywithvalues)
* [`initializeNDArray`](#initializendarray)
* [`intersection`](#intersection)
* [`intersectionBy`](#intersectionby)
* [`intersectionWith`](#intersectionwith)
* [`isSorted`](#issorted)
* [`join`](#join)
* [`JSONtoCSV`](#jsontocsv-)
* [`last`](#last)
* [`longestItem`](#longestitem)
* [`mapObject`](#mapobject-)
* [`maxN`](#maxn)
* [`minN`](#minn)
* [`none`](#none)
* [`nthElement`](#nthelement)
* [`offset`](#offset)
* [`partition`](#partition)
* [`permutations`](#permutations-)
* [`pull`](#pull)
* [`pullAtIndex`](#pullatindex-)
* [`pullAtValue`](#pullatvalue-)
* [`pullBy`](#pullby-)
* [`reducedFilter`](#reducedfilter)
* [`reduceSuccessive`](#reducesuccessive)
* [`reduceWhich`](#reducewhich)
* [`reject`](#reject)
* [`remove`](#remove)
* [`sample`](#sample)
* [`sampleSize`](#samplesize)
* [`shank`](#shank)
* [`shuffle`](#shuffle)
* [`similarity`](#similarity)
* [`sortedIndex`](#sortedindex)
* [`sortedIndexBy`](#sortedindexby)
* [`sortedLastIndex`](#sortedlastindex)
* [`sortedLastIndexBy`](#sortedlastindexby)
* [`stableSort`](#stablesort-)
* [`symmetricDifference`](#symmetricdifference)
* [`symmetricDifferenceBy`](#symmetricdifferenceby)
* [`symmetricDifferenceWith`](#symmetricdifferencewith)
* [`tail`](#tail)
* [`take`](#take)
* [`takeRight`](#takeright)
* [`takeRightWhile`](#takerightwhile)
* [`takeWhile`](#takewhile)
* [`toHash`](#tohash)
* [`union`](#union)
* [`unionBy`](#unionby)
* [`unionWith`](#unionwith)
* [`uniqueElements`](#uniqueelements)
* [`uniqueElementsBy`](#uniqueelementsby)
* [`uniqueElementsByRight`](#uniqueelementsbyright)
* [`uniqueSymmetricDifference`](#uniquesymmetricdifference)
* [`unzip`](#unzip)
* [`unzipWith`](#unzipwith-)
* [`without`](#without)
* [`xProd`](#xprod)
* [`zip`](#zip)
* [`zipObject`](#zipobject)
* [`zipWith`](#zipwith-)



## 📚 Array

### all

如果被提供的断言函数接收数组中每个元素作为参数都返回`true`，则返回`true`，否则返回`false`。


使用 `Array.prototype.every()`来测试是否第二个参数`fn`以集合中每个元素作为参数都返回`true`，使用`Boolean`作为默认值。

```js
const all = (arr, fn = Boolean) => arr.every(fn);
```

示例

```js
all([4, 2, 3], x => x > 1); // true
all([1, 2, 3]); // true
```


### allEqual

检查是否数组中所有的元素都是相等的。

使用 `Array.prototype.every()` 来检测是否数组中的所有元素都和第一个元素相等。

```js
const allEqual = arr => arr.every(val => val === arr[0]);
```


示例

```js
allEqual([1, 2, 3, 4, 5, 6]); // false
allEqual([1, 1, 1, 1]); // true
```


### any

如果被提供的断言函数接收数组中任意一个元素作为参数都返回`true`，则返回`true`，否则返回`false`。

使用 `Array.prototype.every()`来测试是否第二个参数`fn`以集合中任意一个元素作为参数都返回`true`，使用`Boolean`作为默认值。


```js
const any = (arr, fn = Boolean) => arr.some(fn);
```


示例

```js
any([0, 1, 2, 0], x => x >= 2); // true
any([0, 0, 1, 0]); // true
```


### arrayToCSV

将2D数组转换为逗号分隔值(CSV)字符串。

使用 `Array.prototype.map()` 和 `Array.prototype.join(delimiter)` 将一个一维数组转换为字符串。

使用 `Array.prototype.join('\n')` 将所有行合并成CSV字符串, 用换行符分割每一行。

如果没有第二哥参数, `delimiter`会使用一个默认分隔符 `,`.

```js
const arrayToCSV = (arr, delimiter = ',') =>
  arr.map(v => v.map(x => `"${x}"`).join(delimiter)).join('\n');
```


示例

```js
arrayToCSV([['a', 'b'], ['c', 'd']]); // '"a","b"\n"c","d"'
arrayToCSV([['a', 'b'], ['c', 'd']], ';'); // '"a";"b"\n"c";"d"'
```


### bifurcate

将数据分为两组，如果元素在 `filter`数组中对应的是`true`，集合中相应的元素应加入第一个数组，否则加入第二个数组。

基于`filter`使用`Array.prototype.reduce()` 和 `Array.prototype.push()`将元素分组。

```js
const bifurcate = (arr, filter) =>
  arr.reduce((acc, val, i) => (acc[filter[i] ? 0 : 1].push(val), acc), [[], []]);
```


示例

```js
bifurcate(['beep', 'boop', 'foo', 'bar'], [true, true, false, true]); // [ ['beep', 'boop', 'bar'], ['foo'] ]
```

### bifurcateBy

根据断言函数将数据分成两组，断言函数将指定集合中的元素属于哪个组。如果断言函数返回`true`，元素加入第一个数组，否则加入第二个数组。

给予`fn`接收元素的返回值，使用`Array.prototype.reduce()` 和 `Array.prototype.push()`将元素分组。
```js
const bifurcateBy = (arr, fn) =>
  arr.reduce((acc, val, i) => (acc[fn(val, i) ? 0 : 1].push(val), acc), [[], []]);
```


示例

```js
bifurcateBy(['beep', 'boop', 'foo', 'bar'], x => x[0] === 'b'); // [ ['beep', 'boop', 'bar'], ['foo'] ]
```


### chunk

将数组分成指定大小的较小数组。

使用 `Array.from()`创建一个新的数组，该数组与将要生成的块的数量相匹配。
使用 `Array.prototype.slice()` 将新数组的每个元素映射到长度为`size`的块。
如果原始的数组不能被均匀的分割，最后的一块将包含剩余的元素。

```js
const chunk = (arr, size) =>
  Array.from({ length: Math.ceil(arr.length / size) }, (v, i) =>
    arr.slice(i * size, i * size + size)
  );
```


示例

```js
chunk([1, 2, 3, 4, 5], 2); // [[1,2],[3,4],[5]]
```


### compact

删除数组中错误的元素

使用 `Array.prototype.filter()` 过滤掉错误的元素 (`false`, `null`, `0`, `""`, `undefined`,  `NaN`).

```js
const compact = arr => arr.filter(Boolean);
```

示例

```js
compact([0, 1, false, 2, '', 3, 'a', 'e' * 23, NaN, 's', 34]); // [ 1, 2, 3, 'a', 's', 34 ]
```

### countBy

基于给定的函数将数组中的元素进行分组，并返回每个组中的元素数。

使用`Array.prototype.map()`来将数组中的每个元素映射到函数或属性名。
使用 `Array.prototype.reduce()` 创建一个对象，其中的键是从映射结果生成的。

```js
const countBy = (arr, fn) =>
  arr.map(typeof fn === 'function' ? fn : val => val[fn]).reduce((acc, val) => {
    acc[val] = (acc[val] || 0) + 1;
    return acc;
  }, {});
```


示例

```js
countBy([6.1, 4.2, 6.3], Math.floor); // {4: 1, 6: 2}
countBy(['one', 'two', 'three'], 'length'); // {3: 2, 5: 1}
```


### countOccurrences

计算数组中某个元素出现的次数。

Use `Array.prototype.reduce()`在每次遇到数组中的特定值时递增计数器。

```js
const countOccurrences = (arr, val) => arr.reduce((a, v) => (v === val ? a + 1 : a), 0);
```

示例

```js
countOccurrences([1, 1, 2, 1, 2, 3], 1); // 3
```


### deepFlatten

将一个多层嵌套的数组转转换成一个一元数组。

使用递归.
Use `Array.prototype.concat()` with an empty array (`[]`) and the spread operator (`...`) to flatten an array.
使用 `Array.prototype.concat()` 和一个空数组(`[]`)以及展开运算符(`...`)来平铺一个数组。
当每个元素还是一个数字时，递归铺平他。

```js
const deepFlatten = arr => [].concat(...arr.map(v => (Array.isArray(v) ? deepFlatten(v) : v)));
```


示例

```js
deepFlatten([1, [2], [[3], 4], 5]); // [1,2,3,4,5]
```

### difference

返回两个数组间的差异值。

从数组`b`中创建一个 `Set` ，然后用使用另一个数组`a`的`Array.prototype.filter()` 方法过滤掉`b`中的元素。

```js
const difference = (a, b) => {
  const s = new Set(b);
  return a.filter(x => !s.has(x));
};
```

示例

```js
difference([1, 2, 3], [1, 2, 4]); // [3]
```


### differenceBy

将提供的函数应用于两个数组的每个数组元素后，返回两个数组中不同的元素。

通过`b`中的每个元素调用 `fn`后创建一个 `Set` ，然后将`Array.prototype.filter()` 与`fn`调用后的`a`结合使用，只保留先前创建的集合中不包含的值。

```js
const differenceBy = (a, b, fn) => {
  const s = new Set(b.map(fn));
  return a.filter(x => !s.has(fn(x)));
};
```

示例

```js
differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor); // [1.2]
differenceBy([{ x: 2 }, { x: 1 }], [{ x: 1 }], v => v.x); // [ { x: 2 } ]
```


### differenceWith


筛选出比较器函数不返回`true`的数组中的所有值。

使用 `Array.prototype.filter()` 和 `Array.prototype.findIndex()` 查找合适的值。

```js
const differenceWith = (arr, val, comp) => arr.filter(a => val.findIndex(b => comp(a, b)) === -1);
```


示例

```js
differenceWith([1, 1.2, 1.5, 3, 0], [1.9, 3, 0], (a, b) => Math.round(a) === Math.round(b)); // [1, 1.2]
```

### drop

返回一个新数组，从原数组左边删除`n`个元素。

使用 `Array.prototype.slice()` 从左侧删除指定数量的元素。

```js
const drop = (arr, n = 1) => arr.slice(n);
```

> slice(n) 表示取数组下标n以后的元素（含n）

示例

```js
drop([1, 2, 3]); // [2,3]
drop([1, 2, 3], 2); // [3]
drop([1, 2, 3], 42); // []
```


### dropRight

返回一个新数组，从原数组右边删除`n`个元素。

使用 `Array.prototype.slice()`从右边删除指定数目的元素。

```js
const dropRight = (arr, n = 1) => arr.slice(0, -n);
```

> slice(0, -n) 表示取数组第一个到倒数第n个元素（不含-n）


示例

```js
dropRight([1, 2, 3]); // [1,2]
dropRight([1, 2, 3], 2); // [1]
dropRight([1, 2, 3], 42); // []
```


### dropRightWhile

从数组尾部移除数组中的元素，直到传递的函数返回`true`。返回数组中剩余的元素。

遍历数组，使用`Array.prototype.slice()`删除数组的最后一个元素，直到函数的返回值为`true`。返回剩余的元素。

```js
const dropRightWhile = (arr, func) => {
  while (arr.length > 0 && !func(arr[arr.length - 1])) arr = arr.slice(0, -1);
  return arr;
};
```

示例

```js
dropRightWhile([1, 2, 3, 4], n => n < 3); // [1, 2]
```

### dropWhile

移除数组中的元素，直到传递的函数返回`true`。返回数组中剩余的元素。

遍历数组，使用`Array.prototype.slice()`删除数组的第一个元素，直到函数的返回值为`true`。返回剩余的元素。

```js
const dropWhile = (arr, func) => {
  while (arr.length > 0 && !func(arr[0])) arr = arr.slice(1);
  return arr;
};
```


示例

```js
dropWhile([1, 2, 3, 4], n => n >= 3); // [3,4]
```

### everyNth

返回数组中所有下标是n的倍数的元素。

使用 `Array.prototype.filter()` 创建包含给定数组中所有下标是n的倍数的元素的新数组。

```js
const everyNth = (arr, nth) => arr.filter((e, i) => i % nth === nth - 1);
```


示例

```js
everyNth([1, 2, 3, 4, 5, 6], 2); // [ 2, 4, 6 ]
```


### filterFalsy

把数组中的`虚值`过滤掉。

使用 `Array.prototype.filter()`创建一个只包含`真值`的新数组。 


```js
const filterFalsy = arr => arr.filter(Boolean);
```

> `falsy`(虚值)是在` Boolean `上下文中已认定可转换为‘假‘的值。例如：false，0，""，null，undefined 和 NaN 。

> `Truthy` (真值)指的是在 布尔值 上下文中转换后的值为真的值。所有值都是真值，除非它们被定义为 `falsy`。

示例

```js
filterFalsy(['', true, {}, false, 'sample', 1, 0]); // [true, {}, 'sample', 1]
```



### filterNonUnique

过滤调数组中重复的值。

使用 `Array.prototype.filter()`创建一个只包含唯一值的数组。

```js
const filterNonUnique = arr => arr.filter(i => arr.indexOf(i) === arr.lastIndexOf(i));
```

> filter() 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。 

> filter 不会改变原数组，它返回过滤后的新数组。

示例

```js
filterNonUnique([1, 2, 2, 3, 4, 4, 5]); // [1, 3, 5]
```


### filterNonUniqueBy

基于给定的比较器函数，过滤掉数组中重复的元素。

使用`Array.prototype.filter()` 和 `Array.prototype.every()` 创建一个新数组，该数组只包含唯一值，基于给定的比较器函数 `fn`。

比较器函数接收四个参数：正在被比较的两个元素和他们的索引。

```js
const filterNonUniqueBy = (arr, fn) =>
  arr.filter((v, i) => arr.every((x, j) => (i === j) === fn(v, x, i, j)));
```


示例

```js
filterNonUniqueBy(
  [
    { id: 0, value: 'a' },
    { id: 1, value: 'b' },
    { id: 2, value: 'c' },
    { id: 1, value: 'd' },
    { id: 0, value: 'e' }
  ],
  (a, b) => a.id == b.id
); // [ { id: 2, value: 'c' } ]
```


### findLast

返回所提供函数返回`真值`的最后一个元素。

使用 `Array.prototype.filter()` 将调用`fn`后返回`虚值`的元素过滤掉, 然后调用`Array.prototype.pop()` 来获取最后一个元素。

```js
const findLast = (arr, fn) => arr.filter(fn).pop();
```


示例

```js
findLast([1, 2, 3, 4], n => n % 2 === 1); // 3
```



### findLastIndex

返回所提供函数返回`真值`的最后一个元素的索引。

使用 `Array.prototype.map()` 将每个元素映射到具有其索引和值的数组。
使用 `Array.prototype.filter()` 将调用`fn`后返回`虚值`的元素过滤掉, 然后调用`Array.prototype.pop()` 来获取最后一个元素的索引。

```js
const findLastIndex = (arr, fn) =>
  arr
    .map((val, i) => [i, val])
    .filter(([i, val]) => fn(val, i, arr))
    .pop()[0];
```


示例

```js
findLastIndex([1, 2, 3, 4], n => n % 2 === 1); // 2 (index of the value 3)
```


### flatten

根据指定的深度展平一个数组。

使用递归，每层递归 `depth` 递减1。
使用 `Array.prototype.reduce()` 和 `Array.prototype.concat()` 来合并数组或者元素。
基本情况下，当`depth` 等于1时停止递归。
忽略第二个参数的情况下， `depth` 默认为1（单层展开）。

```js
const flatten = (arr, depth = 1) =>
  arr.reduce((a, v) => a.concat(depth > 1 && Array.isArray(v) ? flatten(v, depth - 1) : v), []);
```


示例

```js
flatten([1, [2], 3, 4]); // [1, 2, 3, 4]
flatten([1, [2, [3, [4, 5], 6], 7], 8], 2); // [1, 2, 3, [4, 5], 6, 7, 8]
```


### forEachRight

对数组中的每个元素执行一次所提供的函数，从数组的最后一个元素开始。


使用 `Array.prototype.slice(0)` 克隆给定的数组，并使用`Array.prototype.reverse()` 将它反转，然后使用`Array.prototype.forEach()`遍历反转后的数组。

```js
const forEachRight = (arr, callback) =>
  arr
    .slice(0)
    .reverse()
    .forEach(callback);
```

示例

```js
forEachRight([1, 2, 3, 4], val => console.log(val)); // '4', '3', '2', '1'
```


### groupBy

基于给定的函数将数组分组。

使用 `Array.prototype.map()` 将组数中的值映射到一个函数或者属性名。

使用 `Array.prototype.reduce()` 创建一个对象，其中的键由映射的结果生成。

```js
const groupBy = (arr, fn) =>
  arr.map(typeof fn === 'function' ? fn : val => val[fn]).reduce((acc, val, i) => {
    acc[val] = (acc[val] || []).concat(arr[i]);
    return acc;
  }, {});
```


示例

```js
groupBy([6.1, 4.2, 6.3], Math.floor); // {4: [4.2], 6: [6.1, 6.3]}
groupBy(['one', 'two', 'three'], 'length'); // {3: ['one', 'two'], 5: ['three']}
```


### head

Returns the head of a list.

Use `arr[0]` to return the first element of the passed array.

```js
const head = arr => arr[0];
```


示例

```js
head([1, 2, 3]); // 1
```





### indexOfAll

Returns all indices of `val` in an array.
If `val` never occurs, returns `[]`.

Use `Array.prototype.reduce()` to loop over elements and store indices for matching elements.
Return the array of indices.

```js
const indexOfAll = (arr, val) => arr.reduce((acc, el, i) => (el === val ? [...acc, i] : acc), []);
```


示例

```js
indexOfAll([1, 2, 3, 1, 2, 3], 1); // [0,3]
indexOfAll([1, 2, 3], 4); // []
```





### initial

Returns all the elements of an array except the last one.

Use `arr.slice(0,-1)` to return all but the last element of the array.

```js
const initial = arr => arr.slice(0, -1);
```


示例

```js
initial([1, 2, 3]); // [1,2]
```





### initialize2DArray

Initializes a 2D array of given width and height and value.

Use `Array.prototype.map()` to generate h rows where each is a new array of size w initialize with value. If the value is not provided, default to `null`.

```js
const initialize2DArray = (w, h, val = null) =>
  Array.from({ length: h }).map(() => Array.from({ length: w }).fill(val));
```


示例

```js
initialize2DArray(2, 2, 0); // [[0,0], [0,0]]
```





### initializeArrayWithRange

Initializes an array containing the numbers in the specified range where `start` and `end` are inclusive with their common difference `step`.

Use `Array.from()` to create an array of the desired length, `(end - start + 1)/step`, and a map function to fill it with the desired values in the given range.
You can omit `start` to use a default value of `0`.
You can omit `step` to use a default value of `1`.

```js
const initializeArrayWithRange = (end, start = 0, step = 1) =>
  Array.from({ length: Math.ceil((end - start + 1) / step) }, (v, i) => i * step + start);
```


示例

```js
initializeArrayWithRange(5); // [0,1,2,3,4,5]
initializeArrayWithRange(7, 3); // [3,4,5,6,7]
initializeArrayWithRange(9, 0, 2); // [0,2,4,6,8]
```





### initializeArrayWithRangeRight

Initializes an array containing the numbers in the specified range (in reverse) where `start` and `end` are inclusive with their common difference `step`.

Use `Array.from(Math.ceil((end+1-start)/step))` to create an array of the desired length(the amounts of elements is equal to `(end-start)/step` or `(end+1-start)/step` for inclusive end), `Array.prototype.map()` to fill with the desired values in a range.
You can omit `start` to use a default value of `0`.
You can omit `step` to use a default value of `1`.

```js
const initializeArrayWithRangeRight = (end, start = 0, step = 1) =>
  Array.from({ length: Math.ceil((end + 1 - start) / step) }).map(
    (v, i, arr) => (arr.length - i - 1) * step + start
  );
```


示例

```js
initializeArrayWithRangeRight(5); // [5,4,3,2,1,0]
initializeArrayWithRangeRight(7, 3); // [7,6,5,4,3]
initializeArrayWithRangeRight(9, 0, 2); // [8,6,4,2,0]
```





### initializeArrayWithValues

Initializes and fills an array with the specified values.

Use `Array(n)` to create an array of the desired length, `fill(v)` to fill it with the desired values.
You can omit `val` to use a default value of `0`.

```js
const initializeArrayWithValues = (n, val = 0) => Array(n).fill(val);
```


示例

```js
initializeArrayWithValues(5, 2); // [2, 2, 2, 2, 2]
```





### initializeNDArray

Create a n-dimensional array with given value.

Use recursion.
Use `Array.prototype.map()` to generate rows where each is a new array initialized using `initializeNDArray`.

```js
const initializeNDArray = (val, ...args) =>
  args.length === 0
    ? val
    : Array.from({ length: args[0] }).map(() => initializeNDArray(val, ...args.slice(1)));
```


示例

```js
initializeNDArray(1, 3); // [1,1,1]
initializeNDArray(5, 2, 2, 2); // [[[5,5],[5,5]],[[5,5],[5,5]]]
```





### intersection

Returns a list of elements that exist in both arrays.

Create a `Set` from `b`, then use `Array.prototype.filter()` on `a` to only keep values contained in `b`.

```js
const intersection = (a, b) => {
  const s = new Set(b);
  return a.filter(x => s.has(x));
};
```


示例

```js
intersection([1, 2, 3], [4, 3, 2]); // [2, 3]
```





### intersectionBy

Returns a list of elements that exist in both arrays, after applying the provided function to each array element of both.

Create a `Set` by applying `fn` to all elements in `b`, then use `Array.prototype.filter()` on `a` to only keep elements, which produce values contained in `b` when `fn` is applied to them.

```js
const intersectionBy = (a, b, fn) => {
  const s = new Set(b.map(fn));
  return a.filter(x => s.has(fn(x)));
};
```


示例

```js
intersectionBy([2.1, 1.2], [2.3, 3.4], Math.floor); // [2.1]
```





### intersectionWith

Returns a list of elements that exist in both arrays, using a provided comparator function.

Use `Array.prototype.filter()` and `Array.prototype.findIndex()` in combination with the provided comparator to determine intersecting values.

```js
const intersectionWith = (a, b, comp) => a.filter(x => b.findIndex(y => comp(x, y)) !== -1);
```


示例

```js
intersectionWith([1, 1.2, 1.5, 3, 0], [1.9, 3, 0, 3.9], (a, b) => Math.round(a) === Math.round(b)); // [1.5, 3, 0]
```





### isSorted

Returns `1` if the array is sorted in ascending order, `-1` if it is sorted in descending order or `0` if it is not sorted.

Calculate the ordering `direction` for the first two elements.
Use `Object.entries()` to loop over array objects and compare them in pairs.
Return `0` if the `direction` changes or the `direction` if the last element is reached.

```js
const isSorted = arr => {
  let direction = -(arr[0] - arr[1]);
  for (let [i, val] of arr.entries()) {
    direction = !direction ? -(arr[i - 1] - arr[i]) : direction;
    if (i === arr.length - 1) return !direction ? 0 : direction;
    else if ((val - arr[i + 1]) * direction > 0) return 0;
  }
};
```


示例

```js
isSorted([0, 1, 2, 2]); // 1
isSorted([4, 3, 2]); // -1
isSorted([4, 3, 5]); // 0
```





### join

Joins all elements of an array into a string and returns this string.
Uses a separator and an end separator.

Use `Array.prototype.reduce()` to combine elements into a string.
Omit the second argument, `separator`, to use a default separator of `','`.
Omit the third argument, `end`, to use the same value as `separator` by default.

```js
const join = (arr, separator = ',', end = separator) =>
  arr.reduce(
    (acc, val, i) =>
      i === arr.length - 2
        ? acc + val + end
        : i === arr.length - 1
          ? acc + val
          : acc + val + separator,
    ''
  );
```


示例

```js
join(['pen', 'pineapple', 'apple', 'pen'], ',', '&'); // "pen,pineapple,apple&pen"
join(['pen', 'pineapple', 'apple', 'pen'], ','); // "pen,pineapple,apple,pen"
join(['pen', 'pineapple', 'apple', 'pen']); // "pen,pineapple,apple,pen"
```





### JSONtoCSV ![advanced](/advanced.svg)

Converts an array of objects to a comma-separated values (CSV) string that contains only the `columns` specified.

Use `Array.prototype.join(delimiter)` to combine all the names in `columns` to create the first row.
Use `Array.prototype.map()` and `Array.prototype.reduce()` to create a row for each object, substituting non-existent values with empty strings and only mapping values in `columns`.
Use `Array.prototype.join('\n')` to combine all rows into a string.
Omit the third argument, `delimiter`, to use a default delimiter of `,`.

```js
const JSONtoCSV = (arr, columns, delimiter = ',') =>
  [
    columns.join(delimiter),
    ...arr.map(obj =>
      columns.reduce(
        (acc, key) => `${acc}${!acc.length ? '' : delimiter}"${!obj[key] ? '' : obj[key]}"`,
        ''
      )
    )
  ].join('\n');
```


示例

```js
JSONtoCSV([{ a: 1, b: 2 }, { a: 3, b: 4, c: 5 }, { a: 6 }, { b: 7 }], ['a', 'b']); // 'a,b\n"1","2"\n"3","4"\n"6",""\n"","7"'
JSONtoCSV([{ a: 1, b: 2 }, { a: 3, b: 4, c: 5 }, { a: 6 }, { b: 7 }], ['a', 'b'], ';'); // 'a;b\n"1";"2"\n"3";"4"\n"6";""\n"";"7"'
```





### last

Returns the last element in an array.

Use `arr.length - 1` to compute the index of the last element of the given array and returning it.

```js
const last = arr => arr[arr.length - 1];
```


示例

```js
last([1, 2, 3]); // 3
```





### longestItem

Takes any number of iterable objects or objects with a `length` property and returns the longest one.
If multiple objects have the same length, the first one will be returned.
Returns `undefined` if no arguments are provided.

Use `Array.prototype.reduce()`, comparing the `length` of objects to find the longest one.

```js
const longestItem = (...vals) => vals.reduce((a, x) => (x.length > a.length ? x : a));
```


示例

```js
longestItem('this', 'is', 'a', 'testcase'); // 'testcase'
longestItem(...['a', 'ab', 'abc']); // 'abc'
longestItem(...['a', 'ab', 'abc'], 'abcd'); // 'abcd'
longestItem([1, 2, 3], [1, 2], [1, 2, 3, 4, 5]); // [1, 2, 3, 4, 5]
longestItem([1, 2, 3], 'foobar'); // 'foobar'
```





### mapObject ![advanced](/advanced.svg)

Maps the values of an array to an object using a function, where the key-value pairs consist of the original value as the key and the mapped value.

Use an anonymous inner function scope to declare an undefined memory space, using closures to store a return value. Use a new `Array` to store the array with a map of the function over its data set and a comma operator to return a second step, without needing to move from one context to another (due to closures and order of operations).

```js
const mapObject = (arr, fn) =>
  (a => (
    (a = [arr, arr.map(fn)]), a[0].reduce((acc, val, ind) => ((acc[val] = a[1][ind]), acc), {})
  ))();
```


示例

```js
const squareIt = arr => mapObject(arr, a => a * a);
squareIt([1, 2, 3]); // { 1: 1, 2: 4, 3: 9 }
```





### maxN

Returns the `n` maximum elements from the provided array.
If `n` is greater than or equal to the provided array's length, then return the original array (sorted in descending order).

Use `Array.prototype.sort()` combined with the spread operator (`...`) to create a shallow clone of the array and sort it in descending order.
Use `Array.prototype.slice()` to get the specified number of elements.
Omit the second argument, `n`, to get a one-element array.

```js
const maxN = (arr, n = 1) => [...arr].sort((a, b) => b - a).slice(0, n);
```


示例

```js
maxN([1, 2, 3]); // [3]
maxN([1, 2, 3], 2); // [3,2]
```





### minN

Returns the `n` minimum elements from the provided array.
If `n` is greater than or equal to the provided array's length, then return the original array (sorted in ascending order).

Use `Array.prototype.sort()` combined with the spread operator (`...`) to create a shallow clone of the array and sort it in ascending order.
Use `Array.prototype.slice()` to get the specified number of elements.
Omit the second argument, `n`, to get a one-element array.

```js
const minN = (arr, n = 1) => [...arr].sort((a, b) => a - b).slice(0, n);
```


示例

```js
minN([1, 2, 3]); // [1]
minN([1, 2, 3], 2); // [1,2]
```





### none

Returns `true` if the provided predicate function returns `false` for all elements in a collection, `false` otherwise.

Use `Array.prototype.some()` to test if any elements in the collection return `true` based on `fn`.
Omit the second argument, `fn`, to use `Boolean` as a default.

```js
const none = (arr, fn = Boolean) => !arr.some(fn);
```


示例

```js
none([0, 1, 3, 0], x => x == 2); // true
none([0, 0, 0]); // true
```





### nthElement

Returns the nth element of an array.

Use `Array.prototype.slice()` to get an array containing the nth element at the first place.
If the index is out of bounds, return `undefined`.
Omit the second argument, `n`, to get the first element of the array.

```js
const nthElement = (arr, n = 0) => (n === -1 ? arr.slice(n) : arr.slice(n, n + 1))[0];
```


示例

```js
nthElement(['a', 'b', 'c'], 1); // 'b'
nthElement(['a', 'b', 'b'], -3); // 'a'
```





### offset

Moves the specified amount of elements to the end of the array.

Use `Array.prototype.slice()` twice to get the elements after the specified index and the elements before that.
Use the spread operator(`...`) to combine the two into one array.
If `offset` is negative, the elements will be moved from end to start.

```js
const offset = (arr, offset) => [...arr.slice(offset), ...arr.slice(0, offset)];
```


示例

```js
offset([1, 2, 3, 4, 5], 2); // [3, 4, 5, 1, 2]
offset([1, 2, 3, 4, 5], -2); // [4, 5, 1, 2, 3]
```





### partition

Groups the elements into two arrays, depending on the provided function's truthiness for each element.

Use `Array.prototype.reduce()` to create an array of two arrays.
Use `Array.prototype.push()` to add elements for which `fn` returns `true` to the first array and elements for which `fn` returns `false` to the second one.

```js
const partition = (arr, fn) =>
  arr.reduce(
    (acc, val, i, arr) => {
      acc[fn(val, i, arr) ? 0 : 1].push(val);
      return acc;
    },
    [[], []]
  );
```


示例

```js
const users = [{ user: 'barney', age: 36, active: false }, { user: 'fred', age: 40, active: true }];
partition(users, o => o.active); // [[{ 'user': 'fred',    'age': 40, 'active': true }],[{ 'user': 'barney',  'age': 36, 'active': false }]]
```





### permutations ![advanced](/advanced.svg)

⚠️ **WARNING**: This function's execution time increases exponentially with each array element. Anything more than 8 to 10 entries will cause your browser to hang as it tries to solve all the different combinations.

Generates all permutations of an array's elements (contains duplicates).

Use recursion.
For each element in the given array, create all the partial permutations for the rest of its elements.
Use `Array.prototype.map()` to combine the element with each partial permutation, then `Array.prototype.reduce()` to combine all permutations in one array.
Base cases are for array `length` equal to `2` or `1`.

```js
const permutations = arr => {
  if (arr.length <= 2) return arr.length === 2 ? [arr, [arr[1], arr[0]]] : arr;
  return arr.reduce(
    (acc, item, i) =>
      acc.concat(
        permutations([...arr.slice(0, i), ...arr.slice(i + 1)]).map(val => [item, ...val])
      ),
    []
  );
};
```


示例

```js
permutations([1, 33, 5]); // [ [ 1, 33, 5 ], [ 1, 5, 33 ], [ 33, 1, 5 ], [ 33, 5, 1 ], [ 5, 1, 33 ], [ 5, 33, 1 ] ]
```





### pull

Mutates the original array to filter out the values specified.

Use `Array.prototype.filter()` and `Array.prototype.includes()` to pull out the values that are not needed.
Use `Array.prototype.length = 0` to mutate the passed in an array by resetting it's length to zero and `Array.prototype.push()` to re-populate it with only the pulled values.

_(For a snippet that does not mutate the original array see [`without`](#without))_

```js
const pull = (arr, ...args) => {
  let argState = Array.isArray(args[0]) ? args[0] : args;
  let pulled = arr.filter((v, i) => !argState.includes(v));
  arr.length = 0;
  pulled.forEach(v => arr.push(v));
};
```


示例

```js
let myArray = ['a', 'b', 'c', 'a', 'b', 'c'];
pull(myArray, 'a', 'c'); // myArray = [ 'b', 'b' ]
```





### pullAtIndex ![advanced](/advanced.svg)

Mutates the original array to filter out the values at the specified indexes.

Use `Array.prototype.filter()` and `Array.prototype.includes()` to pull out the values that are not needed.
Use `Array.prototype.length = 0` to mutate the passed in an array by resetting it's length to zero and `Array.prototype.push()` to re-populate it with only the pulled values.
Use `Array.prototype.push()` to keep track of pulled values

```js
const pullAtIndex = (arr, pullArr) => {
  let removed = [];
  let pulled = arr
    .map((v, i) => (pullArr.includes(i) ? removed.push(v) : v))
    .filter((v, i) => !pullArr.includes(i));
  arr.length = 0;
  pulled.forEach(v => arr.push(v));
  return removed;
};
```


示例

```js
let myArray = ['a', 'b', 'c', 'd'];
let pulled = pullAtIndex(myArray, [1, 3]); // myArray = [ 'a', 'c' ] , pulled = [ 'b', 'd' ]
```





### pullAtValue ![advanced](/advanced.svg)

Mutates the original array to filter out the values specified. Returns the removed elements.

Use `Array.prototype.filter()` and `Array.prototype.includes()` to pull out the values that are not needed.
Use `Array.prototype.length = 0` to mutate the passed in an array by resetting it's length to zero and `Array.prototype.push()` to re-populate it with only the pulled values.
Use `Array.prototype.push()` to keep track of pulled values

```js
const pullAtValue = (arr, pullArr) => {
  let removed = [],
    pushToRemove = arr.forEach((v, i) => (pullArr.includes(v) ? removed.push(v) : v)),
    mutateTo = arr.filter((v, i) => !pullArr.includes(v));
  arr.length = 0;
  mutateTo.forEach(v => arr.push(v));
  return removed;
};
```


示例

```js
let myArray = ['a', 'b', 'c', 'd'];
let pulled = pullAtValue(myArray, ['b', 'd']); // myArray = [ 'a', 'c' ] , pulled = [ 'b', 'd' ]
```





### pullBy ![advanced](/advanced.svg)

Mutates the original array to filter out the values specified, based on a given iterator function.

Check if the last argument provided in a function.
Use `Array.prototype.map()` to apply the iterator function `fn` to all array elements.
Use `Array.prototype.filter()` and `Array.prototype.includes()` to pull out the values that are not needed.
Use `Array.prototype.length = 0` to mutate the passed in an array by resetting it's length to zero and `Array.prototype.push()` to re-populate it with only the pulled values.

```js
const pullBy = (arr, ...args) => {
  const length = args.length;
  let fn = length > 1 ? args[length - 1] : undefined;
  fn = typeof fn == 'function' ? (args.pop(), fn) : undefined;
  let argState = (Array.isArray(args[0]) ? args[0] : args).map(val => fn(val));
  let pulled = arr.filter((v, i) => !argState.includes(fn(v)));
  arr.length = 0;
  pulled.forEach(v => arr.push(v));
};
```


示例

```js
var myArray = [{ x: 1 }, { x: 2 }, { x: 3 }, { x: 1 }];
pullBy(myArray, [{ x: 1 }, { x: 3 }], o => o.x); // myArray = [{ x: 2 }]
```





### reducedFilter

Filter an array of objects based on a condition while also filtering out unspecified keys.

Use `Array.prototype.filter()` to filter the array based on the predicate `fn` so that it returns the objects for which the condition returned a truthy value.
On the filtered array, use `Array.prototype.map()` to return the new object using `Array.prototype.reduce()` to filter out the keys which were not supplied as the `keys` argument.

```js
const reducedFilter = (data, keys, fn) =>
  data.filter(fn).map(el =>
    keys.reduce((acc, key) => {
      acc[key] = el[key];
      return acc;
    }, {})
  );
```


示例

```js
const data = [
  {
    id: 1,
    name: 'john',
    age: 24
  },
  {
    id: 2,
    name: 'mike',
    age: 50
  }
];

reducedFilter(data, ['id', 'name'], item => item.age > 24); // [{ id: 2, name: 'mike'}]
```





### reduceSuccessive

Applies a function against an accumulator and each element in the array (from left to right), returning an array of successively reduced values.

Use `Array.prototype.reduce()` to apply the given function to the given array, storing each new result.

```js
const reduceSuccessive = (arr, fn, acc) =>
  arr.reduce((res, val, i, arr) => (res.push(fn(res.slice(-1)[0], val, i, arr)), res), [acc]);
```


示例

```js
reduceSuccessive([1, 2, 3, 4, 5, 6], (acc, val) => acc + val, 0); // [0, 1, 3, 6, 10, 15, 21]
```





### reduceWhich

Returns the minimum/maximum value of an array, after applying the provided function to set comparing rule.

Use `Array.prototype.reduce()` in combination with the `comparator` function to get the appropriate element in the array.
You can omit the second parameter, `comparator`, to use the default one that returns the minimum element in the array.

```js
const reduceWhich = (arr, comparator = (a, b) => a - b) =>
  arr.reduce((a, b) => (comparator(a, b) >= 0 ? b : a));
```


示例

```js
reduceWhich([1, 3, 2]); // 1
reduceWhich([1, 3, 2], (a, b) => b - a); // 3
reduceWhich(
  [{ name: 'Tom', age: 12 }, { name: 'Jack', age: 18 }, { name: 'Lucy', age: 9 }],
  (a, b) => a.age - b.age
); // {name: "Lucy", age: 9}
```





### reject

Takes a predicate and array, like `Array.prototype.filter()`, but only keeps `x` if `pred(x) === false`.

```js
const reject = (pred, array) => array.filter((...args) => !pred(...args));
```


示例

```js
reject(x => x % 2 === 0, [1, 2, 3, 4, 5]); // [1, 3, 5]
reject(word => word.length > 4, ['Apple', 'Pear', 'Kiwi', 'Banana']); // ['Pear', 'Kiwi']
```





### remove

Removes elements from an array for which the given function returns `false`.

Use `Array.prototype.filter()` to find array elements that return truthy values and `Array.prototype.reduce()` to remove elements using `Array.prototype.splice()`.
The `func` is invoked with three arguments (`value, index, array`).

```js

const remove = (arr, func) =>
  Array.isArray(arr)
    ? arr.filter(func).reduce((acc, val) => {
      arr.splice(arr.indexOf(val), 1);
      return acc.concat(val);
    }, [])
    : [];
```


示例

```js
remove([1, 2, 3, 4], n => n % 2 === 0); // [2, 4]
```





### sample

Returns a random element from an array.

Use `Math.random()` to generate a random number, multiply it by `length` and round it off to the nearest whole number using `Math.floor()`.
This method also works with strings.

```js
const sample = arr => arr[Math.floor(Math.random() * arr.length)];
```


示例

```js
sample([3, 7, 9, 11]); // 9
```





### sampleSize

Gets `n` random elements at unique keys from `array` up to the size of `array`.

Shuffle the array using the [Fisher-Yates algorithm](https://github.com/30-seconds/30-seconds-of-code#shuffle).
Use `Array.prototype.slice()` to get the first `n` elements.
Omit the second argument, `n` to get only one element at random from the array.

```js
const sampleSize = ([...arr], n = 1) => {
  let m = arr.length;
  while (m) {
    const i = Math.floor(Math.random() * m--);
    [arr[m], arr[i]] = [arr[i], arr[m]];
  }
  return arr.slice(0, n);
};
```


示例

```js
sampleSize([1, 2, 3], 2); // [3,1]
sampleSize([1, 2, 3], 4); // [2,3,1]
```





### shank

Has the same functionality as [`Array.prototype.splice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice), but returning a new array instead of mutating the original array.

Use `Array.prototype.slice()` and `Array.prototype.concat()` to get a new array with the new contents after removing existing elements and/or adding new elements.
Omit the second argument, `index`, to start at `0`.
Omit the third argument, `delCount`, to remove `0` elements.
Omit the fourth argument, `elements`, in order to not add any new elements.

```js
const shank = (arr, index = 0, delCount = 0, ...elements) =>
  arr
    .slice(0, index)
    .concat(elements)
    .concat(arr.slice(index + delCount));
```


示例

```js
const names = ['alpha', 'bravo', 'charlie'];
const namesAndDelta = shank(names, 1, 0, 'delta'); // [ 'alpha', 'delta', 'bravo', 'charlie' ]
const namesNoBravo = shank(names, 1, 1); // [ 'alpha', 'charlie' ]
console.log(names); // ['alpha', 'bravo', 'charlie']
```





### shuffle

Randomizes the order of the values of an array, returning a new array.

Uses the [Fisher-Yates algorithm](https://github.com/30-seconds/30-seconds-of-code#shuffle) to reorder the elements of the array.

```js
const shuffle = ([...arr]) => {
  let m = arr.length;
  while (m) {
    const i = Math.floor(Math.random() * m--);
    [arr[m], arr[i]] = [arr[i], arr[m]];
  }
  return arr;
};
```


示例

```js
const foo = [1, 2, 3];
shuffle(foo); // [2, 3, 1], foo = [1, 2, 3]
```





### similarity

Returns an array of elements that appear in both arrays.

Use `Array.prototype.filter()` to remove values that are not part of `values`, determined using `Array.prototype.includes()`.

```js
const similarity = (arr, values) => arr.filter(v => values.includes(v));
```


示例

```js
similarity([1, 2, 3], [1, 2, 4]); // [1, 2]
```





### sortedIndex

Returns the lowest index at which value should be inserted into array in order to maintain its sort order.

Check if the array is sorted in descending order (loosely).
Use `Array.prototype.findIndex()` to find the appropriate index where the element should be inserted.

```js
const sortedIndex = (arr, n) => {
  const isDescending = arr[0] > arr[arr.length - 1];
  const index = arr.findIndex(el => (isDescending ? n >= el : n <= el));
  return index === -1 ? arr.length : index;
};
```


示例

```js
sortedIndex([5, 3, 2, 1], 4); // 1
sortedIndex([30, 50], 40); // 1
```





### sortedIndexBy

Returns the lowest index at which value should be inserted into array in order to maintain its sort order, based on a provided iterator function.

Check if the array is sorted in descending order (loosely).
Use `Array.prototype.findIndex()` to find the appropriate index where the element should be inserted, based on the iterator function `fn`.

```js
const sortedIndexBy = (arr, n, fn) => {
  const isDescending = fn(arr[0]) > fn(arr[arr.length - 1]);
  const val = fn(n);
  const index = arr.findIndex(el => (isDescending ? val >= fn(el) : val <= fn(el)));
  return index === -1 ? arr.length : index;
};
```


示例

```js
sortedIndexBy([{ x: 4 }, { x: 5 }], { x: 4 }, o => o.x); // 0
```





### sortedLastIndex

Returns the highest index at which value should be inserted into array in order to maintain its sort order.

Check if the array is sorted in descending order (loosely).
Use `Array.prototype.reverse()` and `Array.prototype.findIndex()` to find the appropriate last index where the element should be inserted.

```js
const sortedLastIndex = (arr, n) => {
  const isDescending = arr[0] > arr[arr.length - 1];
  const index = arr.reverse().findIndex(el => (isDescending ? n <= el : n >= el));
  return index === -1 ? 0 : arr.length - index;
};
```


示例

```js
sortedLastIndex([10, 20, 30, 30, 40], 30); // 4
```





### sortedLastIndexBy

Returns the highest index at which value should be inserted into array in order to maintain its sort order, based on a provided iterator function.

Check if the array is sorted in descending order (loosely).
Use `Array.prototype.map()` to apply the iterator function to all elements of the array.
Use `Array.prototype.reverse()` and `Array.prototype.findIndex()` to find the appropriate last index where the element should be inserted, based on the provided iterator function.

```js
const sortedLastIndexBy = (arr, n, fn) => {
  const isDescending = fn(arr[0]) > fn(arr[arr.length - 1]);
  const val = fn(n);
  const index = arr
    .map(fn)
    .reverse()
    .findIndex(el => (isDescending ? val <= el : val >= el));
  return index === -1 ? 0 : arr.length - index;
};
```


示例

```js
sortedLastIndexBy([{ x: 4 }, { x: 5 }], { x: 4 }, o => o.x); // 1
```





### stableSort ![advanced](/advanced.svg)

Performs stable sorting of an array, preserving the initial indexes of items when their values are the same.
Does not mutate the original array, but returns a new array instead.

Use `Array.prototype.map()` to pair each element of the input array with its corresponding index.
Use `Array.prototype.sort()` and a `compare` function to sort the list, preserving their initial order if the items compared are equal.
Use `Array.prototype.map()` to convert back to the initial array items.

```js
const stableSort = (arr, compare) =>
  arr
    .map((item, index) => ({ item, index }))
    .sort((a, b) => compare(a.item, b.item) || a.index - b.index)
    .map(({ item }) => item);
```


示例

```js
const arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const stable = stableSort(arr, () => 0); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```





### symmetricDifference

Returns the symmetric difference between two arrays, without filtering out duplicate values.

Create a `Set` from each array, then use `Array.prototype.filter()` on each of them to only keep values not contained in the other.

```js
const symmetricDifference = (a, b) => {
  const sA = new Set(a),
    sB = new Set(b);
  return [...a.filter(x => !sB.has(x)), ...b.filter(x => !sA.has(x))];
};
```


示例

```js
symmetricDifference([1, 2, 3], [1, 2, 4]); // [3, 4]
symmetricDifference([1, 2, 2], [1, 3, 1]); // [2, 2, 3]
```





### symmetricDifferenceBy

Returns the symmetric difference between two arrays, after applying the provided function to each array element of both.

Create a `Set` by applying `fn` to each array's elements, then use `Array.prototype.filter()` on each of them to only keep values not contained in the other.

```js
const symmetricDifferenceBy = (a, b, fn) => {
  const sA = new Set(a.map(v => fn(v))),
    sB = new Set(b.map(v => fn(v)));
  return [...a.filter(x => !sB.has(fn(x))), ...b.filter(x => !sA.has(fn(x)))];
};
```


示例

```js
symmetricDifferenceBy([2.1, 1.2], [2.3, 3.4], Math.floor); // [ 1.2, 3.4 ]
```





### symmetricDifferenceWith

Returns the symmetric difference between two arrays, using a provided function as a comparator.

Use `Array.prototype.filter()` and `Array.prototype.findIndex()` to find the appropriate values.

```js
const symmetricDifferenceWith = (arr, val, comp) => [
  ...arr.filter(a => val.findIndex(b => comp(a, b)) === -1),
  ...val.filter(a => arr.findIndex(b => comp(a, b)) === -1)
];
```


示例

```js
symmetricDifferenceWith(
  [1, 1.2, 1.5, 3, 0],
  [1.9, 3, 0, 3.9],
  (a, b) => Math.round(a) === Math.round(b)
); // [1, 1.2, 3.9]
```





### tail

Returns all elements in an array except for the first one.

Return `Array.prototype.slice(1)` if the array's `length` is more than `1`, otherwise, return the whole array.

```js
const tail = arr => (arr.length > 1 ? arr.slice(1) : arr);
```


示例

```js
tail([1, 2, 3]); // [2,3]
tail([1]); // [1]
```





### take

Returns an array with n elements removed from the beginning.

Use `Array.prototype.slice()` to create a slice of the array with `n` elements taken from the beginning.

```js
const take = (arr, n = 1) => arr.slice(0, n);
```


示例

```js
take([1, 2, 3], 5); // [1, 2, 3]
take([1, 2, 3], 0); // []
```





### takeRight

Returns an array with n elements removed from the end.

Use `Array.prototype.slice()` to create a slice of the array with `n` elements taken from the end.

```js
const takeRight = (arr, n = 1) => arr.slice(arr.length - n, arr.length);
```


示例

```js
takeRight([1, 2, 3], 2); // [ 2, 3 ]
takeRight([1, 2, 3]); // [3]
```





### takeRightWhile

Removes elements from the end of an array until the passed function returns `true`. Returns the removed elements.

Loop through the array, using a `Array.prototype.reduceRight()` and accumulating elements while the function returns falsy value.

```js
const takeRightWhile = (arr, func) =>
  arr.reduceRight((acc, el) => (func(el) ? acc : [el, ...acc]), []);
```


示例

```js
takeRightWhile([1, 2, 3, 4], n => n < 3); // [3, 4]
```





### takeWhile

Removes elements in an array until the passed function returns `true`. Returns the removed elements.

Loop through the array, using a `for...of` loop over `Array.prototype.entries()` until the returned value from the function is `true`.
Return the removed elements, using `Array.prototype.slice()`.

```js
const takeWhile = (arr, func) => {
  for (const [i, val] of arr.entries()) if (func(val)) return arr.slice(0, i);
  return arr;
};
```


示例

```js
takeWhile([1, 2, 3, 4], n => n >= 3); // [1, 2]
```





### toHash

Reduces a given Array-like into a value hash (keyed data store).

Given an Iterable or Array-like structure, call `Array.prototype.reduce.call()` on the provided object to step over it and return an Object, keyed by the reference value.

```js
const toHash = (object, key) =>
  Array.prototype.reduce.call(
    object,
    (acc, data, index) => ((acc[!key ? index : data[key]] = data), acc),
    {}
  );
```


示例

```js
toHash([4, 3, 2, 1]); // { 0: 4, 1: 3, 2: 2, 3: 1 }
toHash([{ a: 'label' }], 'a'); // { label: { a: 'label' } }
// A more in depth example:
let users = [{ id: 1, first: 'Jon' }, { id: 2, first: 'Joe' }, { id: 3, first: 'Moe' }];
let managers = [{ manager: 1, employees: [2, 3] }];
// We use function here because we want a bindable reference, but a closure referencing the hash would work, too.
managers.forEach(
  manager =>
    (manager.employees = manager.employees.map(function(id) {
      return this[id];
    }, toHash(users, 'id')))
);
managers; // [ { manager:1, employees: [ { id: 2, first: "Joe" }, { id: 3, first: "Moe" } ] } ]
```





### union

Returns every element that exists in any of the two arrays once.

Create a `Set` with all values of `a` and `b` and convert to an array.

```js
const union = (a, b) => Array.from(new Set([...a, ...b]));
```


示例

```js
union([1, 2, 3], [4, 3, 2]); // [1,2,3,4]
```





### unionBy

Returns every element that exists in any of the two arrays once, after applying the provided function to each array element of both.

Create a `Set` by applying all `fn` to all values of `a`.
Create a `Set` from `a` and all elements in `b` whose value, after applying `fn` does not match a value in the previously created set.
Return the last set converted to an array.

```js
const unionBy = (a, b, fn) => {
  const s = new Set(a.map(fn));
  return Array.from(new Set([...a, ...b.filter(x => !s.has(fn(x)))]));
};
```


示例

```js
unionBy([2.1], [1.2, 2.3], Math.floor); // [2.1, 1.2]
```





### unionWith

Returns every element that exists in any of the two arrays once, using a provided comparator function.

Create a `Set` with all values of `a` and values in `b` for which the comparator finds no matches in `a`, using `Array.prototype.findIndex()`.

```js
const unionWith = (a, b, comp) =>
  Array.from(new Set([...a, ...b.filter(x => a.findIndex(y => comp(x, y)) === -1)]));
```


示例

```js
unionWith([1, 1.2, 1.5, 3, 0], [1.9, 3, 0, 3.9], (a, b) => Math.round(a) === Math.round(b)); // [1, 1.2, 1.5, 3, 0, 3.9]
```





### uniqueElements

Returns all unique values of an array.

Use ES6 `Set` and the `...rest` operator to discard all duplicated values.

```js
const uniqueElements = arr => [...new Set(arr)];
```


示例

```js
uniqueElements([1, 2, 2, 3, 4, 4, 5]); // [1, 2, 3, 4, 5]
```





### uniqueElementsBy

Returns all unique values of an array, based on a provided comparator function.

Use `Array.prototype.reduce()` and `Array.prototype.some()` for an array containing only the first unique occurence of each value, based on the comparator function, `fn`.
The comparator function takes two arguments: the values of the two elements being compared.

```js
const uniqueElementsBy = (arr, fn) =>
  arr.reduce((acc, v) => {
    if (!acc.some(x => fn(v, x))) acc.push(v);
    return acc;
  }, []);
```


示例

```js
uniqueElementsBy(
  [
    { id: 0, value: 'a' },
    { id: 1, value: 'b' },
    { id: 2, value: 'c' },
    { id: 1, value: 'd' },
    { id: 0, value: 'e' }
  ],
  (a, b) => a.id == b.id
); // [ { id: 0, value: 'a' }, { id: 1, value: 'b' }, { id: 2, value: 'c' } ]
```





### uniqueElementsByRight

Returns all unique values of an array, based on a provided comparator function.

Use `Array.prototype.reduce()` and `Array.prototype.some()` for an array containing only the last unique occurence of each value, based on the comparator function, `fn`.
The comparator function takes two arguments: the values of the two elements being compared.

```js
const uniqueElementsByRight = (arr, fn) =>
  arr.reduceRight((acc, v) => {
    if (!acc.some(x => fn(v, x))) acc.push(v);
    return acc;
  }, []);
```


示例

```js
uniqueElementsByRight(
  [
    { id: 0, value: 'a' },
    { id: 1, value: 'b' },
    { id: 2, value: 'c' },
    { id: 1, value: 'd' },
    { id: 0, value: 'e' }
  ],
  (a, b) => a.id == b.id
); // [ { id: 0, value: 'e' }, { id: 1, value: 'd' }, { id: 2, value: 'c' } ]
```





### uniqueSymmetricDifference

Returns the unique symmetric difference between two arrays, not containing duplicate values from either array.

Use `Array.prototype.filter()` and `Array.prototype.includes()` on each array to remove values contained in the other, then create a `Set` from the results, removing duplicate values.

```js
const uniqueSymmetricDifference = (a, b) => [
  ...new Set([...a.filter(v => !b.includes(v)), ...b.filter(v => !a.includes(v))])
];
```


示例

```js
uniqueSymmetricDifference([1, 2, 3], [1, 2, 4]); // [3, 4]
uniqueSymmetricDifference([1, 2, 2], [1, 3, 1]); // [2, 3]
```





### unzip

Creates an array of arrays, ungrouping the elements in an array produced by [zip](#zip).

Use `Math.max.apply()` to get the longest subarray in the array, `Array.prototype.map()` to make each element an array.
Use `Array.prototype.reduce()` and `Array.prototype.forEach()` to map grouped values to individual arrays.

```js
const unzip = arr =>
  arr.reduce(
    (acc, val) => (val.forEach((v, i) => acc[i].push(v)), acc),
    Array.from({
      length: Math.max(...arr.map(x => x.length))
    }).map(x => [])
  );
```


示例

```js
unzip([['a', 1, true], ['b', 2, false]]); // [['a', 'b'], [1, 2], [true, false]]
unzip([['a', 1, true], ['b', 2]]); // [['a', 'b'], [1, 2], [true]]
```





### unzipWith ![advanced](/advanced.svg)

Creates an array of elements, ungrouping the elements in an array produced by [zip](#zip) and applying the provided function.

Use `Math.max.apply()` to get the longest subarray in the array, `Array.prototype.map()` to make each element an array.
Use `Array.prototype.reduce()` and `Array.prototype.forEach()` to map grouped values to individual arrays.
Use `Array.prototype.map()` and the spread operator (`...`) to apply `fn` to each individual group of elements.

```js
const unzipWith = (arr, fn) =>
  arr
    .reduce(
      (acc, val) => (val.forEach((v, i) => acc[i].push(v)), acc),
      Array.from({
        length: Math.max(...arr.map(x => x.length))
      }).map(x => [])
    )
    .map(val => fn(...val));
```


示例

```js
unzipWith([[1, 10, 100], [2, 20, 200]], (...args) => args.reduce((acc, v) => acc + v, 0)); // [3, 30, 300]
```





### without

Filters out the elements of an array, that have one of the specified values.

Use `Array.prototype.filter()` to create an array excluding(using `!Array.includes()`) all given values.

_(For a snippet that mutates the original array see [`pull`](#pull))_

```js
const without = (arr, ...args) => arr.filter(v => !args.includes(v));
```


示例

```js
without([2, 1, 2, 3], 1, 2); // [3]
```





### xProd

Creates a new array out of the two supplied by creating each possible pair from the arrays.

Use `Array.prototype.reduce()`, `Array.prototype.map()` and `Array.prototype.concat()` to produce every possible pair from the elements of the two arrays and save them in an array.

```js
const xProd = (a, b) => a.reduce((acc, x) => acc.concat(b.map(y => [x, y])), []);
```


示例

```js
xProd([1, 2], ['a', 'b']); // [[1, 'a'], [1, 'b'], [2, 'a'], [2, 'b']]
```





### zip

Creates an array of elements, grouped based on the position in the original arrays.

Use `Math.max.apply()` to get the longest array in the arguments.
Creates an array with that length as return value and use `Array.from()` with a map-function to create an array of grouped elements.
If lengths of the argument-arrays vary, `undefined` is used where no value could be found.

```js
const zip = (...arrays) => {
  const maxLength = Math.max(...arrays.map(x => x.length));
  return Array.from({ length: maxLength }).map((_, i) => {
    return Array.from({ length: arrays.length }, (_, k) => arrays[k][i]);
  });
};
```


示例

```js
zip(['a', 'b'], [1, 2], [true, false]); // [['a', 1, true], ['b', 2, false]]
zip(['a'], [1, 2], [true, false]); // [['a', 1, true], [undefined, 2, false]]
```





### zipObject

Given an array of valid property identifiers and an array of values, return an object associating the properties to the values.

Since an object can have undefined values but not undefined property pointers, the array of properties is used to decide the structure of the resulting object using `Array.prototype.reduce()`.

```js
const zipObject = (props, values) =>
  props.reduce((obj, prop, index) => ((obj[prop] = values[index]), obj), {});
```


示例

```js
zipObject(['a', 'b', 'c'], [1, 2]); // {a: 1, b: 2, c: undefined}
zipObject(['a', 'b'], [1, 2, 3]); // {a: 1, b: 2}
```





### zipWith ![advanced](/advanced.svg)

Creates an array of elements, grouped based on the position in the original arrays and using function as the last value to specify how grouped values should be combined.

Check if the last argument provided is a function.
Use `Math.max()` to get the longest array in the arguments.
Creates an array with that length as return value and use `Array.from()` with a map-function to create an array of grouped elements.
If lengths of the argument-arrays vary, `undefined` is used where no value could be found.
The function is invoked with the elements of each group `(...group)`.

```js
const zipWith = (...array) => {
  const fn = typeof array[array.length - 1] === 'function' ? array.pop() : undefined;
  return Array.from(
    { length: Math.max(...array.map(a => a.length)) },
    (_, i) => (fn ? fn(...array.map(a => a[i])) : array.map(a => a[i]))
  );
};
```


示例

```js
zipWith([1, 2], [10, 20], [100, 200], (a, b, c) => a + b + c); // [111,222]
zipWith(
  [1, 2, 3],
  [10, 20],
  [100, 200],
  (a, b, c) => (a != null ? a : 'a') + (b != null ? b : 'b') + (c != null ? c : 'c')
); // [111, 222, '3bc']
```




