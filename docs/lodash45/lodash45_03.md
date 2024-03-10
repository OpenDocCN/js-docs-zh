# Array

# Array

# chunk

## chunk

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5508 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.chunk "See the npm package.")

```
_.chunk(array, [size=0]) 
```

将数组拆分成多个 size 长度的块，并组成一个新数组。 如果数组无法被分割成全部等长的块，那么最后剩余的元素将组成一个块。

### 参数

1.  array (Array)

    需要被处理的数组

2.  [size=0] (number)

    每个块的长度

### 返回值 (Array)

返回一个拆分好的新数组

### 示例

```
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']] 
```

# compact

## compact

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5539 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.compact "See the npm package.")

```
_.compact(array) 
```

创建一个移除了所有假值的数组。例如：`false`、`null`、 `0`、`""`、`undefined`， 以及`NaN` 都是 “假值”.

### 参数

1.  array (Array)

    需要被处理的数组。

### 返回值 (Array)

返回移除了假值的数组。

### 示例

```
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3] 
```

# concat

## concat

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5574 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.concat "See the npm package.")

```
_.concat(array, [values]) 
```

创建一个用任何数组 或 值连接的新数组。

### 参数

1.  array (Array)

    需要被连接的数组

2.  [values] (...*)

    需要被连接的值的队列

### 返回值 (Array)

返回连接后的新数组

### 示例

```
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);

console.log(other);
// => [1, 2, 3, [4]]

console.log(array);
// => [1] 
```

# difference

## difference

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5596 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.difference "See the npm package.")

```
_.difference(array, [values]) 
```

创建一个差异化后的数组，不包括使用 [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero) 方法提供的数组。

### 参数

1.  array (Array)

    需要处理的数组

2.  [values] (...Array)

    用于对比差异的数组

### 返回值 (Array)

返回一个差异化后的新数组

### 示例

```
_.difference([3, 2, 1], [4, 2]);
// => [3, 1] 
```

# differenceBy

## differenceBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5621 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.differenceby "See the npm package.")

```
_.differenceBy(array, [values], [iteratee=_.identity]) 
```

这个方法类似 `_.difference`，除了它接受一个 iteratee 调用每一个数组和值。iteratee 会传入一个参数：(value)。

### 参数

1.  array (Array)

    需要处理的数组

2.  [values] (...Array)

    用于对比差异的数组

3.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (Array)

返回一个差异化后的新数组

### 示例

```
_.differenceBy([3.1, 2.2, 1.3], [4.4, 2.5], Math.floor);
// => [3.1, 1.3]

// 使用了 `_.property` 的回调结果
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }] 
```

# differenceWith

## differenceWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5648 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.differencewith "See the npm package.")

```
_.differenceWith(array, [values], [comparator]) 
```

这个方法类似 `_.difference`，除了它接受一个 comparator 调用每一个数组元素的值。 comparator 会传入 2 个参数：(arrVal, othVal)。

### 参数

1.  array (Array)

    需要处理的数组

2.  [values] (...Array)

    用于对比差异的数组

3.  [comparator] (Function)

    这个函数会处理每一个元素

### 返回值 (Array)

返回一个差异化后的新数组

### 示例

```
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];

_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual);
// => [{ 'x': 2, 'y': 1 }] 
```

# drop

## drop

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5682 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.drop "See the npm package.")

```
_.drop(array, [n=1]) 
```

裁剪数组中的前 N 个数组，返回剩余的部分。

### 参数

1.  array (Array)

    需要处理的数组

2.  [n=1] (number)

    裁剪的个数

### 返回值 (Array)

返回数组的剩余的部分。

### 示例

```
_.drop([1, 2, 3]);
// => [2, 3]

_.drop([1, 2, 3], 2);
// => [3]

_.drop([1, 2, 3], 5);
// => []

_.drop([1, 2, 3], 0);
// => [1, 2, 3] 
```

# dropRight

## dropRight

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5715 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.dropright "See the npm package.")

```
_.dropRight(array, [n=1]) 
```

从右边开始裁剪数组中的 N 个数组，返回剩余的部分。

### 参数

1.  array (Array)

    需要处理的数组

2.  [n=1] (number)

    裁剪的个数

### 返回值 (Array)

返回数组的剩余的部分。

### 示例

```
_.dropRight([1, 2, 3]);
// => [1, 2]

_.dropRight([1, 2, 3], 2);
// => [1]

_.dropRight([1, 2, 3], 5);
// => []

_.dropRight([1, 2, 3], 0);
// => [1, 2, 3] 
```

# dropRightWhile

## dropRightWhile

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5759 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.droprightwhile "See the npm package.")

```
_.dropRightWhile(array, [predicate=_.identity]) 
```

