# Object

# assign

## assign

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10703 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.assign "See the npm package.")

```
_.assign(object, [sources])
_.assign(object, [sources]) 
```

分配来源对象的可枚举属性到目标对象上。 来源对象的应用规则是从左到右，随后的下一个对象的属性会覆盖上一个对象的属性。

**注意:** 这方法会改变源对象，参考自 [`Object.assign`](https://mdn.io/Object/assign).

### 参数

1.  object (Object)

    目标对象

2.  [sources] (...Object)

    来源对象

### 返回值 (Object)

返回对象

### 示例

```
function Foo() {
  this.c = 3;
}

function Bar() {
  this.e = 5;
}

Foo.prototype.d = 4;
Bar.prototype.f = 6;

_.assign({ 'a': 1 }, new Foo, new Bar);
// => { 'a': 1, 'c': 3, 'e': 5 } 
```

# assignIn extend

## assignIn extend

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10736 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.assignin "See the npm package.")

```
_.assignIn(object, [sources]) 
```

这个方法类似 `_.assign`。 除了它会遍历并继承来源对象的属性。

**注意:** 这方法会改变源对象

### 参数

1.  object (Object)

    目标对象

2.  [sources] (...Object)

    来源对象

### 返回值 (Object)

返回对象

### 示例

```
function Foo() {
  this.b = 2;
}

function Bar() {
  this.d = 4;
}

Foo.prototype.c = 3;
Bar.prototype.e = 5;

_.assignIn({ 'a': 1 }, new Foo, new Bar);
// => { 'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5 } 
```

# assignInWith extendWith

## assignInWith extendWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10767 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.assigninwith "See the npm package.")

```
_.assignInWith(object, sources, [customizer]) 
```

这个方法类似 `_.assignIn`。 除了它接受一个 customizer`决定如何分配值。 如果`customizer`返回`undefined`将会由分配处理方法代替。`customizer` 会传入 5 个参数：(objValue, srcValue, key, object, source)。

**注意:** 这方法会改变源对象

### 参数

1.  object (Object)

    目标对象

2.  sources (...Object)

    来源对象

3.  [customizer] (Function)

    这个函数决定分配的值

### 返回值 (Object)

返回对象

### 示例

```
function customizer(objValue, srcValue) {
  return _.isUndefined(objValue) ? srcValue : objValue;
}

var defaults = _.partialRight(_.assignInWith, customizer);

defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 } 
```

# assignWith

## assignWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10797 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.assignwith "See the npm package.")

```
_.assignWith(object, sources, [customizer]) 
```

这个方法类似 `_.assign`。 除了它接受一个 customizer`决定如何分配值。 如果`customizer`返回`undefined`将会由分配处理方法代替。`customizer` 会传入 5 个参数：(objValue, srcValue, key, object, source)。

**注意:** 这方法会改变源对象

### 参数

1.  object (Object)

    目标对象

2.  sources (...Object)

    来源对象

3.  [customizer] (Function)

    这个函数决定分配的值

### 返回值 (Object)

返回对象

### 示例

```
function customizer(objValue, srcValue) {
  return _.isUndefined(objValue) ? srcValue : objValue;
}

var defaults = _.partialRight(_.assignWith, customizer);

defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 } 
```

# at

## at

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10820 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.at "See the npm package.")

```
_.at(object, [paths]) 
```

根据 `object` 的路径获取值为数组。

### 参数

1.  object (Object)

    要遍历的对象

2.  [paths] (...(string|string[])

    要获取的对象的元素路径，单独指定或者指定在数组中

### 返回值 (Array)

返回选中值的数组

### 示例

```
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

_.at(object, ['a[0].b.c', 'a[1]']);
// => [3, 4]

_.at(['a', 'b', 'c'], 0, 2);
// => ['a', 'c'] 
```

# create

## create

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10856 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.create "See the npm package.")

```
_.create(prototype, [properties]) 
```

创建一个继承 `prototype` 的对象。 如果提供了 `properties`，它的可枚举属性会被分配到创建的对象上。

