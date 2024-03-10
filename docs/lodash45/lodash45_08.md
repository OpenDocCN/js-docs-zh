# Math

# add

## add

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13849 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.add "See the npm package.")

```
_.add(augend, addend) 
```

相加两个数

### 参数

1.  augend (number)

    相加的第一个数

2.  addend (number)

    相加的第二个数

### 返回值 (number)

返回总和

### 示例

```
_.add(6, 4);
// => 10 
```

# ceil

## ceil

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13883 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.ceil "See the npm package.")

```
_.ceil(number, [precision=0]) 
```

根据 `precision` 向上舍入 `number`。

### 参数

1.  number (number)

    要向上舍入的值

2.  [precision=0] (number)

    精度

### 返回值 (number)

返回向上舍入的结果

### 示例

```
_.ceil(4.006);
// => 5

_.ceil(6.004, 2);
// => 6.01

_.ceil(6040, -2);
// => 6100 
```

# floor

## floor

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13905 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.floor "See the npm package.")

```
_.floor(number, [precision=0]) 
```

根据 `precision` 向下保留 `number`。

### 参数

1.  number (number)

    要向下保留的数

2.  [precision=0] (number)

    精度

### 返回值 (number)

返回向下保留的结果

### 示例

```
_.floor(4.006);
// => 4

_.floor(0.046, 2);
// => 0.04

_.floor(4060, -2);
// => 4000 
```

# max

## max

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13924 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.max "See the npm package.")

```
_.max(array) 
```

计算 `array` 中最大的值。 如果 `array` 是 空的或者假值将会返回 undefined。

### 参数

1.  array (Array)

    要计算的数组

### 返回值 (*)

返回最大的值

### 示例

```
_.max([4, 2, 8, 6]);
// => 8

_.max([]);
// => undefined 
```

# maxBy

## maxBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13952 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.maxby "See the npm package.")

```
_.maxBy(array, [iteratee=_.identity]) 
```

这个方法类似 `_.max` 除了它接受 `iteratee` 调用每一个元素，根据返回的 value 决定排序准则。 iteratee 会传入 1 个参数：(value)。

### 参数

1.  array (Array)

    要遍历的数组

2.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (*)

返回最大值

### 示例

```
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.maxBy(objects, function(o) { return o.n; });
// => { 'n': 2 }

// 使用了 `_.property` iteratee 的回调结果
_.maxBy(objects, 'n');
// => { 'n': 2 } 
```

# mean

## mean

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13971 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.mean "See the npm package.")

```
_.mean(array) 
```

计算 `array` 的平均值。

### 参数

1.  array (Array)

    要遍历的数组

### 返回值 (number)

返回平均值

### 示例

```
_.mean([4, 2, 8, 6]);
// => 5 
```

# min

## min

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13991 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.min "See the npm package.")

```
_.min(array) 
```

计算 array 中最小的值。 如果 array 是 空的或者假值将会返回 undefined。

### 参数

1.  array (Array)

    要计算的数组

### 返回值 (*)

返回最小值

### 示例

```
_.min([4, 2, 8, 6]);
// => 2

_.min([]);
// => undefined 
```

# minBy

## minBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L14018 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.minby "See the npm package.")

```
_.minBy(array, [iteratee=_.identity]) 
```

这个方法类似 `_.min`。 除了它接受 iteratee 调用每一个元素，根据返回的 value 决定排序准则。 iteratee 会传入 1 个参数：(value)。

### 参数

1.  array (Array)

    要遍历的数组

2.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (*)

返回最小值

### 示例

```
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.minBy(objects, function(o) { return o.n; });
// => { 'n': 1 }

// 使用了 `_.property` iteratee 的回调结果
_.minBy(objects, 'n');
// => { 'n': 1 } 
```

# round

## round

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L14044 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.round "See the npm package.")

```
_.round(number, [precision=0]) 
```

根据 precision 四舍五入 number。

### 参数

1.  number (number)

    要四舍五入的值

2.  [precision=0] (number)

    精度

### 返回值 (number)

返回四舍五入的结果

### 示例

```
_.round(4.006);
// => 4

_.round(4.006, 2);
// => 4.01

_.round(4060, -2);
// => 4100 
```

# subtract

## subtract

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L14060 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.subtract "See the npm package.")

```
_.subtract(minuend, subtrahend) 
```

两双相减

### 参数

1.  minuend (number)

    相减的第一个数

2.  subtrahend (number)

    相减的第二个数

### 返回值 (number)

返回结果

### 示例

```
_.subtract(6, 4);
// => 2 
```

# sum

## sum

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L14087 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.sum "See the npm package.")

```
_.sum(array) 
```

计算 `array` 中值的总和

### 参数

1.  array (Array)

    要遍历的数组

### 返回值 (number)

返回总和

### 示例

```
_.sum([4, 2, 8, 6]);
// => 20 
```

# sumBy

## sumBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L14115 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.sumby "See the npm package.")

```
_.sumBy(array, [iteratee=_.identity]) 
```

这个方法类似 `_.sum`。 除了它接受 iteratee 调用每一个元素，根据返回的 value 决定如何计算。 iteratee 会传入 1 个参数：(value)。

### 参数

1.  array (Array)

    要遍历的数组

2.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (number)

返回总和

### 示例

```
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.sumBy(objects, function(o) { return o.n; });
// => 20

// 使用了 `_.property` 的回调结果
_.sumBy(objects, 'n');
// => 20 
```