从右边开始裁剪数组，起点从 `predicate` 返回假值开始。`predicate` 会传入 3 个参数：(value, index, array)。

### 参数

1.  array (Array)

    需要处理的数组

2.  [predicate=_.identity] (Function|Object|string)

    这个函数会在每一次迭代调用

### 返回值 (Array)

返回裁剪后的数组

### 示例

```
var resolve = _.partial(_.map, _, 'user');

var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

resolve( _.dropRightWhile(users, function(o) { return !o.active; }) );
// => ['barney']

// 使用了 `_.matches` 的回调结果
resolve( _.dropRightWhile(users, { 'user': 'pebbles', 'active': false }) );
// => ['barney', 'fred']

// 使用了 `_.matchesProperty` 的回调结果
resolve( _.dropRightWhile(users, ['active', false]) );
// => ['barney']

// 使用了 `_.property` 的回调结果
resolve( _.dropRightWhile(users, 'active') );
// => ['barney', 'fred', 'pebbles'] 
```

# dropWhile

## dropWhile

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5797 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.dropwhile "See the npm package.")

```
_.dropWhile(array, [predicate=_.identity]) 
```

裁剪数组，起点从 `predicate` 返回假值开始。`predicate` 会传入 3 个参数：(value, index, array)。

### 参数

1.  array (Array)

    array 需要处理的数组

2.  [predicate=_.identity] (Function|Object|string)

    这个函数会在每一次迭代调用

### 返回值 (Array)

Returns the slice of `array`.

### 示例

```
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.dropWhile(users, function(o) { return !o.active; });
// => 结果: ['pebbles']

// 使用了 `_.matches` 的回调处理
_.dropWhile(users, { 'user': 'barney', 'active': false });
// => 结果: ['fred', 'pebbles']

// 使用了 `_.matchesProperty` 的回调处理
_.dropWhile(users, ['active', false]);
// => 结果: ['pebbles']

// 使用了 `_.property` 的回调处理
_.dropWhile(users, 'active');
// => 结果: ['barney', 'fred', 'pebbles'] 
```

# fill

## fill

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5830 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.fill "See the npm package.")

```
_.fill(array, value, [start=0], [end=array.length]) 
```

指定 `值` 填充数组，从 `start` 到 `end` 的位置，但不包括 `end` 本身的位置。

**注意:** 这个方法会改变数组

### 参数

1.  array (Array)

    需要填充的数组

2.  value (*)

    填充的值

3.  [start=0] (number)

    开始位置

4.  [end=array.length] (number)

    结束位置

### 返回值 (Array)

返回数组

### 示例

```
var array = [1, 2, 3];

_.fill(array, 'a');
console.log(array);
// => ['a', 'a', 'a']

_.fill(Array(3), 2);
// => [2, 2, 2]

_.fill([4, 6, 8, 10], '*', 1, 3);
// => [4, '*', '*', 10] 
```

# findIndex

## findIndex

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5874 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.findindex "See the npm package.")

```
_.findIndex(array, [predicate=_.identity]) 
```

这个方法类似 `_.find`。除了它返回最先通过 `predicate` 判断为真值的元素的 index ，而不是元素本身。

### 参数

1.  array (Array)

    需要搜索的数组

2.  [predicate=_.identity] (Function|Object|string)

    这个函数会在每一次迭代调用

### 返回值 (number)

返回符合元素的 index，否则返回 `-1`。

### 示例

```
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.findIndex(users, function(o) { return o.user == 'barney'; });
// => 0

// 使用了 `_.matches` 的回调结果
_.findIndex(users, { 'user': 'fred', 'active': false });
// => 1

// 使用了 `_.matchesProperty` 的回调结果
_.findIndex(users, ['active', false]);
// => 0

// 使用了 `_.property` 的回调结果
_.findIndex(users, 'active');
// => 2 
```

# findLastIndex

## findLastIndex

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5912 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.findlastindex "See the npm package.")

```
_.findLastIndex(array, [predicate=_.identity]) 
```

这个方式类似 `_.findIndex` ， 不过它是从右到左的。

### 参数

1.  array (Array)

    需要搜索的数组

2.  [predicate=_.identity] (Function|Object|string)

    这个函数会在每一次迭代调用

### 返回值 (number)

返回符合元素的 index，否则返回 `-1`。

### 示例

```
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.findLastIndex(users, function(o) { return o.user == 'pebbles'; });
// => 2

// 使用了 `_.matches` 的回调结果
_.findLastIndex(users, { 'user': 'barney', 'active': true });
// => 0

// 使用了 `_.matchesProperty` 的回调结果
_.findLastIndex(users, ['active', false]);
// => 2

// 使用了 `_.property` 的回调结果
_.findLastIndex(users, 'active');
// => 0 
```

