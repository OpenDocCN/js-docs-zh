# Seq

# Seq

# _

## _

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L1494 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash._ "See the npm package.")

```
_(value) 
```

创建一个经 `lodash` 包装后的对象会启用隐式链。返回的数组、集合、方法相互之间能够链式调用。 检索唯一值或返回原始值会自动解除链条并返回计算后的值，否则需要调用 `_#value` 方法解除链(即获得计算结果)。

显式链式调用，在任何情况下需要先用 `_#value` 解除链后，才能使用 `_.chain` 开启。

链式方法是惰性计算的，直到隐式或者显式调用了 `_#value` 才会执行计算。

惰性计算接受几种支持 shortcut fusion 的方法， shortcut fusion 是一种通过合并链式 iteratee 调用从而大大降低迭代的次数以提高执行性能的方式。 部分链有资格 shortcut fusion，如果它至少有超过二百个元素的数组和任何只接受一个参数的 iteratees。 触发的方式是任何一个 shortcut fusion 有了变化。

链式方法支持定制版本，只要 `_#value` 包含或者间接包含在版本中。

除了 lodash 的自身方法，包装后的对象还支持 `Array` 的 `String` 的方法。

支持 `Array` 的方法: `concat`, `join`, `pop`, `push`, `shift`, `sort`, `splice`, 以及 `unshift`

支持 `String` 的方法: `replace` 以及 `split`

支持 shortcut fusion 的方法: `at`, `compact`, `drop`, `dropRight`, `dropWhile`, `filter`, `find`, `findLast`, `head`, `initial`, `last`, `map`, `reject`, `reverse`, `slice`, `tail`, `take`, `takeRight`, `takeRightWhile`, `takeWhile`, 以及 `toArray`

默认不支持 链式调用 的方法: `add`, `attempt`, `camelCase`, `capitalize`, `ceil`, `clamp`, `clone`, `cloneDeep`, `cloneDeepWith`, `cloneWith`, `deburr`, `endsWith`, `eq`, `escape`, `escapeRegExp`, `every`, `find`, `findIndex`, `findKey`, `findLast`, `findLastIndex`, `findLastKey`, `floor`, `forEach`, `forEachRight`, `forIn`, `forInRight`, `forOwn`, `forOwnRight`, `get`, `gt`, `gte`, `has`, `hasIn`, `head`, `identity`, `includes`, `indexOf`, `inRange`, `invoke`, `isArguments`, `isArray`, `isArrayBuffer`, `isArrayLike`, `isArrayLikeObject`, `isBoolean`, `isBuffer`, `isDate`, `isElement`, `isEmpty`, `isEqual`, `isEqualWith`, `isError`, `isFinite`, `isFunction`, `isInteger`, `isLength`, `isMap`, `isMatch`, `isMatchWith`, `isNaN`, `isNative`, `isNil`, `isNull`, `isNumber`, `isObject`, `isObjectLike`, `isPlainObject`, `isRegExp`, `isSafeInteger`, `isSet`, `isString`, `isUndefined`, `isTypedArray`, `isWeakMap`, `isWeakSet`, `join`, `kebabCase`, `last`, `lastIndexOf`, `lowerCase`, `lowerFirst`, `lt`, `lte`, `max`, `maxBy`, `mean`, `min`, `minBy`, `noConflict`, `noop`, `now`, `pad`, `padEnd`, `padStart`, `parseInt`, `pop`, `random`, `reduce`, `reduceRight`, `repeat`, `result`, `round`, `runInContext`, `sample`, `shift`, `size`, `snakeCase`, `some`, `sortedIndex`, `sortedIndexBy`, `sortedLastIndex`, `sortedLastIndexBy`, `startCase`, `startsWith`, `subtract`, `sum`, `sumBy`, `template`, `times`, `toLower`, `toInteger`, `toLength`, `toNumber`, `toSafeInteger`, `toString`, `toUpper`, `trim`, `trimEnd`, `trimStart`, `truncate`, `unescape`, `uniqueId`, `upperCase`, `upperFirst`, `value`, 以及 `words`

