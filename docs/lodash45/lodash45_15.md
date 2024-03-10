# Util

# attempt

## attempt

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13095 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.attempt "See the npm package.")

```js
_.attempt(func) 
```

尝试调用函数，返回结果 或者 错误对象。 任何附加的参数都会在调用时传给函数。

### 参数

1.  func (Function)

    要调用的函数

### 返回值 (*)

返回函数结果或者错误对象

### 示例

```js
// 避免因为错误的选择器而抛出
var elements = _.attempt(function(selector) {
  return document.querySelectorAll(selector);
}, '>_>');

if (_.isError(elements)) {
  elements = [];
} 
```

# bindAll

## bindAll

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13128 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.bindall "See the npm package.")

```js
_.bindAll(object, methodNames) 
```

绑定对象的方法到对象本身，覆盖已存在的方法。

**注意:** 这个方法不会设置 "length" 属性到约束的函数。

### 参数

1.  object (Object)

    要绑定的对象

2.  methodNames (...(string|string[])

    要绑定的方法名 单独指定或指定在数组中。

### 返回值 (Object)

返回对象

### 示例

```js
var view = {
  'label': 'docs',
  'onClick': function() {
    console.log('clicked ' + this.label);
  }
};

_.bindAll(view, 'onClick');
jQuery(element).on('click', view.onClick);
// => logs 'clicked docs' when clicked 
```

# cond

## cond

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13161 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.cond "See the npm package.")

```js
_.cond(pairs) 
```

创建一个函数。 这个函数会遍历 `pairs`，并执行最先返回真值对应的函数，并绑定 `this` 及传入创建函数的参数。

### 参数

1.  pairs (Array)

    判断函数对

### 返回值 (Function)

返回新的函数

### 示例

```js
var func = _.cond([
  [_.matches({ 'a': 1 }),           _.constant('matches A')],
  [_.conforms({ 'b': _.isNumber }), _.constant('matches B')],
  [_.constant(true),                _.constant('no match')]
]);

func({ 'a': 1, 'b': 2 });
// => 输出：'matches A'

func({ 'a': 0, 'b': 1 });
// => 输出：'matches B'

func({ 'a': '1', 'b': '2' });
// => 输出：'no match' 
```

# conforms

## conforms

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13203 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.conforms "See the npm package.")

```js
_.conforms(source) 
```

创建一个函数。 这个函数会调用 `source` 的属性名对应的 `predicate` 与传入对象相对应属性名的值进行 `predicate` 处理。 如果都符合返回 `true`，否则返回 `false`

### 参数

1.  source (Object)

    包含 predicates 属性值的对象

### 返回值 (Function)

返回新的函数

### 示例

```js
var users = [
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 }
];

_.filter(users, _.conforms({ 'age': _.partial(_.gt, _, 38) }));
// => [{ 'user': 'fred', 'age': 40 }] 
```

# constant

## constant

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13223 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.constant "See the npm package.")

```js
_.constant(value) 
```

创建一个返回 `value` 的函数

### 参数

1.  value (*)

    要返回的值

### 返回值 (Function)

返回新的函数

### 示例

```js
var object = { 'user': 'fred' };
var getter = _.constant(object);

getter() === object;
// => true 
```

# flow

## flow

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13249 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.flow "See the npm package.")

```js
_.flow([funcs]) 
```

创建一个函数。 返回的结果是调用提供函数的结果，`this` 会绑定到创建函数。 每一个连续调用，传入的参数都是前一个函数返回的结果。

### 参数

1.  [funcs] (...(Function|Function[])

    要调用的函数

### 返回值 (Function)

返回新的函数

### 示例

```js
function square(n) {
  return n * n;
}

var addSquare = _.flow(_.add, square);
addSquare(1, 2);
// => 9 
```

# flowRight

## flowRight

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13269 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.flowright "See the npm package.")

```js
_.flowRight([funcs]) 
```

这个方法类似 `_.flow`，除了它调用函数的顺序是从右往左的。

### 参数

1.  [funcs] (...(Function|Function[])

    要调用的函数

### 返回值 (Function)

返回新的函数

### 示例

```js
function square(n) {
  return n * n;
}

var addSquare = _.flowRight(square, _.add);
addSquare(1, 2);
// => 9 
```

# identity

## identity

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13286 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.identity "See the npm package.")

```js
_.identity(value) 
```

这个方法返回首个提供的参数

### 参数

1.  value (*)

    任何值

### 返回值 (*)

返回 value