# flatten

## flatten

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5931 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.flatten "See the npm package.")

```
_.flatten(array) 
```

向上一级展平数组嵌套

### 参数

1.  array (Array)

    需要展平的数组

### 返回值 (Array)

返回展平后的新数组

### 示例

```
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5] 
```

# flattenDeep

## flattenDeep

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5949 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.flattendeep "See the npm package.")

```
_.flattenDeep(array) 
```

递归展平 `数组`.

### 参数

1.  array (Array)

    需要展平的数组

### 返回值 (Array)

返回展平后的新数组

### 示例

```
_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5] 
```

# flattenDepth

## flattenDepth

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5973 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.flattendepth "See the npm package.")

```
_.flattenDepth(array, [depth=1]) 
```

根据 `depth` 递归展平 `数组` 的层级

### 参数

1.  array (Array)

    需要展平的数组

2.  [depth=1] (number)

    展平的层级

### 返回值 (Array)

返回展平后的新数组

### 示例

```
var array = [1, [2, [3, [4]], 5]];

_.flattenDepth(array, 1);
// => [1, 2, [3, [4]], 5]

_.flattenDepth(array, 2);
// => [1, 2, 3, [4], 5] 
```

# fromPairs

## fromPairs

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L5995 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.frompairs "See the npm package.")

```
_.fromPairs(pairs) 
```

反向版 `_.toPairs`，这个方法返回一个由键值对构成的对象。

### 参数

1.  pairs (Array)

    键值对

### 返回值 (Object)

返回一个新对象

### 示例

```
_.fromPairs([['fred', 30], ['barney', 40]]);
// => { 'fred': 30, 'barney': 40 } 
```

# head first

## head first

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6024 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.head "See the npm package.")

```
_.head(array) 
```

获得数组的首个元素

### 参数

1.  array (Array)

    要检索的数组

### 返回值 (*)

返回数组中的首个元素

### 示例

```
_.head([1, 2, 3]);
// => 1

_.head([]);
// => undefined 
```

# indexOf

## indexOf

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6047 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.indexof "See the npm package.")

```
_.indexOf(array, value, [fromIndex=0]) 
```

根据 value 使用 SameValueZero 等值比较返回数组中首次匹配的 index， 如果 fromIndex 为负值，将从数组尾端索引进行匹配，如果将 fromIndex 设置为 true，将使用更快的二进制检索机制。

### 参数

1.  array (Array)

    要检索的数组

2.  value (*)

    要检索的值

3.  [fromIndex=0] (number)

    需要检索的起始位置，如果为 true 将使用二进制检索方式。

### 返回值 (number)

返回匹配值的 index，否则返回 -1。

### 示例

```
_.indexOf([1, 2, 1, 2], 2);
// => 1

// 使用了 `fromIndex`
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3 
```

# initial

## initial

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6072 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.initial "See the npm package.")

```
_.initial(需要检索的数组) 
```

获取数组中除了最后一个元素之外的所有元素

### 参数

1.  需要检索的数组 (Array)

### 返回值 (Array)

返回没有最后一个元素的数组

### 示例

```
_.initial([1, 2, 3]);
// => [1, 2] 
```

# intersection

## intersection

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6089 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.intersection "See the npm package.")

```
_.intersection([arrays]) 
```

创建一个包含所有使用 [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero) 进行等值比较后筛选的唯一值数组。

### 参数

1.  [arrays] (...Array)

    需要处理的数组队列

### 返回值 (Array)

返回数组中所有数组共享元素的新数组

### 示例

```
_.intersection([2, 1], [4, 2], [1, 2]);
// => [2] 
```

# intersectionBy

## intersectionBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6114 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.intersectionby "See the npm package.")

```
_.intersectionBy([arrays], [iteratee=_.identity]) 
```

这个方法类似 `_.intersection`，除了它接受一个 iteratee 调用每一个数组和值。iteratee 会传入一个参数：(value)

### 参数

1.  [arrays] (...Array)

    需要检索的数组

2.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (Array)

返回数组中共享元素的新数组

### 示例

```
_.intersectionBy([2.1, 1.2], [4.3, 2.4], Math.floor);
// => [2.1]

// 使用了 `_.property` 的回调结果
_.intersectionBy([{ 'x': 1 }], [{ 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }] 
```

# intersectionWith

## intersectionWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6145 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.intersectionwith "See the npm package.")

```
_.intersectionWith([arrays], [comparator]) 
```

这个方法类似 `_.intersection`，除了它接受一个 comparator 调用每一个数组和值。iteratee 会传入 2 个参数：((arrVal, othVal)

### 参数

1.  [arrays] (...Array)

    需要检索的数组

2.  [comparator] (Function)

    这个函数会处理每一个元素

### 返回值 (Array)

返回数组中共享元素的新数组

### 示例

```
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.intersectionWith(objects, others, _.isEqual);
// => [{ 'x': 1, 'y': 2 }] 
```

# join

## join

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6173 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.join "See the npm package.")

