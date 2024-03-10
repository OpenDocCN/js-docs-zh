# Number

# clamp

## clamp

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11907 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.clamp "See the npm package.")

```
_.clamp(number, [min], max) 
```

返回限制在 `min` 和 `max` 之间的值

### 参数

1.  number (number)

    被限制的值

2.  [min] (number)

    最小绝对值

3.  max (number)

    最大绝对值

### 返回值 (number)

[min, max] 中的一个

### 示例

```
_.clamp(-10, -5, 5);
// => -5

_.clamp(10, -5, 5);
// => 5 
```

# inRange

## inRange

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11958 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.inrange "See the npm package.")

```
_.inRange(number, [start=0], end) 
```

检查 `n` 是否在 `start` 与 `end` 之间，但不包括 `end`。 如果 `end` 没有指定，那么 `start` 设置为 0。 如果 `start` 大于 `end`，那么参数会交换以便支持负范围。

### 参数

1.  number (number)

    要检查的值

2.  [start=0] (number)

    开始范围

3.  end (number)

    结束范围

### 返回值 (boolean)

如果值在范围内返回`true`，否则返回 `false`

### 示例

```
_.inRange(3, 2, 4);
// => true

_.inRange(4, 8);
// => true

_.inRange(4, 2);
// => false

_.inRange(2, 2);
// => false

_.inRange(1.2, 2);
// => true

_.inRange(5.2, 4);
// => false

_.inRange(-3, -2, -6);
// => true 
```

# random

## random

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11998 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.random "See the npm package.")

```
_.random([min=0], [max=1], [floating]) 
```

产生一个包括 `min` 与 `max` 之间的数。 如果只提供一个参数返回一个 0 到提供数之间的数。 如果 `floating` 设为 true，或者 `min` 或 `max` 是浮点数，结果返回浮点数。

**注意:** JavaScript 遵循 IEEE-754 标准处理无法预料的浮点数结果。

### 参数

1.  [min=0] (number)

    最小值

2.  [max=1] (number)

    最大值

3.  [floating] (boolean)

    是否返回浮点数

### 返回值 (number)

返回随机数

### 示例

```
_.random(0, 5);
// =>  0 和 5 之间的数

_.random(5);
// => 同样是 0 和 5 之间的数

_.random(5, true);
// => 0 和 5 之间的浮点数

_.random(1.2, 5.2);
// =>  1.2 和 5.2 之间的浮点数 
```