### 示例

```js
var object = { 'user': 'fred' };

_.identity(object) === object;
// => true 
```

# iteratee

## iteratee

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13319 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.iteratee "See the npm package.")

```js
_.iteratee([func=_.identity]) 
```

创建一个调用 `func` 的函数。 如果 `func` 是一个属性名，传入包含这个属性名的对象，回调返回对应属性名的值。 如果 `func` 是一个对象，传入的元素有相同的对象属性，回调返回 `true`。 其他情况返回 `false`。

### 参数

1.  [func=_.identity] (*)

    转换成 callback 的值

### 返回值 (Function)

返回 callback.

### 示例

```js
var users = [
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 }
];

// 创建一个自定义 iteratee
_.iteratee = _.wrap(_.iteratee, function(callback, func) {
  var p = /^(\S+)\s*([<>])\s*(\S+)$/.exec(func);
  return !p ? callback(func) : function(object) {
    return (p[2] == '>' ? object[p[1]] > p[3] : object[p[1]] < p[3]);
  };
});

_.filter(users, 'age > 36');
// => [{ 'user': 'fred', 'age': 40 }] 
```

# matches

## matches

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13344 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.matches "See the npm package.")

```js
_.matches(source) 
```

创建一个深比较的方法来比较给定的对象和 `source` 对象。 如果给定的对象拥有相同的属性值返回 `true`，否则返回 `false`

**注意:** 这个方法支持以 `_.isEqual` 的方式比较相同的值。

### 参数

1.  source (Object)

    要匹配的源对象

### 返回值 (Function)

返回新的函数

### 示例

```js
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

_.filter(users, _.matches({ 'age': 40, 'active': false }));
// => [{ 'user': 'fred', 'age': 40, 'active': false }] 
```

# matchesProperty

## matchesProperty

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13370 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.matchesproperty "See the npm package.")

```js
_.matchesProperty(path, srcValue) 
```

创建一个深比较的方法来比较给定对象的 `path` 的值是否是 `srcValue`。 如果是返回 `true`，否则返回 `false`

**注意:** 这个方法支持以 `_.isEqual` 的方式比较相同的值。

### 参数

1.  path (Array|string)

    给定对象的属性路径名

2.  srcValue (*)

    要匹配的值

### 返回值 (Function)

返回新的函数

### 示例

```js
var users = [
  { 'user': 'barney' },
  { 'user': 'fred' }
];

_.find(users, _.matchesProperty('user', 'fred'));
// => { 'user': 'fred' } 
```

# method

## method

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13397 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.method "See the npm package.")

```js
_.method(path, [args]) 
```

创建一个调用给定对象 `path` 上的函数。 任何附加的参数都会传入这个调用函数中。

### 参数

1.  path (Array|string)

    调用函数所在对象的路径

2.  [args] (...*)

    传递给调用函数的参数

### 返回值 (Function)

返回新的函数

### 示例

```js
var objects = [
  { 'a': { 'b': { 'c': _.constant(2) } } },
  { 'a': { 'b': { 'c': _.constant(1) } } }
];

_.map(objects, _.method('a.b.c'));
// => [2, 1]

_.invokeMap(_.sortBy(objects, _.method(['a', 'b', 'c'])), 'a.b.c');
// => [1, 2] 
```

# methodOf

## methodOf

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13425 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.methodof "See the npm package.")

```js
_.methodOf(object, [args]) 
```

反向版 `_.method`。 这个创建一个函数调用给定 `object` 的 `path` 上的方法， 任何附加的参数都会传入这个调用函数中。

### 参数

1.  object (Object)

    要检索的对象

2.  [args] (...*)

    传递给调用函数的参数

### 返回值 (Function)

返回新的函数

### 示例

```js
var array = _.times(3, _.constant),
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.methodOf(object));
// => [2, 0]

_.map([['a', '2'], ['c', '0']], _.methodOf(object));
// => [2, 0] 
```

# mixin

## mixin

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13464 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.mixin "See the npm package.")

```js
_.mixin([object=lodash], source, [options]) 
```

添加来源对象自身的所有可枚举函数属性到目标对象。 如果 `object` 是个函数，那么函数方法将被添加到原型链上。

**注意:** 使用 `_.runInContext` 来创建原始的 `lodash` 函数来避免修改造成的冲突。

### 参数

1.  [object=lodash] (Function|Object)

    目标对象

2.  source (Object)

    来源对象

3.  [options] (Object)

    选项对象