### 参数

1.  prototype (Object)

    要继承的对象

2.  [properties] (Object)

    待分配的属性

### 返回值 (Object)

返回新对象

### 示例

```
function Shape() {
  this.x = 0;
  this.y = 0;
}

function Circle() {
  Shape.call(this);
}

Circle.prototype = _.create(Shape.prototype, {
  'constructor': Circle
});

var circle = new Circle;
circle instanceof Circle;
// => true

circle instanceof Shape;
// => true 
```

# defaults

## defaults

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10879 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.defaults "See the npm package.")

```
_.defaults(object, [sources]) 
```

分配来源对象的可枚举属性到目标对象所有解析为 `undefined` 的属性上。 来源对象从左到右应用。 一旦设置了相同属性的值，后续的将被忽略掉。

**注意:** 这方法会改变源对象

### 参数

1.  object (Object)

    目标对象

2.  [sources] (...Object)

    来源对象

### 返回值 (Object)

返回对象

### 示例

```
_.defaults({ 'user': 'barney' }, { 'age': 36 }, { 'user': 'fred' });
// => { 'user': 'barney', 'age': 36 } 
```

# defaultsDeep

## defaultsDeep

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10901 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.defaultsdeep "See the npm package.")

```
_.defaultsDeep(object, [sources]) 
```

这个方法类似 `_.defaults`，除了它会递归分配默认属性。

**注意:** 这方法会改变源对象

### 参数

1.  object (Object)

    目标对象

2.  [sources] (...Object)

    来源对象

### 返回值 (Object)

返回对象

### 示例

```
_.defaultsDeep({ 'user': { 'name': 'barney' } }, { 'user': { 'name': 'fred', 'age': 36 } });
// => { 'user': { 'name': 'barney', 'age': 36 } } 
```

# findKey

## findKey

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10940 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.findkey "See the npm package.")

```
_.findKey(object, [predicate=_.identity]) 
```

这个方法类似 `_.find`。 除了它返回最先被 `predicate` 判断为真值的元素 key，而不是元素本身。

### 参数

1.  object (Object)

    需要检索的对象

2.  [predicate=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (string|undefined)

返回匹配的 key，否则返回 `undefined`。

### 示例

```
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findKey(users, function(o) { return o.age < 40; });
// => 'barney' (无法保证遍历的顺序)

// 使用了 `_.matches` 的回调结果
_.findKey(users, { 'age': 1, 'active': true });
// => 'pebbles'

// 使用了 `_.matchesProperty` 的回调结果
_.findKey(users, ['active', false]);
// => 'fred'

// 使用了 `_.property` 的回调结果
_.findKey(users, 'active');
// => 'barney' 
```

# findLastKey

## findLastKey

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10977 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.findlastkey "See the npm package.")

```
_.findLastKey(object, [predicate=_.identity]) 
```

这个方法类似 `_.findKey`。 不过它是反方向开始遍历的。

### 参数

1.  object (Object)

    需要检索的对象

2.  [predicate=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (string|undefined)

返回匹配的 key，否则返回 `undefined`。

### 示例

```
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findLastKey(users, function(o) { return o.age < 40; });
// => 返回 'pebbles'， `_.findKey` 会返回 'barney'

// 使用了 `_.matches` 的回调结果
_.findLastKey(users, { 'age': 36, 'active': true });
// => 'barney'

// 使用了 `_.matchesProperty` 的回调结果
_.findLastKey(users, ['active', false]);
// => 'fred'

// 使用了 `_.property` 的回调结果
_.findLastKey(users, 'active');
// => 'pebbles' 
```

# forIn

## forIn

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11006 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.forin "See the npm package.")

```
_.forIn(object, [iteratee=_.identity]) 
```

使用 `iteratee` 遍历对象的自身和继承的可枚举属性。 iteratee 会传入 3 个参数：(value, key, object)。 如果返回 false，iteratee 会提前退出遍历。

### 参数