```
_.join(array, [separator=',']) 
```

将数组中的所有元素转换为由 `separator` 分隔的字符串。

### 参数

1.  array (Array)

    需要转换的数组

2.  [separator=','] (string)

    分隔符

### 返回值 (string)

返回连接好的字符串

### 示例

```
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c' 
```

# last

## last

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6190 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.last "See the npm package.")

```
_.last(array) 
```

获取数组中的最后一个元素

### 参数

1.  array (Array)

    要检索的数组

### 返回值 (*)

返回数组中的最后一个元素

### 示例

```
_.last([1, 2, 3]);
// => 3 
```

# lastIndexOf

## lastIndexOf

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6218 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.lastindexof "See the npm package.")

```
_.lastIndexOf(array, value, [fromIndex=array.length-1]) 
```

这个方法类似 `_.indexOf`，除了它是从右到左遍历元素的。 这个方法类似 `_.indexOf` except that it iterates over elements of `array` from right to left.

### 参数

1.  array (Array)

    需要检索的数组

2.  value (*)

    要检索的值

3.  [fromIndex=array.length-1] (number)

    检索 index 的起点

### 返回值 (number)

返回匹配元素的 index，否则返回 -1

### 示例

```
_.lastIndexOf([1, 2, 1, 2], 2);
// => 3

// 使用了 `fromIndex`
_.lastIndexOf([1, 2, 1, 2], 2, 2);
// => 1 
```

# prototype.reverse

## prototype.reverse

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6405 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.prototype.reverse "See the npm package.")

```
_.prototype.reverse() 
```

反转数组，第一个元素移动到最后一位，第二个元素移动到倒数第二，类似这样。

**注意:** 这个方法会改变数组，根据 [`Array#reverse`](https://mdn.io/Array/reverse)

### 返回值 (Array)

返回原数组

### 示例

```
var array = [1, 2, 3];

_.reverse(array);
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1] 
```

# pull

## pull

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6258 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.pull "See the npm package.")

```
_.pull(array, [values]) 
```

移除所有经过 [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero) 等值比较为 true 的元素

**注意:** 不同于 `_.without`，这个方法会改变数组。

### 参数

1.  array (Array)

    需要调整的数组

2.  [values] (...*)

    要移除的值

### 返回值 (Array)

返回数组本身

### 示例

```
var array = [1, 2, 3, 1, 2, 3];

_.pull(array, 2, 3);
console.log(array);
// => [1, 1] 
```

# pullAll

## pullAll

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6279 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.pullall "See the npm package.")

```
_.pullAll(array, values) 
```

这个方式类似 `_.pull`，除了它接受数组形式的一系列值。

**注意:** 不同于 `_.difference`，这个方法会改变数组。

### 参数

1.  array (Array)

    需要调整的数组

2.  values (Array)

    要移除的值

### 返回值 (Array)

返回数组本身

### 示例

```
var array = [1, 2, 3, 1, 2, 3];

_.pullAll(array, [2, 3]);
console.log(array);
// => [1, 1] 
```

# pullAllBy

## pullAllBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6305 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.pullallby "See the npm package.")

```
_.pullAllBy(array, values, [iteratee=_.identity]) 
```

这个方法类似 `_.pullAll`，除了它接受一个 comparator 调用每一个数组元素的值。 comparator 会传入一个参数：(value)。

**注意:** 不同于 `_.differenceBy`，这个方法会改变数组。

### 参数

1.  array (Array)

    需要调整的数组

2.  values (Array)

    要移除的值

3.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (Array)

返回数组本身

### 示例

```
var array = [{ 'x': 1 }, { 'x': 2 }, { 'x': 3 }, { 'x': 1 }];

_.pullAllBy(array, [{ 'x': 1 }, { 'x': 3 }], 'x');
console.log(array);
// => [{ 'x': 2 }] 
```

# pullAt

## pullAt

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6334 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.pullat "See the npm package.")

```
_.pullAt(array, [indexes]) 
```

根据给的 `indexes` 移除对应的数组元素并返回被移除的元素。

**注意:** 不同于 `_.at`，这个方法会改变数组。

### 参数

1.  array (Array)

    需要调整的数组

2.  [indexes] (...(number|number[])

    indexes 可以是特殊的数组队列，或者个别的单个或多个参数

### 返回值 (Array)

返回被移除的元素数组

### 示例

```
var array = [5, 10, 15, 20];
var evens = _.pullAt(array, 1, 3);

console.log(array);
// => [5, 15]

console.log(evens);
// => [10, 20] 
```

# remove

## remove

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6366 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.remove "See the npm package.")