支持 链式调用 的方法: `after`, `ary`, `assign`, `assignIn`, `assignInWith`, `assignWith`, `at`, `before`, `bind`, `bindAll`, `bindKey`, `castArray`, `chain`, `chunk`, `commit`, `compact`, `concat`, `conforms`, `constant`, `countBy`, `create`, `curry`, `debounce`, `defaults`, `defaultsDeep`, `defer`, `delay`, `difference`, `differenceBy`, `differenceWith`, `drop`, `dropRight`, `dropRightWhile`, `dropWhile`, `fill`, `filter`, `flatten`, `flattenDeep`, `flattenDepth`, `flip`, `flow`, `flowRight`, `fromPairs`, `functions`, `functionsIn`, `groupBy`, `initial`, `intersection`, `intersectionBy`, `intersectionWith`, `invert`, `invertBy`, `invokeMap`, `iteratee`, `keyBy`, `keys`, `keysIn`, `map`, `mapKeys`, `mapValues`, `matches`, `matchesProperty`, `memoize`, `merge`, `mergeWith`, `method`, `methodOf`, `mixin`, `negate`, `nthArg`, `omit`, `omitBy`, `once`, `orderBy`, `over`, `overArgs`, `overEvery`, `overSome`, `partial`, `partialRight`, `partition`, `pick`, `pickBy`, `plant`, `property`, `propertyOf`, `pull`, `pullAll`, `pullAllBy`, `pullAt`, `push`, `range`, `rangeRight`, `rearg`, `reject`, `remove`, `rest`, `reverse`, `sampleSize`, `set`, `setWith`, `shuffle`, `slice`, `sort`, `sortBy`, `splice`, `spread`, `tail`, `take`, `takeRight`, `takeRightWhile`, `takeWhile`, `tap`, `throttle`, `thru`, `toArray`, `toPairs`, `toPairsIn`, `toPath`, `toPlainObject`, `transform`, `unary`, `union`, `unionBy`, `unionWith`, `uniq`, `uniqBy`, `uniqWith`, `unset`, `unshift`, `unzip`, `unzipWith`, `values`, `valuesIn`, `without`, `wrap`, `xor`, `xorBy`, `xorWith`, `zip`, `zipObject`, `zipObjectDeep`, 以及 `zipWith`

### 参数

1.  value (*)

    需要被包装为 `lodash` 实例的值.

### 返回值 (Object)

返回 `lodash` 包装后的实例

### 示例

```
function square(n) {
  return n * n;
}

var wrapped = _([1, 2, 3]);

// 返回未包装的值
wrapped.reduce(_.add);
// => 6

// 返回链式包装的值
var squares = wrapped.map(square);

_.isArray(squares);
// => false

_.isArray(squares.value());
// => true 
```

# chain

## chain

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7163 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.chain "See the npm package.")

```
_.chain(value) 
```

创建一个经 `lodash` 包装的对象以启用显式链模式，要解除链必须使用 `_#value` 方法。

### 参数

1.  value (*)

    要包装的值

### 返回值 (Object)

返回 `lodash` 包装的实例

### 示例

```
var users = [
  { 'user': 'barney',  'age': 36 },
  { 'user': 'fred',    'age': 40 },
  { 'user': 'pebbles', 'age': 1 }
];

var youngest = _
  .chain(users)
  .sortBy('age')
  .map(function(o) {
    return o.user + ' is ' + o.age;
  })
  .head()
  .value();
// => 'pebbles is 1' 
```

# prototype.at

## prototype.at

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7238 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.prototype.at "See the npm package.")

```
_.prototype.at([paths]) 
```

这个方法是 `_.at` 的包装版本

### 参数

1.  [paths] (...(string|string[])

    要选择元素的属性路径， 单独指定或者数组

### 返回值 (Object)

返回 `lodash` 的包装实例

### 示例

```
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

_(object).at(['a[0].b.c', 'a[1]']).value();
// => [3, 4]

_(['a', 'b', 'c']).at(0, 2).value();
// => ['a', 'c'] 
```

# prototype.chain

## prototype.chain

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7286 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.prototype.chain "See the npm package.")

```
_.prototype.chain() 
```

开启包装对象的显式链。

### 返回值 (Object)

返回 `lodash` 的包装实例

### 示例