1.  object (Object)

    要遍历的对象

2.  [iteratee=_.identity] (Function)

    这个函数会处理每一个元素

### 返回值 (Object)

返回对象

### 示例

```
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forIn(new Foo, function(value, key) {
  console.log(key);
});
// => 输出 'a', 'b', 然后 'c' (无法保证遍历的顺序) 
```

# forInRight

## forInRight

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11036 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.forinright "See the npm package.")

```
_.forInRight(object, [iteratee=_.identity]) 
```

这个方法类似 `_.forIn`。 除了它是反方向开始遍历的。

### 参数

1.  object (Object)

    要遍历的对象

2.  [iteratee=_.identity] (Function)

    这个函数会处理每一个元素

### 返回值 (Object)

返回对象

### 示例

```
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forInRight(new Foo, function(value, key) {
  console.log(key);
});
// => 输出 'c', 'b', 然后 'a'， `_.forIn` 会输出 'a', 'b', 然后 'c' 
```

# forOwn

## forOwn

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11066 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.forown "See the npm package.")

```
_.forOwn(object, [iteratee=_.identity]) 
```

使用 `iteratee` 遍历自身的可枚举属性。 iteratee 会传入 3 个参数：(value, key, object)。 如果返回 false，iteratee 会提前退出遍历。

### 参数

1.  object (Object)

    要遍历的对象

2.  [iteratee=_.identity] (Function)

    这个函数会处理每一个元素

### 返回值 (Object)

返回对象

### 示例

```
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forOwn(new Foo, function(value, key) {
  console.log(key);
});
// => 输出 'a' 然后 'b' (无法保证遍历的顺序) 
```

# forOwnRight

## forOwnRight

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11093 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.forownright "See the npm package.")

```
_.forOwnRight(object, [iteratee=_.identity]) 
```

这个方法类似 `_.forOwn`。 除了它是反方向开始遍历的。

### 参数

1.  object (Object)

    要遍历的对象

2.  [iteratee=_.identity] (Function)

    这个函数会处理每一个元素

### 返回值 (Object)

返回对象

### 示例

```
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forOwnRight(new Foo, function(value, key) {
  console.log(key);
});
// => 输出 'b' 然后 'a'， `_.forOwn` 会输出 'a' 然后 'b' 
```

# functions

## functions

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11117 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.functions "See the npm package.")

```
_.functions(object) 
```

返回一个 function 对象自身可枚举属性名的数组。

### 参数

1.  object (Object)

    要检索的对象

### 返回值 (Array)

返回包含属性名的新数组

### 示例

```
function Foo() {
  this.a = _.constant('a');
  this.b = _.constant('b');
}

Foo.prototype.c = _.constant('c');

_.functions(new Foo);
// => ['a', 'b'] 
```

# functionsIn

## functionsIn

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11141 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.functionsin "See the npm package.")

```
_.functionsIn(object) 
```

返回一个 function 对象自身和继承的可枚举属性名的数组。

### 参数

1.  object (Object)

    要检索的对象

### 返回值 (Array)

返回包含属性名的新数组

### 示例

```
function Foo() {
  this.a = _.constant('a');
  this.b = _.constant('b');
}

Foo.prototype.c = _.constant('c');

_.functionsIn(new Foo);
// => ['a', 'b', 'c'] 
```

# get

## get

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11169 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.get "See the npm package.")

```
_.get(object, path, [defaultValue]) 
```

根据对象路径获取值。 如果解析 value 是 `undefined` 会以 `defaultValue` 取代。

### 参数

1.  object (Object)

    要检索的对象

2.  path (Array|string)

    要获取的对象路径

3.  [defaultValue] (*)

    如果解析值是 `undefined`，这值会被返回

### 返回值 (*)

返回解析的值

### 示例

```
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.get(object, 'a[0].b.c');
// => 3

_.get(object, ['a', '0', 'b', 'c']);
// => 3

_.get(object, 'a.b.c', 'default');
// => 'default' 
```