```
_.remove(array, [predicate=_.identity]) 
```

移除经过 `predicate` 处理为真值的元素，并返回被移除的元素。predicate 会传入 3 个参数：(value, index, array)

**注意:** Unlike `_.filter`，这个方法会改变数组。

### 参数

1.  array (Array)

    需要调整的数组

2.  [predicate=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (Array)

返回被移除的元素的数组

### 示例

```
var array = [1, 2, 3, 4];
var evens = _.remove(array, function(n) {
  return n % 2 == 0;
});

console.log(array);
// => [1, 3]

console.log(evens);
// => [2, 4] 
```

# slice

## slice

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6423 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.slice "See the npm package.")

```
_.slice(array, [start=0], [end=array.length]) 
```

创建一个裁剪后的数组，从 start 到 end 的位置，但不包括 end 本身的位置。

**注意:** 这个方法用于代替 [`Array#slice`](https://mdn.io/Array/slice) 来确保数组正确返回

### 参数

1.  array (Array)

    需要裁剪的数组

2.  [start=0] (number)

    开始位置

3.  [end=array.length] (number)

    结束位置

### 返回值 (Array)

返回裁剪后的数组

# sortedIndex

## sortedIndex

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6457 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.sortedindex "See the npm package.")

```
_.sortedIndex(array, value) 
```

使用二进制的方式检索来决定 value 应该插入在数组中位置。它的 index 应该尽可能的小以保证数组的排序。

### 参数

1.  array (Array)

    需要检索的已排序数组

2.  value (*)

    要评估位置的值

### 返回值 (number)

返回 value 应该在数组中插入的 index。

### 示例

```
_.sortedIndex([30, 50], 40);
// => 1

_.sortedIndex([4, 5], 4);
// => 0 
```

# sortedIndexBy

## sortedIndexBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6482 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.sortedindexby "See the npm package.")

```
_.sortedIndexBy(array, value, [iteratee=_.identity]) 
```

这个方法类似 `_.sortedIndex`，除了它接受一个 iteratee 调用每一个数组和值来计算排序。iteratee 会传入一个参数：(value)。

### 参数

1.  array (Array)

    需要检索的已排序数组

2.  value (*)

    要评估位置的值

3.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (number)

返回 value 应该在数组中插入的 index。

### 示例

```
var dict = { 'thirty': 30, 'forty': 40, 'fifty': 50 };

_.sortedIndexBy(['thirty', 'fifty'], 'forty', _.propertyOf(dict));
// => 1

// 使用了 `_.property` 回调结果
_.sortedIndexBy([{ 'x': 4 }, { 'x': 5 }], { 'x': 4 }, 'x');
// => 0 
```

# sortedIndexOf

## sortedIndexOf

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6500 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.sortedindexof "See the npm package.")

```
_.sortedIndexOf(array, value) 
```

这个方法类似 `_.indexOf`，除了它是执行二进制来检索已经排序的数组的。

### 参数

1.  array (Array)

    需要检索的数组

2.  value (*)

    要评估位置的值

### 返回值 (number)

返回匹配值的 index ，否则返回 `-1`.

### 示例

```
_.sortedIndexOf([1, 1, 2, 2], 2);
// => 2 
```

# sortedLastIndex

## sortedLastIndex

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6525 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.sortedlastindex "See the npm package.")

```
_.sortedLastIndex(array, value) 
```

这个方法类似 `_.sortedIndex`，除了它返回在 value 中尽可能大的 index 位置。

### 参数

1.  array (Array)

    需要检索的已排序数组

2.  value (*)

    要评估位置的值

### 返回值 (number)

返回 value 应该在数组中插入的 index。

### 示例

```
_.sortedLastIndex([4, 5], 4);
// => 1 
```

# sortedLastIndexBy

## sortedLastIndexBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6545 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.sortedlastindexby "See the npm package.")

```
_.sortedLastIndexBy(array, value, [iteratee=_.identity]) 
```

这个方法类似 `_.sortedLastIndex`，除了它接受一个 iteratee 调用每一个数组和值来计算排序。iteratee 会传入一个参数：(value)。

### 参数

1.  array (Array)

    需要检索的已排序数组

2.  value (*)

    要评估位置的值

3.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (number)

返回 value 应该在数组中插入的 index。

### 示例

```
// 使用了 `_.property` 的回调结果
_.sortedLastIndexBy([{ 'x': 4 }, { 'x': 5 }], { 'x': 4 }, 'x');
// => 1 
```

# sortedLastIndexOf

## sortedLastIndexOf

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6563 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.sortedlastindexof "See the npm package.")