```
var users = [
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 }
];

// 不启用显式链
_(users).head();
// => { 'user': 'barney', 'age': 36 }

// 启用显式链
_(users)
  .chain()
  .head()
  .pick('user')
  .value();
// => { 'user': 'barney' } 
```

# prototype.commit

## prototype.commit

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7315 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.prototype.commit "See the npm package.")

```
_.prototype.commit() 
```

执行链式队列并返回结果

### 返回值 (Object)

返回 `lodash` 的包装实例

### 示例

```
var array = [1, 2];
var wrapped = _(array).push(3);

console.log(array);
// => [1, 2]

wrapped = wrapped.commit();
console.log(array);
// => [1, 2, 3]

wrapped.last();
// => 3

console.log(array);
// => [1, 2, 3] 
```

# prototype.next

## prototype.next

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7361 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.prototype.next "See the npm package.")

```
_.prototype.next() 
```

获得包装对象的下一个值，遵循 [iterator 协议](https://mdn.io/iteration_protocols#iterator)。

### 返回值 (Object)

返回下一个 iterator 值

### 示例

```
var wrapped = _([1, 2]);

wrapped.next();
// => { 'done': false, 'value': 1 }

wrapped.next();
// => { 'done': false, 'value': 2 }

wrapped.next();
// => { 'done': true, 'value': undefined } 
```

# prototype.plant

## prototype.plant

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7415 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.prototype.plant "See the npm package.")

```
_.prototype.plant(value) 
```

创建一个链式队列的拷贝，传入的值作为链式队列的值。

### 参数

1.  value (*)

    替换原值的值

### 返回值 (Object)

返回 `lodash` 的包装实例

### 示例

```
function square(n) {
  return n * n;
}

var wrapped = _([1, 2]).map(square);
var other = wrapped.plant([3, 4]);

other.value();
// => [9, 16]

wrapped.value();
// => [1, 4] 
```

# prototype.Symbol.iterator

## prototype.Symbol.iterator

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7388 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.prototype.symbol.iterator "See the npm package.")

```
_.prototype.Symbol.iterator() 
```

启用包装对象为 iterable。

### 返回值 (Object)

返回包装对象

### 示例

```
var wrapped = _([1, 2]);

wrapped[Symbol.iterator]() === wrapped;
// => true

Array.from(wrapped);
// => [1, 2] 
```

# prototype.value run, toJSON, valueOf

## prototype.value run, toJSON, valueOf

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7481 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.prototype.value "See the npm package.")

```
_.prototype.value() 
```

执行链式队列并提取解链后的值

### 返回值 (*)

返回解链后的值

### 示例

```
_([1, 2, 3]).value();
// => [1, 2, 3] 
```

# tap

## tap

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7190 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.tap "See the npm package.")

```
_.tap(value, interceptor) 
```

这个方法调用一个 `interceptor` 并返回 `value`。`interceptor` 传入一个参数：(value) 目的是 `进入` 链的中间以便执行操作。

### 参数

1.  value (*)

    提供给 `interceptor` 的值

2.  interceptor (Function)

    调用函数

### 返回值 (*)

返回 `value`

### 示例

```
_([1, 2, 3])
 .tap(function(array) {
   // 改变传入的数组
   array.pop();
 })
 .reverse()
 .value();
// => [2, 1] 
```

# thru

## thru

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7215 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.thru "See the npm package.")

```
_.thru(value, interceptor) 
```

这个方法类似 `_.tap`， 除了它返回 `interceptor` 的返回结果

### 参数

1.  value (*)

    提供给 `interceptor` 的值

2.  interceptor (Function)

    调用函数

### 返回值 (*)

返回 `interceptor` 的返回结果

### 示例

```
_('  abc  ')
 .chain()
 .trim()
 .thru(function(value) {
   return [value];
 })
 .value();
// => ['abc'] 
```

# wrapperFlatMap

## wrapperFlatMap

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L7336 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.wrapperflatmap "See the npm package.")

```
_.wrapperFlatMap([iteratee=_.identity]) 
```

这个方法是 `_.flatMap` 的包装版本。

### 参数

1.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (Object)

返回 `lodash` 的包装实例

### 示例

```
function duplicate(n) {
  return [n, n];
}

_([1, 2]).flatMap(duplicate).value();
// => [1, 1, 2, 2] 
```