# has

## has

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11200 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.has "See the npm package.")

```
_.has(object, path) 
```

检查 `path` 是否是对象的直接属性。

### 参数

1.  object (Object)

    要检索的对象

2.  path (Array|string)

    要检查的路径

### 返回值 (boolean)

如果存在返回 true，否则返回 `false`

### 示例

```
var object = { 'a': { 'b': { 'c': 3 } } };
var other = _.create({ 'a': _.create({ 'b': _.create({ 'c': 3 }) }) });

_.has(object, 'a');
// => true

_.has(object, 'a.b.c');
// => true

_.has(object, ['a', 'b', 'c']);
// => true

_.has(other, 'a');
// => false 
```

# hasIn

## hasIn

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11229 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.hasin "See the npm package.")

```
_.hasIn(object, path) 
```

检查 `path` 是否是对象的直接 或者 继承属性。

### 参数

1.  object (Object)

    要检索的对象

2.  path (Array|string)

    要检查的路径

### 返回值 (boolean)

如果存在返回 true，否则返回 `false`

### 示例

```
var object = _.create({ 'a': _.create({ 'b': _.create({ 'c': 3 }) }) });

_.hasIn(object, 'a');
// => true

_.hasIn(object, 'a.b.c');
// => true

_.hasIn(object, ['a', 'b', 'c']);
// => true

_.hasIn(object, 'b');
// => false 
```

# invert

## invert

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11252 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.invert "See the npm package.")

```
_.invert(object, [multiVal]) 
```

创建一个键值倒置的对象。 如果 `object` 有重复的值，后面的值会覆盖前面的值。 如果 `multiVal` 为 true，重复的值则组成数组。

### 参数

1.  object (Object)

    要倒置的对象

2.  [multiVal] (boolean)

    每个 key 允许多个值

### 返回值 (Object)

返回新的倒置的对象

### 示例

```
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invert(object);
// => { '1': 'c', '2': 'b' } 
```

# invertBy

## invertBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11279 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.invertby "See the npm package.")

```
_.invertBy(object, [iteratee=_.identity]) 
```

这个方法类似 `_.invert`。 除了它接受 iteratee 调用每一个元素，可在返回值中定制 key。 iteratee 会传入 1 个参数：(value)。

### 参数

1.  object (Object)

    要倒置的对象

2.  [iteratee=_.identity] (Function|Object|string)

    这个函数会调用每一个元素

### 返回值 (Object)

返回新的倒置的对象

### 示例

```
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invertBy(object);
// => { '1': ['a', 'c'], '2': ['b'] }

_.invertBy(object, function(value) {
  return 'group' + value;
});
// => { 'group1': ['a', 'c'], 'group2': ['b'] } 
```

# invoke

## invoke

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11303 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.invoke "See the npm package.")

```
_.invoke(object, path, [args]) 
```

调用对象路径的方法

### 参数

1.  object (Object)

    要检索的对象

2.  path (Array|string)

    要调用方法的路径

3.  [args] (...*)

    调用方法的参数

### 返回值 (*)

返回调用方法的结果

var object = { 'a': [{ 'b': { 'c': [1, 2, 3, 4] } }] };

_.invoke(object, 'a[0].b.c.slice', 1, 3); // => [2, 3]

# keys

## keys

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11332 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.keys "See the npm package.")

```
_.keys(object) 
```

创建 `object` 自身可枚举属性名为一个数组。

**注意:** 非对象的值会被强制转换为对象，查看 [ES spec](http://ecma-international.org/ecma-262/6.0/#sec-object.keys) 了解详情

### 参数

1.  object (Object)

    要检索的对象

### 返回值 (Array)

返回包含属性名的数组

### 示例

```
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keys(new Foo);
// => ['a', 'b'] (无法保证遍历的顺序)

_.keys('hi');
// => ['0', '1'] 
```

# keysIn

## keysIn

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11372 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.keysin "See the npm package.")

```
_.keysIn(object) 
```