```
_.sortedLastIndexOf(array, value) 
```

这个方法类似 `_.lastIndexOf`，除了它是执行二进制来检索已经排序的数组的。

### 参数

1.  array (Array)

    需要检索的数组

2.  value (*)

    要评估位置的值

### 返回值 (number)

返回匹配值的 index ，否则返回 -1.

### 示例

```
_.sortedLastIndexOf([1, 1, 2, 2], 2);
// => 3 
```

# sortedUniq

## sortedUniq

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6587 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.sorteduniq "See the npm package.")

```
_.sortedUniq(array) 
```

这个方法类似 `_.uniq`，除了它会排序并优化数组。

### 参数

1.  array (Array)

    要调整的数组

### 返回值 (Array)

返回一个不重复的数组

### 示例

```
_.sortedUniq([1, 1, 2]);
// => [1, 2] 
```

# sortedUniqBy

## sortedUniqBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6607 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.sorteduniqby "See the npm package.")

```
_.sortedUniqBy(array, [iteratee]) 
```

这个方法类似 `_.uniqBy`，除了它接受一个 iteratee 调用每一个数组和值来排序并优化数组。

### 参数

1.  array (Array)

    要调整的数组

2.  [iteratee] (Function)

    这个函数会处理每一个元素

### 返回值 (Array)

返回一个不重复的数组

### 示例

```
_.sortedUniqBy([1.1, 1.2, 2.3, 2.4], Math.floor);
// => [1.1, 2.3] 
```

# tail

## tail

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6626 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.tail "See the npm package.")

```
_.tail(array) 
```

获取数组中除了第一个元素的剩余数组

### 参数

1.  array (Array)

    要检索的数组

### 返回值 (Array)

返回数组中除了第一个元素的剩余数组

### 示例

```
_.tail([1, 2, 3]);
// => [2, 3] 
```

# take

## take

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6654 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.take "See the npm package.")

```
_.take(array, [n=1]) 
```

从数组的起始元素开始提取 N 个元素。

### 参数

1.  array (Array)

    需要处理的数组

2.  [n=1] (number)

    要提取的个数

### 返回值 (Array)

返回提取的元素数组

### 示例

```
_.take([1, 2, 3]);
// => [1]

_.take([1, 2, 3], 2);
// => [1, 2]

_.take([1, 2, 3], 5);
// => [1, 2, 3]

_.take([1, 2, 3], 0);
// => [] 
```

# takeRight

## takeRight

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6686 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.takeright "See the npm package.")

```
_.takeRight(array, [n=1]) 
```

从数组的结束元素开始提取 N 个数组

### 参数

1.  array (Array)

    需要处理的数组

2.  [n=1] (number)

    要提取的个数

### 返回值 (Array)

返回提取的元素数组

### 示例

```
_.takeRight([1, 2, 3]);
// => [3]

_.takeRight([1, 2, 3], 2);
// => [2, 3]

_.takeRight([1, 2, 3], 5);
// => [1, 2, 3]

_.takeRight([1, 2, 3], 0);
// => [] 
```

# takeRightWhile

## takeRightWhile

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6728 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.takerightwhile "See the npm package.")

```
_.takeRightWhile(array, [predicate=_.identity]) 
```

从数组的最右边开始提取数组，直到 `predicate` 返回假值。`predicate` 会传入三个参数：(value, index, array)。

### 参数

1.  array (Array)

    需要处理的数组

2.  [predicate=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (Array)

返回提取的元素数组

### 示例

```
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.takeRightWhile(users, function(o) { return !o.active; });
// => 结果:  ['fred', 'pebbles']

// 使用了 `_.matches` 的回调处理
_.takeRightWhile(users, { 'user': 'pebbles', 'active': false });
// => 结果:  ['pebbles']

// 使用了 `_.matchesProperty` 的回调处理
_.takeRightWhile(users, ['active', false]);
// => 结果:  ['fred', 'pebbles']

// 使用了 `_.property` 的回调处理
_.takeRightWhile(users, 'active');
// => [] 
```

# takeWhile

## takeWhile

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6766 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.takewhile "See the npm package.")

```
_.takeWhile(array, [predicate=_.identity]) 
```

从数组的开始提取数组，直到 predicate 返回假值。predicate 会传入三个参数：(value, index, array)。

### 参数

1.  array (Array)

    需要处理的数组

2.  [predicate=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (Array)

返回提取的元素数组

### 示例

```
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false},
  { 'user': 'pebbles', 'active': true }
];

_.takeWhile(users, function(o) { return !o.active; });
// => objects for ['barney', 'fred']

// 使用了 `_.matches` 的回调处理
_.takeWhile(users, { 'user': 'barney', 'active': false });
// =>结果: ['barney']

// 使用了 `_.matchesProperty` 的回调处理
_.takeWhile(users, ['active', false]);
// =>结果: ['barney', 'fred']

// 使用了 `_.property` 的回调处理
_.takeWhile(users, 'active');
// => [] 
```

# union

## union

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6785 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.union "See the npm package.")