4.  [options.chain=true] (boolean)

    是否开启链式操作

### 返回值 (Function|Object)

返回对象

### 示例

```js
function vowels(string) {
  return _.filter(string, function(v) {
    return /[aeiou]/i.test(v);
  });
}

_.mixin({ 'vowels': vowels });
_.vowels('fred');
// => ['e']

_('fred').vowels().value();
// => ['e']

_.mixin({ 'vowels': vowels }, { 'chain': false });
_('fred').vowels();
// => ['e'] 
```

# noConflict

## noConflict

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13510 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.noconflict "See the npm package.")

```js
_.noConflict() 
```

释放 `_` 为原来的值，并返回一个 `lodash` 的引用

### 返回值 (Function)

返回 `lodash` 函数

### 示例

```js
var lodash = _.noConflict(); 
```

# noop

## noop

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13530 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.noop "See the npm package.")

```js
_.noop() 
```

无论传递什么参数，都返回 `undefined`。

### 示例

```js
var object = { 'user': 'fred' };

_.noop(object) === undefined;
// => true 
```

# nthArg

## nthArg

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13549 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.ntharg "See the npm package.")

```js
_.nthArg([n=0]) 
```

创建一个返回第 N 个参数的函数。

### 参数

1.  [n=0] (number)

    要返回参数的索引

### 返回值 (Function)

返回新的函数

### 示例

```js
var func = _.nthArg(1);

func('a', 'b', 'c');
// => 'b' 
```

# over

## over

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13571 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.over "See the npm package.")

```js
_.over(iteratees) 
```

创建一个传入提供的参数的函数并调用 `iteratees` 返回结果的函数。

### 参数

1.  iteratees (...(Function|Function[])

    要调用的 iteratees

### 返回值 (Function)

返回新的函数

### 示例

```js
var func = _.over(Math.max, Math.min);

func(1, 2, 3, 4);
// => [4, 1] 
```

# overEvery

## overEvery

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13594 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.overevery "See the npm package.")

```js
_.overEvery(predicates) 
```

创建一个传入提供的参数的函数并调用 `iteratees` 判断是否 全部 都为真值的函数。

### 参数

1.  predicates (...(Function|Function[])

    要调用的 predicates

### 返回值 (Function)

返回新的函数

### 示例

```js
var func = _.overEvery(Boolean, isFinite);

func('1');
// => true

func(null);
// => false

func(NaN);
// => false 
```

# overSome

## overSome

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13617 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.oversome "See the npm package.")

```js
_.overSome(predicates) 
```

创建一个传入提供的参数的函数并调用 `iteratees` 判断是否 存在 有真值的函数。

### 参数

1.  predicates (...(Function|Function[])

    要调用的 predicates

### 返回值 (Function)

返回新的函数

### 示例

```js
var func = _.overSome(Boolean, isFinite);

func('1');
// => true

func(null);
// => true

func(NaN);
// => false 
```

# property

## property

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13640 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.property "See the npm package.")

```js
_.property(path) 
```

创建一个返回给定对象的 `path` 的值的函数。

### 参数

1.  path (Array|string)

    要得到值的属性路径

### 返回值 (Function)

返回新的函数

### 示例

```js
var objects = [
  { 'a': { 'b': { 'c': 2 } } },
  { 'a': { 'b': { 'c': 1 } } }
];

_.map(objects, _.property('a.b.c'));
// => [2, 1]

_.map(_.sortBy(objects, _.property(['a', 'b', 'c'])), 'a.b.c');
// => [1, 2] 
```

# propertyOf

## propertyOf

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13664 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.propertyof "See the npm package.")

```js
_.propertyOf(object) 
```

反向版 `_.property`。 这个方法创建的函数返回给定 path 在对象上的值。

### 参数

1.  object (Object)

    要检索的对象

### 返回值 (Function)

返回新的函数

### 示例

```js
var array = [0, 1, 2],
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.propertyOf(object));
// => [2, 0]

_.map([['a', '2'], ['c', '0']], _.propertyOf(object));
// => [2, 0] 
```

# range

## range

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13708 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.range "See the npm package.")

```js
_.range([start=0], end, [step=1]) 
```

创建一个包含从 `start` 到 `end`，但不包含 `end` 本身范围数字的数组。 如果 `start` 是负数，而 `end` 或 `step` 没有指定，那么 `step` 从 `-1` 为开始。 如果 `end` 没有指定，`start` 设置为 `0`。 如果 `end` 小于 `start`，会创建一个空数组，除非指定了 `step`。