创建 `object` 自身 或 继承的可枚举属性名为一个数组。

**注意:** 非对象的值会被强制转换为对象

### 参数

1.  object (Object)

    要检索的对象

### 返回值 (Array)

返回包含属性名的数组

### 示例

```
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keysIn(new Foo);
// => ['a', 'b', 'c'] (无法保证遍历的顺序) 
```

# mapKeys

## mapKeys

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11408 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.mapkeys "See the npm package.")

```
_.mapKeys(object, [iteratee=_.identity]) 
```

反向版 `_.mapValues`。 这个方法创建一个对象，对象的值与源对象相同，但 key 是通过 `iteratee` 产生的。

### 参数

1.  object (Object)

    要遍历的对象

2.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (Object)

返回映射后的新对象

### 示例

```
_.mapKeys({ 'a': 1, 'b': 2 }, function(value, key) {
  return key + value;
});
// => { 'a1': 1, 'b2': 2 } 
```

# mapValues

## mapValues

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11442 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.mapvalues "See the npm package.")

```
_.mapValues(object, [iteratee=_.identity]) 
```

创建一个对象，对象的 key 相同，值是通过 `iteratee` 产生的。 iteratee 会传入 3 个参数： (value, key, object)

### 参数

1.  object (Object)

    要遍历的对象

2.  [iteratee=_.identity] (Function|Object|string)

    这个函数会处理每一个元素

### 返回值 (Object)

返回映射后的对象

### 示例

```
var users = {
  'fred':    { 'user': 'fred',    'age': 40 },
  'pebbles': { 'user': 'pebbles', 'age': 1 }
};

_.mapValues(users, function(o) { return o.age; });
// => { 'fred': 40, 'pebbles': 1 } (无法保证遍历的顺序)

// 使用了 `_.property` 的回调结果
_.mapValues(users, 'age');
// => { 'fred': 40, 'pebbles': 1 } (无法保证遍历的顺序) 
```

# merge

## merge

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11479 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.merge "See the npm package.")

```
_.merge(object, [sources]) 
```

递归合并来源对象的自身和继承的可枚举属性到目标对象。 跳过来源对象解析为 `undefined` 的属性。 数组和普通对象会递归合并，其他对象和值会被直接分配。 来源对象从左到右分配，后续的来源对象属性会覆盖之前分配的属性。

**注意:** 这方法会改变源对象

### 参数

1.  object (Object)

    目标对象

2.  [sources] (...Object)

    来源对象

### 返回值 (Object)

返回对象

### 示例

```
var users = {
  'data': [{ 'user': 'barney' }, { 'user': 'fred' }]
};

var ages = {
  'data': [{ 'age': 36 }, { 'age': 40 }]
};

_.merge(users, ages);
// => { 'data': [{ 'user': 'barney', 'age': 36 }, { 'user': 'fred', 'age': 40 }] } 
```

# mergeWith

## mergeWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11516 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.mergewith "See the npm package.")

```
_.mergeWith(object, sources, customizer) 
```

这个方法类似 `_.merge`。 除了它接受一个 `customizer` 决定如何合并。 如果 `customizer` 返回 `undefined` 将会由合并处理方法代替。

### 参数

1.  object (Object)

    目标对象

2.  sources (...Object)

    来源对象

3.  customizer (Function)

    这个方法决定如何合并

### 返回值 (Object)

返回对象

### 示例

```
function customizer(objValue, srcValue) {
  if (_.isArray(objValue)) {
    return objValue.concat(srcValue);
  }
}

var object = {
  'fruits': ['apple'],
  'vegetables': ['beet']
};

var other = {
  'fruits': ['banana'],
  'vegetables': ['carrot']
};

_.mergeWith(object, other, customizer);
// => { 'fruits': ['apple', 'banana'], 'vegetables': ['beet', 'carrot'] } 
```

# omit

## omit

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11537 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.omit "See the npm package.")

```
_.omit(object, [props]) 
```