```
_.union([arrays]) 
```

创建顺序排列的唯一值组成的数组。所有值经过 [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero) 等值比较。

### 参数

1.  [arrays] (...Array)

    需要处理的数组队列

### 返回值 (Array)

返回处理好的数组

### 示例

```
_.union([2, 1], [4, 2], [1, 2]);
// => [2, 1, 4] 
```

# unionBy

## unionBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6807 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.unionby "See the npm package.")

```
_.unionBy([arrays], [iteratee=_.identity]) 
```

这个方法类似 `_.union`，除了它接受一个 iteratee 调用每一个数组和值。iteratee 会传入一个参数：(value)。

### 参数

1.  [arrays] (...Array)

    需要处理的数组队列

2.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (Array)

返回处理好的数组

### 示例

```
_.unionBy([2.1, 1.2], [4.3, 2.4], Math.floor);
// => [2.1, 1.2, 4.3]

// 使用了 `_.property` 的回调结果
_.unionBy([{ 'x': 1 }], [{ 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }, { 'x': 2 }] 
```

# unionWith

## unionWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6833 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.unionwith "See the npm package.")

```
_.unionWith([arrays], [comparator]) 
```

这个方法类似 `_.union`， 除了它接受一个 comparator 调用每一个数组元素的值。 comparator 会传入 2 个参数：(arrVal, othVal)。

### 参数

1.  [arrays] (...Array)

    需要处理的数组队列

2.  [comparator] (Function)

    这个函数会处理每一个元素

### 返回值 (Array)

返回处理好的数组

### 示例

```
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.unionWith(objects, others, _.isEqual);
// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }] 
```

# uniq

## uniq

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6854 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.uniq "See the npm package.")

```
_.uniq(array) 
```

创建一个不重复的数组副本。使用了 [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero) 等值比较。只有首次出现的元素才会被保留。

### 参数

1.  array (Array)

    需要处理的数组

### 返回值 (Array)

返回不重复的数组

### 示例

```
_.uniq([2, 1, 2]);
// => [2, 1] 
```

# uniqBy

## uniqBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6878 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.uniqby "See the npm package.")

```
_.uniqBy(array, [iteratee=_.identity]) 
```

这个方法类似 `_.uniq`，除了它接受一个 iteratee 调用每一个数组和值来计算唯一性。iteratee 会传入一个参数：(value)。

### 参数

1.  array (Array)

    需要处理的数组

2.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (Array)

返回不重复的数组

### 示例

```
_.uniqBy([2.1, 1.2, 2.3], Math.floor);
// => [2.1, 1.2]

// 使用了 `_.property` 的回调结果
_.uniqBy([{ 'x': 1 }, { 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }, { 'x': 2 }] 
```

# uniqWith

## uniqWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6900 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.uniqwith "See the npm package.")

```
_.uniqWith(array, [comparator]) 
```

这个方法类似 `_.uniq`，除了它接受一个 `comparator` 来比较计算唯一性。 `comparator` 会传入 2 个参数：(arrVal, othVal)

### 参数

1.  array (Array)

    需要处理的数组

2.  [comparator] (Function)

    这个函数会处理每一个元素

### 返回值 (Array)

返回不重复的数组

### 示例

```
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 },  { 'x': 1, 'y': 2 }];

_.uniqWith(objects, _.isEqual);
// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }] 
```

# unzip

## unzip

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6922 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.unzip "See the npm package.")

```
_.unzip(array) 
```

这个方法类似 `_.zip`，除了它接收一个打包后的数组并且还原为打包前的状态。

### 参数

1.  array (Array)

    需要解包的已打包数组

### 返回值 (Array)

返回一个解包后的数组

### 示例

```
var zipped = _.zip(['fred', 'barney'], [30, 40], [true, false]);
// => [['fred', 30, true], ['barney', 40, false]]

_.unzip(zipped);
// => [['fred', 'barney'], [30, 40], [true, false]] 
```

# unzipWith

## unzipWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6955 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.unzipwith "See the npm package.")

```
_.unzipWith(array, [iteratee=_.identity]) 
```

这个方法类似 `_.unzip`，除了它接受一个 iteratee 来决定如何重组解包后的数组。iteratee 会传入 4 个参数：(accumulator, value, index, group)。每组的第一个元素作为初始化的值

### 参数

1.  array (Array)

    需要解包的已打包数组

2.  [iteratee=_.identity] (Function)

    决定如何重组解包后的元素

### 返回值 (Array)