**注意:** JavaScript 遵循 IEEE-754 标准处理无法预料的浮点数结果。

### 参数

1.  [start=0] (number)

    开始的范围

2.  end (number)

    结束的范围

3.  [step=1] (number)

    范围的增量 或者 减量

### 返回值 (Array)

返回范围内数字组成的新数组

### 示例

```js
_.range(4);
// => [0, 1, 2, 3]

_.range(-4);
// => [0, -1, -2, -3]

_.range(1, 5);
// => [1, 2, 3, 4]

_.range(0, 20, 5);
// => [0, 5, 10, 15]

_.range(0, -4, -1);
// => [0, -1, -2, -3]

_.range(1, 4, 0);
// => [1, 1, 1]

_.range(0);
// => [] 
```

# rangeRight

## rangeRight

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13744 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.rangeright "See the npm package.")

```js
_.rangeRight([start=0], end, [step=1]) 
```

这个方法类似 `_.range`， 除了它是降序生成值的。

### 参数

1.  [start=0] (number)

    开始的范围

2.  end (number)

    结束的范围

3.  [step=1] (number)

    范围的增量 或者 减量

### 返回值 (Array)

返回范围内数字组成的新数组

### 示例

```js
_.rangeRight(4);
// => [3, 2, 1, 0]

_.rangeRight(-4);
// => [-3, -2, -1, 0]

_.rangeRight(1, 5);
// => [4, 3, 2, 1]

_.rangeRight(0, 20, 5);
// => [15, 10, 5, 0]

_.rangeRight(0, -4, -1);
// => [-3, -2, -1, 0]

_.rangeRight(1, 4, 0);
// => [1, 1, 1]

_.rangeRight(0);
// => [] 
```

# runInContext

## runInContext

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L1300 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.runincontext "See the npm package.")

```js
_.runInContext([context=root]) 
```

创建一个给定上下文对象的原始的 `lodash` 函数。

### 参数

1.  [context=root] (Object)

    上下文对象

### 返回值 (Function)

返回新的 `lodash` 对象

### 示例

```js
_.mixin({ 'foo': _.constant('foo') });

var lodash = _.runInContext();
lodash.mixin({ 'bar': lodash.constant('bar') });

_.isFunction(_.foo);
// => true
_.isFunction(_.bar);
// => false

lodash.isFunction(lodash.foo);
// => false
lodash.isFunction(lodash.bar);
// => true

// 使用 `context` 模拟 `Date#getTime` 调用 `_.now`
var mock = _.runInContext({
  'Date': function() {
    return { 'getTime': getTimeMock };
  }
});

// 或者在 Node.js 中创建一个更高级的 `defer`
var defer = _.runInContext({ 'setTimeout': setImmediate }).defer; 
```

# times

## times

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13764 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.times "See the npm package.")

```js
_.times(n, [iteratee=_.identity]) 
```

调用 iteratee N 次，每次调用返回的结果存入到数组中。 iteratee 会传入 1 个参数：(index)。

### 参数

1.  n (number)

    要调用 `iteratee` 的次数

2.  [iteratee=_.identity] (Function)

    这个函数会处理每一个元素

### 返回值 (Array)

返回调用结果的数组

### 示例

```js
_.times(3, String);
// => ['0', '1', '2']

 _.times(4, _.constant(true));
// => [true, true, true, true] 
```

# toPath

## toPath

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13807 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.topath "See the npm package.")

```js
_.toPath(value) 
```

创建 `value` 为属性路径的数组

### 参数

1.  value (*)

    要转换的值

### 返回值 (Array)

返回包含属性路径的数组

### 示例

```js
_.toPath('a.b.c');
// => ['a', 'b', 'c']

_.toPath('a[0].b.c');
// => ['a', '0', 'b', 'c']

var path = ['a', 'b', 'c'],
    newPath = _.toPath(path);

console.log(newPath);
// => ['a', 'b', 'c']

console.log(path === newPath);
// => false 
```

# uniqueId

## uniqueId

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13828 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.uniqueid "See the npm package.")

```js
_.uniqueId([prefix]) 
```

创建唯一 ID。 如果提供了 `prefix`，会被添加到 ID 前缀上。

### 参数

1.  [prefix] (string)

    要添加到 ID 前缀的值

### 返回值 (string)

返回唯一 ID

### 示例

```js
_.uniqueId('contact_');
// => 'contact_104'

_.uniqueId();
// => '105' 
```