反向版 `_.pick`。 这个方法返回忽略属性之外的自身和继承的可枚举属性。

### 参数

1.  object (Object)

    来源对象

2.  [props] (...(string|string[])

    要被忽略的属性，单独指定或指定在数组中

### 返回值 (Object)

返回新对象

### 示例

```
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omit(object, ['a', 'c']);
// => { 'b': '2' } 
```

# omitBy

## omitBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11562 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.omitby "See the npm package.")

```
_.omitBy(object, [predicate=_.identity]) 
```

反向版 `_.pickBy`。 这个方法返回经 `predicate` 判断不是真值的属性的自身和继承的可枚举属性。

### 参数

1.  object (Object)

    来源对象

2.  [predicate=_.identity] (Function|Object|string)

    这个函数会调用每一个属性

### 返回值 (Object)

返回新对象

### 示例

```
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omitBy(object, _.isNumber);
// => { 'b': '2' } 
```

# pick

## pick

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11585 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.pick "See the npm package.")

```
_.pick(object, [props]) 
```

创建一个从 `object` 中选中的属性的对象。

### 参数

1.  object (Object)

    来源对象

2.  [props] (...(string|string[])

    要选中的属性名，单独指定或指定在数组中

### 返回值 (Object)

返回新对象

### 示例

```
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 } 
```

# pickBy

## pickBy

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11606 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.pickby "See the npm package.")

```
_.pickBy(object, [predicate=_.identity]) 
```

创建一个从 `object` 中经 `predicate` 判断为真值的属性为对象。 predicate 会传入 1 个参数：(value)

### 参数

1.  object (Object)

    来源对象

2.  [predicate=_.identity] (Function|Object|string)

    这个函数会调用每一个属性

### 返回值 (Object)

返回新对象

### 示例

```
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pickBy(object, _.isNumber);
// => { 'a': 1, 'c': 3 } 
```

# result

## result

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11637 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.result "See the npm package.")

```
_.result(object, path, [defaultValue]) 
```

这个方法类似 `_.get`。 除了如果解析到的值是一个函数的话，就绑定 `this` 到这个函数并返回执行后的结果。

### 参数

1.  object (Object)

    要检索的对象

2.  path (Array|string)

    要解析的属性路径

3.  [defaultValue] (*)

    如果值是 `undefined`，返回这个值

### 返回值 (*)

返回解析后的值

### 示例

```
var object = { 'a': [{ 'b': { 'c1': 3, 'c2': _.constant(4) } }] };

_.result(object, 'a[0].b.c1');
// => 3

_.result(object, 'a[0].b.c2');
// => 4

_.result(object, 'a[0].b.c3', 'default');
// => 'default'

_.result(object, 'a[0].b.c3', _.constant('default'));
// => 'default' 
```

# set

## set

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11675 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.set "See the npm package.")

```
_.set(object, path, value) 
```

设置值到对象对应的属性路径上，如果没有则创建这部分路径。 缺少的索引属性会创建为数组，而缺少的属性会创建为对象。 使用 `_.setWith` 定制创建。

### 参数

1.  object (Object)

    要修改的对象

2.  path (Array|string)

    要设置的对象路径

3.  value (*)

    要设置的值

### 返回值 (Object)

返回对象

### 示例

```
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.set(object, 'a[0].b.c', 4);
console.log(object.a[0].b.c);
// => 4

_.set(object, 'x[0].y.z', 5);
console.log(object.x[0].y.z);
// => 5 
```

# setWith

## setWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11700 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.setwith "See the npm package.")

```
_.setWith(object, path, value, [customizer]) 
```

这个方法类似 `_.set`。 除了它接受一个 `customizer` 决定如何设置对象路径的值。 如果 `customizer` 返回 `undefined` 将会有它的处理方法代替。 `customizer` 会传入 3 个参数：(nsValue, key, nsObject) **注意:** 这个方法会改变源对象

### 参数

1.  object (Object)

    要修改的对象

2.  path (Array|string)

    要设置的对象路径