返回一个解包后的数组

### 示例

```
var zipped = _.zip([1, 2], [10, 20], [100, 200]);
// => [[1, 10, 100], [2, 20, 200]]

_.unzipWith(zipped, _.add);
// => [3, 30, 300] 
```

# without

## without

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L6982 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.without "See the npm package.")

```
_.without(array, [values]) 
```

创建一个移除了所有提供的 values 的数组。使用了 [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero) 等值比较。

### 参数

1.  array (Array)

    要处理的数组

2.  [values] (...*)

    要排除的值

### 返回值 (Array)

返回一个处理好的新数组

### 示例

```
_.without([1, 2, 1, 3], 1, 2);
// => [3] 
```

# xor

## xor

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7001 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.xor "See the npm package.")

```
_.xor([arrays]) 
```

创建一个包含了所有唯一值的数组。使用了 [symmetric difference](https://en.wikipedia.org/wiki/Symmetric_difference) 等值比较。

### 参数

1.  [arrays] (...Array)

    要处理的数组

### 返回值 (Array)

包含了所有唯一值的新数组

### 示例

```
_.xor([2, 1], [4, 2]);
// => [1, 4] 
```

# xorBy

## xorBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7023 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.xorby "See the npm package.")

```
_.xorBy([arrays], [iteratee=_.identity]) 
```

这个方法类似 `_.xor`，除了它接受一个 iteratee 调用每一个数组和值。iteratee 会传入一个参数：(value)。

### 参数

1.  [arrays] (...Array)

    要处理的数组

2.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (Array)

包含了所有唯一值的新数组

### 示例

```
_.xorBy([2.1, 1.2], [4.3, 2.4], Math.floor);
// => [1.2, 4.3]

// 使用了 `_.property` 的回调结果
_.xorBy([{ 'x': 1 }], [{ 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 2 }] 
```

# xorWith

## xorWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7048 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.xorwith "See the npm package.")

```
_.xorWith([arrays], [comparator]) 
```

这个方法类似 `_.xor`，除了它接受一个 comparator 调用每一个数组元素的值。 comparator 会传入 2 个参数：(arrVal, othVal)。

### 参数

1.  [arrays] (...Array)

    要处理的数组

2.  [comparator] (Function)

    这个函数会处理每一个元素

### 返回值 (Array)

包含了所有唯一值的新数组

### 示例

```
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.xorWith(objects, others, _.isEqual);
// => [{ 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }] 
```

# zip

## zip

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7069 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.zip "See the npm package.")

```
_.zip([arrays]) 
```

创建一个打包所有元素后的数组。第一个元素包含所有提供数组的第一个元素，第二个包含所有提供数组的第二个元素，以此类推。

### 参数

1.  [arrays] (...Array)

    要处理的数组队列

### 返回值 (Array)

返回一个打包后的数组

### 示例

```
_.zip(['fred', 'barney'], [30, 40], [true, false]);
// => [['fred', 30, true], ['barney', 40, false]] 
```

# zipObject

## zipObject

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7085 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.zipobject "See the npm package.")

```
_.zipObject([props=[]], [values=[]]) 
```

这个方法类似 `_.fromPairs`，除了它接受 2 个数组，一个作为属性名，一个作为属性值。

### 参数

1.  [props=[]] (Array)

    属性名

2.  [values=[]] (Array)

    属性值

### 返回值 (Object)

返回一个新的对象

### 示例

```
_.zipObject(['a', 'b'], [1, 2]);
// => { 'a': 1, 'b': 2 } 
```

# zipObjectDeep

## zipObjectDeep

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7105 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.zipobjectdeep "See the npm package.")

```
_.zipObjectDeep([props=[]], [values=[]]) 
```

这个方法类似 `_.zipObject`，除了它支持属性路径。 This method is like `_.zipObject` except that it supports property paths.

### 参数

1.  [props=[]] (Array)

    属性名

2.  [values=[]] (Array)

    属性值

### 返回值 (Object)

返回新的对象

### 示例

```
_.zipObjectDeep(['a.b[0].c', 'a.b[1].d'], [1, 2]);
// => { 'a': { 'b': [{ 'c': 1 }, { 'd': 2 }] } } 
```

# zipWith

## zipWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7127 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.zipwith "See the npm package.")

```
_.zipWith([arrays]) 
```

这个方法类似 _.zip， 除了它接受一个 iteratee 决定如何重组值。 iteratee 会调用每一组元素。

### 参数

1.  [arrays] (...Array)

    要处理的数组队列

### 返回值 (Array)

返回一个打包后的数组

### 示例

```
_.zipWith([1, 2], [10, 20], [100, 200], function(a, b, c) {
  return a + b + c;
});
// => [111, 222] 
```