3.  value (*)

    要设置的值

4.  [customizer] (Function)

    这个函数决定如何分配值

### 返回值 (Object)

返回对象

### 示例

```
_.setWith({ '0': { 'length': 2 } }, '[0][1][2]', 3, Object);
// => { '0': { '1': { '2': 3 }, 'length': 2 } } 
```

# toPairs

## toPairs

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11725 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.topairs "See the npm package.")

```
_.toPairs(object) 
```

创建一个对象自身可枚举属性的键值对数组。

### 参数

1.  object (Object)

    要检索的对象

### 返回值 (Array)

返回键值对的数组

### 示例

```
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.toPairs(new Foo);
// => [['a', 1], ['b', 2]] (无法保证遍历的顺序) 
```

# toPairsIn

## toPairsIn

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11749 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.topairsin "See the npm package.")

```
_.toPairsIn(object) 
```

创建一个对象自身和继承的可枚举属性的键值对数组。

### 参数

1.  object (Object)

    要检索的对象

### 返回值 (Array)

返回键值对的数组

### 示例

```
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.toPairsIn(new Foo);
// => [['a', 1], ['b', 2], ['c', 1]] (无法保证遍历的顺序) 
```

# transform

## transform

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11780 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.transform "See the npm package.")

```
_.transform(object, [iteratee=_.identity], [accumulator]) 
```

`_.reduce` 的代替方法。 这个方法会改变对象为一个新的 `accumulator` 对象，来自每一次经 `iteratee` 处理自身可枚举对象的结果。 每次调用可能会改变 `accumulator` 对象。 iteratee 会传入 4 个对象：(accumulator, value, key, object)。 如果返回 `false`，iteratee 会提前退出。

### 参数

1.  object (Array|Object)

    要遍历的对象

2.  [iteratee=_.identity] (Function)

    这个函数会处理每一个元素

3.  [accumulator] (*)

    定制叠加的值

### 返回值 (*)

返回叠加后的值

### 示例

```
_.transform([2, 3, 4], function(result, n) {
  result.push(n *= n);
  return n % 2 == 0;
}, []);
// => [4, 9]

_.transform({ 'a': 1, 'b': 2, 'c': 1 }, function(result, value, key) {
  (result[value] || (result[value] = [])).push(key);
}, {});
// => { '1': ['a', 'c'], '2': ['b'] } 
```

# unset

## unset

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11828 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.unset "See the npm package.")

```
_.unset(object, path) 
```

移除对象路径的属性。 **注意:** 这个方法会改变源对象

### 参数

1.  object (Object)

    要修改的对象

2.  path (Array|string)

    要移除的对象路径

### 返回值 (boolean)

移除成功返回 `true`，否则返回 `false`

### 示例

```
var object = { 'a': [{ 'b': { 'c': 7 } }] };
_.unset(object, 'a[0].b.c');
// => true

console.log(object);
// => { 'a': [{ 'b': {} }] };

_.unset(object, 'a[0].b.c');
// => true

console.log(object);
// => { 'a': [{ 'b': {} }] }; 
```

# values

## values

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11857 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.values "See the npm package.")

```
_.values(object) 
```

创建 `object` 自身可枚举属性的值为数组

**注意:** 非对象的值会强制转换为对象

### 参数

1.  object (Object)

    要检索的对象

### 返回值 (Array)

返回对象属性的值的数组

### 示例

```
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.values(new Foo);
// => [1, 2] (无法保证遍历的顺序)

_.values('hi');
// => ['h', 'i'] 
```

# valuesIn

## valuesIn

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L11883 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.valuesin "See the npm package.")

```
_.valuesIn(object) 
```

创建 `object` 自身和继承的可枚举属性的值为数组

**注意:** 非对象的值会强制转换为对象

### 参数

1.  object (Object)

    要检索的对象

### 返回值 (Array)

Returns the array of property values.

### 示例

```
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.valuesIn(new Foo);
// => [1, 2, 3] (无法保证遍历的顺序) 
```