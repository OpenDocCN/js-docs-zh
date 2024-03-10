# Lang

# Lang

# castArray

## castArray

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9262 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.castarray "See the npm package.")

```
_.castArray(value) 
```

如果 `value` 不是数组, 那么强制转为数组

### 参数

1.  value (*)

    要处理的值

### 返回值 (Array)

返回转换后的数组

### 示例

```
_.castArray(1);
// => [1]

_.castArray({ 'a': 1 });
// => [{ 'a': 1 }]

_.castArray('abc');
// => ['abc']

_.castArray(null);
// => [null]

_.castArray(undefined);
// => [undefined]

_.castArray();
// => []

var array = [1, 2, 3];
console.log(_.castArray(array) === array);
// => true 
```

# clone

## clone

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9294 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.clone "See the npm package.")

```
_.clone(value) 
```

创建一个 `value` 的浅拷贝。

**注意:** 这个方法参考自 [structured clone algorithm](https://mdn.io/Structured_clone_algorithm) 以及支持 arrays、array buffers、 booleans、 date objects、maps、 numbers， `Object` objects, regexes, sets, strings, symbols, 以及 typed arrays。 参数对象的可枚举属性会拷贝为普通对象。 一些不可拷贝的对象，例如 error objects、functions, DOM nodes, 以及 WeakMaps 会返回空对象。

### 参数

1.  value (*)

    要拷贝的值

### 返回值 (*)

返回拷贝后的值

### 示例

```
var objects = [{ 'a': 1 }, { 'b': 2 }];

var shallow = _.clone(objects);
console.log(shallow[0] === objects[0]);
// => true 
```

# cloneDeep

## cloneDeep

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9346 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.clonedeep "See the npm package.")

```
_.cloneDeep(value) 
```

这个方法类似 `_.clone`，除了它会递归拷贝 `value`。

### 参数

1.  value (*)

    要深拷贝的值

### 返回值 (*)

返回拷贝后的值

### 示例

```
var objects = [{ 'a': 1 }, { 'b': 2 }];

var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
// => false 
```

# cloneDeepWith

## cloneDeepWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9376 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.clonedeepwith "See the npm package.")

```
_.cloneDeepWith(value, [customizer]) 
```

这个方法类似 `_.cloneWith`，除了它会递归拷贝 `value`。

### 参数

1.  value (*)

    要深拷贝的值

2.  [customizer] (Function)

    这个函数定制返回的拷贝值

### 返回值 (*)

返回拷贝后的值

### 示例

```
function customizer(value) {
  if (_.isElement(value)) {
    return value.cloneNode(true);
  }
}

var el = _.cloneDeep(document.body, customizer);

console.log(el === document.body);
// => false
console.log(el.nodeName);
// => BODY
console.log(el.childNodes.length);
// => 20 
```

# cloneWith

## cloneWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9326 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.clonewith "See the npm package.")

```
_.cloneWith(value, [customizer]) 
```

这个方法类似 `_.clone`，除了它接受一个 `customizer` 定制返回的拷贝值。 如果 `customizer` 返回 `undefined` 将会拷贝处理方法代替。 `customizer` 会传入 5 个参数：(value [, index|key, object, stack])

### 参数

1.  value (*)

    要拷贝的值

2.  [customizer] (Function)

    这个函数定制返回的拷贝值

### 返回值 (*)

返回拷贝后的值

### 示例

```
function customizer(value) {
  if (_.isElement(value)) {
    return value.cloneNode(false);
  }
}

var el = _.cloneWith(document.body, customizer);

console.log(el === document.body);
// => false
console.log(el.nodeName);
// => 'BODY'
console.log(el.childNodes.length);
// => 0 
```

# eq

## eq

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9409 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.eq "See the npm package.")

```
_.eq(value, other) 
```

执行 [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero) 比较两者的值确定它们是否相等。

### 参数

1.  value (*)

    要比较的值

2.  other (*)

    其他要比较的值

### 返回值 (boolean)

相等返回 `true`，否则返回 `false`

### 示例

```
var object = { 'user': 'fred' };
var other = { 'user': 'fred' };

_.eq(object, object);
// => true

_.eq(object, other);
// => false

_.eq('a', 'a');
// => true

_.eq('a', Object('a'));
// => false

_.eq(NaN, NaN);
// => true 
```

# gt

## gt

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9433 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.gt "See the npm package.")

```
_.gt(value, other) 
```

检查 `value` 是否大于 `other`

### 参数

1.  value (*)

    要比较的值

2.  other (*)

    其他要比较的值

### 返回值 (boolean)

如果 `value` 大于 `other`，返回 `true`，否则返回 `false`

### 示例

```
_.gt(3, 1);
// => true

_.gt(3, 3);
// => false

_.gt(1, 3);
// => false 
```

# gte

## gte

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9457 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.gte "See the npm package.")

```
_.gte(value, other) 
```

检查 `value` 是否大于等于 `other`

### 参数

1.  value (*)

    要比较的值

2.  other (*)

    其他要比较的值

### 返回值 (boolean)

如果 `value` 大于等于 `other`，返回 `true`，否则返回 `false`

### 示例

```
_.gte(3, 1);
// => true

_.gte(3, 3);
// => true

_.gte(1, 3);
// => false 
```

# isArguments

## isArguments

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9477 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isarguments "See the npm package.")

```
_.isArguments(value) 
```

检查 `value` 是否是 类 `arguments` 对象。

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isArguments(function() { return arguments; }());
// => true

_.isArguments([1, 2, 3]);
// => false 
```

# isArray

## isArray

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9506 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isarray "See the npm package.")

```
_.isArray(value) 
```

检查 `value` 是否是 `Array` 类对象。

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isArray([1, 2, 3]);
// => true

_.isArray(document.body.children);
// => false

_.isArray('abc');
// => false

_.isArray(_.noop);
// => false 
```

# isArrayBuffer

## isArrayBuffer

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9524 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isarraybuffer "See the npm package.")

```
_.isArrayBuffer(value) 
```

检查 `value` 是否是 `ArrayBuffer` 对象。

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是 `ArrayBuffer`，返回 `true`，否则返回 `false`.

### 示例

```
_.isArrayBuffer(new ArrayBuffer(2));
// => true

_.isArrayBuffer(new Array(2));
// => false 
```

# isArrayLike

## isArrayLike

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9551 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isarraylike "See the npm package.")

```
_.isArrayLike(value) 
```

检查 `value` 是否是类数组。 如果是类数组的话，应该不是一个函数，而且 `value.length` 是个整数，大于等于 0，小于或等于 `Number.MAX_SAFE_INTEGER`

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是类数组，返回 `true`，否则返回 `false`

### 示例

```
_.isArrayLike([1, 2, 3]);
// => true

_.isArrayLike(document.body.children);
// => true

_.isArrayLike('abc');
// => true

_.isArrayLike(_.noop);
// => false 
```

# isArrayLikeObject

## isArrayLikeObject

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9577 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isarraylikeobject "See the npm package.")

```
_.isArrayLikeObject(value) 
```

这个方法类似 `_.isArrayLike`，除了它还检查值是否是个对象。

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是类数组对象，返回 `true`，否则返回 `false`

### 示例

```
_.isArrayLikeObject([1, 2, 3]);
// => true

_.isArrayLikeObject(document.body.children);
// => true

_.isArrayLikeObject('abc');
// => false

_.isArrayLikeObject(_.noop);
// => false 
```

# isBoolean

## isBoolean

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9597 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isboolean "See the npm package.")

```
_.isBoolean(value) 
```

检查 `value` 是否是原始 boolean 类型或者对象。

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isBoolean(false);
// => true

_.isBoolean(null);
// => false 
```

# isBuffer

## isBuffer

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9618 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isbuffer "See the npm package.")

```
_.isBuffer(value) 
```

检查 `value` 是否是个 `buffer`

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isBuffer(new Buffer(2));
// => true

_.isBuffer(new Uint8Array(2));
// => false 
```

# isDate

## isDate

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9638 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isdate "See the npm package.")

```
_.isDate(value) 
```

检查 `value` 是否是 `Date` 类型

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isDate(new Date);
// => true

_.isDate('Mon April 23 2012');
// => false 
```

# isElement

## isElement

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9658 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.iselement "See the npm package.")

```
_.isElement(value) 
```

检查 `value` 是否是可能是 DOM 元素

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是 DOM 元素返回 `true`，否则返回 `false`

### 示例

```
_.isElement(document.body);
// => true

_.isElement('<body>');
// => false 
```

# isEmpty

## isEmpty

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9688 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isempty "See the npm package.")

```
_.isEmpty(value) 
```

检查 `value` 是否为空。 判断的依据是除非是有枚举属性的对象，length 大于 `0` 的 `arguments` object, array, string 或类 jquery 选择器。

### 参数

1.  value (Array|Object|string)

    要检查的值

### 返回值 (boolean)

如果为空返回 `true`，否则返回 `false`

### 示例

```
_.isEmpty(null);
// => true

_.isEmpty(true);
// => true

_.isEmpty(1);
// => true

_.isEmpty([1, 2, 3]);
// => false

_.isEmpty({ 'a': 1 });
// => false 
```

# isEqual

## isEqual

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9726 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isequal "See the npm package.")

```
_.isEqual(value, other) 
```

执行深比较来决定两者的值是否相等。

**注意:** 这个方法支持比较 arrays, array buffers, booleans, date objects, error objects, maps, numbers, `Object` objects, regexes, sets, strings, symbols, 以及 typed arrays. `Object` 对象值比较自身的属性，不包括继承的和可枚举的属性。 不支持函数和 DOM 节点。

### 参数

1.  value (*)

    要比较的值

2.  other (*)

    其他要比较的值

### 返回值 (boolean)

如果相等返回 `true`，否则返回 `false`

### 示例

```
var object = { 'user': 'fred' };
var other = { 'user': 'fred' };

_.isEqual(object, other);
// => true

object === other;
// => false 
```

# isEqualWith

## isEqualWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9760 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isequalwith "See the npm package.")

```
_.isEqualWith(value, other, [customizer]) 
```

这个方法类似 `_.isEqual`。 除了它接受一个 customizer 定制比较值。 如果 customizer 返回 undefined 将会比较处理方法代替。 `customizer` 会传入 7 个参数：(objValue, othValue [, index|key, object, other, stack])

### 参数

1.  value (*)

    要比较的值

2.  other (*)

    其他要比较的值

3.  [customizer] (Function)

    这个函数定制比较值

### 返回值 (boolean)

如果相等返回 `true`，否则返回 `false`

### 示例

```
function isGreeting(value) {
  return /^h(?:i|ello)$/.test(value);
}

function customizer(objValue, othValue) {
  if (isGreeting(objValue) && isGreeting(othValue)) {
    return true;
  }
}

var array = ['hello', 'goodbye'];
var other = ['hi', 'goodbye'];

_.isEqualWith(array, other, customizer);
// => true 
```

# isError

## isError

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9783 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.iserror "See the npm package.")

```
_.isError(value) 
```

检查 `value` 是否是 `Error`, `EvalError`, `RangeError`, `ReferenceError`, `SyntaxError`, `TypeError`, 或 `URIError` object.

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是 error object 返回 `true`，否则返回 `false`

### 示例

```
_.isError(new Error);
// => true

_.isError(Error);
// => false 
```

# isFinite

## isFinite

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9815 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isfinite "See the npm package.")

```
_.isFinite(value) 
```

检查 `value` 是否是原始 finite number。

**注意:** 这个方法基于 [`Number.isFinite`](https://mdn.io/Number/isFinite).

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是 finite number 返回 `true`，否则返回 `false`

### 示例

```
_.isFinite(3);
// => true

_.isFinite(Number.MAX_VALUE);
// => true

_.isFinite(3.14);
// => true

_.isFinite(Infinity);
// => false 
```

# isFunction

## isFunction

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9835 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isfunction "See the npm package.")

```
_.isFunction(value) 
```

检查 `value` 是否是 `Function` 对象。

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isFunction(_);
// => true

_.isFunction(/abc/);
// => false 
```

# isInteger

## isInteger

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9867 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isinteger "See the npm package.")

```
_.isInteger(value) 
```

检查 `value` 是否是整数。

**注意:** 这个方法基于 [`Number.isInteger`](https://mdn.io/Number/isInteger).

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是整数返回 `true`，否则返回 `false`

### 示例

```
_.isInteger(3);
// => true

_.isInteger(Number.MIN_VALUE);
// => false

_.isInteger(Infinity);
// => false

_.isInteger('3');
// => false 
```

# isLength

## isLength

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9895 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.islength "See the npm package.")

```
_.isLength(value) 
```

检查 `value` 是否是有效长度

**注意:** 这个方法参考自 [`ToLength`](http://ecma-international.org/ecma-262/6.0/#sec-tolength).

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是有效长度返回 `true`，否则返回 `false`

### 示例

```
_.isLength(3);
// => true

_.isLength(Number.MIN_VALUE);
// => false

_.isLength(Infinity);
// => false

_.isLength('3');
// => false 
```

# isMap

## isMap

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9970 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.ismap "See the npm package.")

```
_.isMap(value) 
```

检查 `value` 是否是个 `Map` 对象

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是 `Map` 对象返回 `true`，否则返回 `false`

### 示例

```
_.isMap(new Map);
// => true

_.isMap(new WeakMap);
// => false 
```

# isMatch

## isMatch

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9995 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.ismatch "See the npm package.")

```
_.isMatch(object, source) 
```

执行一个深比较来确定`object` 是否包含有 `source` 的属性值。

**注意:** 这个方法支持比较相同的值和 `_.isEqual` 一样

### 参数

1.  object (Object)

    要检查的值

2.  source (Object)

    匹配包含在 object 的对象

### 返回值 (boolean)

如果匹配返回 `true`，否则返回 `false`

### 示例

```
var object = { 'user': 'fred', 'age': 40 };

_.isMatch(object, { 'age': 40 });
// => true

_.isMatch(object, { 'age': 36 });
// => false 
```

# isMatchWith

## isMatchWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10029 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.ismatchwith "See the npm package.")

```
_.isMatchWith(object, source, [customizer]) 
```

这个方法类似 `_.isMatch`。 除了它接受一个 customizer 定制比较的值。 如果 customizer 返回 undefined 将会比较处理方法代替。 customizer 会传入 5 个参数：(objValue, srcValue, index|key, object, source)

### 参数

1.  object (Object)

    要检查的值

2.  source (Object)

    匹配包含在 object 的对象

3.  [customizer] (Function)

    这个函数定制比较值

### 返回值 (boolean)

如果匹配返回 `true`，否则返回 `false`

### 示例

```
function isGreeting(value) {
  return /^h(?:i|ello)$/.test(value);
}

function customizer(objValue, srcValue) {
  if (isGreeting(objValue) && isGreeting(srcValue)) {
    return true;
  }
}

var object = { 'greeting': 'hello' };
var source = { 'greeting': 'hi' };

_.isMatchWith(object, source, customizer);
// => true 
```

# isNaN

## isNaN

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10059 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isnan "See the npm package.")

```
_.isNaN(value) 
```

检查 `value` 是否是 `NaN`.

**注意:** 这个方法不同于 [`isNaN`](https://es5.github.io/#x15.1.2.4) 对 undefind 和 其他非数值返回 true.

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果符合 `NaN` 返回 `true`，否则返回 `false`

### 示例

```
_.isNaN(NaN);
// => true

_.isNaN(new Number(NaN));
// => true

isNaN(undefined);
// => true

_.isNaN(undefined);
// => false 
```

# isNative

## isNative

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10081 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isnative "See the npm package.")

```
_.isNative(value) 
```

检查 `value` 是否是原生函数

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是原生函数返回 `true`，否则返回 `false`

### 示例

```
_.isNative(Array.prototype.push);
// => true

_.isNative(_);
// => false 
```

# isNil

## isNil

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10131 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isnil "See the npm package.")

```
_.isNil(value) 
```

检查 `value` 是否是 `null` 或者 `undefined`。

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是 `null` 或者 `undefined` 返回 `true`，否则返回 `false`

### 示例

```
_.isNil(null);
// => true

_.isNil(void 0);
// => true

_.isNil(NaN);
// => false 
```

# isNull

## isNull

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10108 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isnull "See the npm package.")

```
_.isNull(value) 
```

检查 `value` 是否是 `null`.

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是 `null` 返回 `true`，否则返回 `false`

### 示例

```
_.isNull(null);
// => true

_.isNull(void 0);
// => false 
```

# isNumber

## isNumber

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10159 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isnumber "See the npm package.")

```
_.isNumber(value) 
```

检查 `value` 是否是原始数值型 或者 对象。

**注意:** 要排除 `Infinity`, `-Infinity`, 以及 `NaN` 数值类型，用 `_.isFinite` 方法

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isNumber(3);
// => true

_.isNumber(Number.MIN_VALUE);
// => true

_.isNumber(Infinity);
// => true

_.isNumber('3');
// => false 
```

# isObject

## isObject

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9922 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isobject "See the npm package.")

```
_.isObject(value) 
```

检查 `value` 是否是 `Object` 的 [language type](https://es5.github.io/#x8)。 (例如： arrays, functions, objects, regexes, `new Number(0)`, 以及 `new String('')`)

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是对象返回 `true`，否则返回 `false`

### 示例

```
_.isObject({});
// => true

_.isObject([1, 2, 3]);
// => true

_.isObject(_.noop);
// => true

_.isObject(null);
// => false 
```

# isObjectLike

## isObjectLike

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9950 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isobjectlike "See the npm package.")

```
_.isObjectLike(value) 
```

检查 `value` 是否是 类对象。 类对象应该不是 `null` 以及 `typeof` 的结果是 "object"。

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是类对象返回 `true`，否则返回 `false`

### 示例

```
_.isObjectLike({});
// => true

_.isObjectLike([1, 2, 3]);
// => true

_.isObjectLike(_.noop);
// => false

_.isObjectLike(null);
// => false 
```

# isPlainObject

## isPlainObject

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10191 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isplainobject "See the npm package.")

```
_.isPlainObject(value) 
```

检查 `value` 是否是普通对象。 也就是说该对象由 `Object` 构造函数创建或者 `[[Prototype]]` 为空。

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是普通对象返回 `true`，否则返回 `false`

### 示例

```
function Foo() {
  this.a = 1;
}

_.isPlainObject(new Foo);
// => false

_.isPlainObject([1, 2, 3]);
// => false

_.isPlainObject({ 'x': 0, 'y': 0 });
// => true

_.isPlainObject(Object.create(null));
// => true 
```

# isRegExp

## isRegExp

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10220 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isregexp "See the npm package.")

```
_.isRegExp(value) 
```

检查 `value` 是否是 `RegExp` 对象

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isRegExp(/abc/);
// => true

_.isRegExp('/abc/');
// => false 
```

# isSafeInteger

## isSafeInteger

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10249 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.issafeinteger "See the npm package.")

```
_.isSafeInteger(value) 
```

检查 `value` 是否是安全整数。 这个整数应该是符合 IEEE-754 标准的非双精度浮点数。

**注意:** 这个方法基于 [`Number.isSafeInteger`](https://mdn.io/Number/isSafeInteger).

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是安全整数返回`true`，否则返回 `false`

### 示例

```
_.isSafeInteger(3);
// => true

_.isSafeInteger(Number.MIN_VALUE);
// => false

_.isSafeInteger(Infinity);
// => false

_.isSafeInteger('3');
// => false 
```

# isSet

## isSet

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10269 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isset "See the npm package.")

```
_.isSet(value) 
```

检查 `value` 是否是 `Set` 对象。

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isSet(new Set);
// => true

_.isSet(new WeakSet);
// => false 
```

# isString

## isString

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10289 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isstring "See the npm package.")

```
_.isString(value) 
```

检查 `value` 是否是原始字符串或者对象。

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isString('abc');
// => true

_.isString(1);
// => false 
```

# isSymbol

## isSymbol

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10310 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.issymbol "See the npm package.")

```
_.isSymbol(value) 
```

检查 `value` 是否是原始 `Symbol` 或者对象。

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isSymbol(Symbol.iterator);
// => true

_.isSymbol('abc');
// => false 
```

# isTypedArray

## isTypedArray

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10331 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.istypedarray "See the npm package.")

```
_.isTypedArray(value) 
```

检查 `value` 是否是 TypedArray。

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isTypedArray(new Uint8Array);
// => true

_.isTypedArray([]);
// => false 
```

# isUndefined

## isUndefined

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10351 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isundefined "See the npm package.")

```
_.isUndefined(value) 
```

检查 `value` 是否是 `undefined`.

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isUndefined(void 0);
// => true

_.isUndefined(null);
// => false 
```

# isWeakMap

## isWeakMap

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10371 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isweakmap "See the npm package.")

```
_.isWeakMap(value) 
```

检查 `value` 是否是 `WeakMap` 对象

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isWeakMap(new WeakMap);
// => true

_.isWeakMap(new Map);
// => false 
```

# isWeakSet

## isWeakSet

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10391 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.isweakset "See the npm package.")

```
_.isWeakSet(value) 
```

检查 `value` 是否是 `WeakSet` 对象

### 参数

1.  value (*)

    要检查的值

### 返回值 (boolean)

如果是正确的类型，返回 `true`，否则返回 `false`

### 示例

```
_.isWeakSet(new WeakSet);
// => true

_.isWeakSet(new Set);
// => false 
```

# lt

## lt

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10415 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.lt "See the npm package.")

```
_.lt(value, other) 
```

检查 `value` 是否是 小于 `other`。

### 参数

1.  value (*)

    要比较的值

2.  other (*)

    其他要比较的值

### 返回值 (boolean)

如果 `value` 小于 `other` 返回 `true`，否则返回 `false`

### 示例

```
_.lt(1, 3);
// => true

_.lt(3, 3);
// => false

_.lt(3, 1);
// => false 
```

# lte

## lte

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10439 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.lte "See the npm package.")

```
_.lte(value, other) 
```

检查 `value` 是否是 小于等于 `other`.

### 参数

1.  value (*)

    要比较的值

2.  other (*)

    其他要比较的值

### 返回值 (boolean)

如果 `value` 小于等于 `other` 返回 `true`，否则返回 `false`

### 示例

```
_.lte(1, 3);
// => true

_.lte(3, 3);
// => true

_.lte(3, 1);
// => false 
```

# toArray

## toArray

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10465 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.toarray "See the npm package.")

```
_.toArray(value) 
```

转换 `value` 为数组

### 参数

1.  value (*)

    要转换的值

### 返回值 (Array)

然后转换后的数组

### 示例

```
_.toArray({ 'a': 1, 'b': 2 });
// => [1, 2]

_.toArray('abc');
// => ['a', 'b', 'c']

_.toArray(1);
// => []

_.toArray(null);
// => [] 
```

# toInteger

## toInteger

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10505 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.tointeger "See the npm package.")

```
_.toInteger(value) 
```

转换 `value` 为整数

**注意:** 这个函数参考 [`ToInteger`](http://www.ecma-international.org/ecma-262/6.0/#sec-tointeger).

### 参数

1.  value (*)

    要转换的值

### 返回值 (number)

返回转换后的整数

### 示例

```
_.toInteger(3);
// => 3

_.toInteger(Number.MIN_VALUE);
// => 0

_.toInteger(Infinity);
// => 1.7976931348623157e+308

_.toInteger('3');
// => 3 
```

# toLength

## toLength

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10542 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.tolength "See the npm package.")

```
_.toLength(value) 
```

转换 `value` 为用作类数组对象的长度整数。

**注意:** 这个方法基于 [`ToLength`](http://ecma-international.org/ecma-262/6.0/#sec-tolength).

### 参数

1.  value (*)

    要转换的值

### 返回值 (number)

返回转换后的整数

### 示例

```
_.toLength(3);
// => 3

_.toLength(Number.MIN_VALUE);
// => 0

_.toLength(Infinity);
// => 4294967295

_.toLength('3');
// => 3 
```

# toNumber

## toNumber

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10568 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.tonumber "See the npm package.")

```
_.toNumber(value) 
```

转换 `value` 为数值

### 参数

1.  value (*)

    要处理的值

### 返回值 (number)

返回数值

### 示例

```
_.toNumber(3);
// => 3

_.toNumber(Number.MIN_VALUE);
// => 5e-324

_.toNumber(Infinity);
// => Infinity

_.toNumber('3');
// => 3 
```

# toPlainObject

## toPlainObject

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10606 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.toplainobject "See the npm package.")

```
_.toPlainObject(value) 
```

转换 `value` 为普通对象。 包括继承的可枚举属性。

### 参数

1.  value (*)

    要转换的值

### 返回值 (Object)

返回转换后的普通对象

### 示例

```
function Foo() {
  this.b = 2;
}

Foo.prototype.c = 3;

_.assign({ 'a': 1 }, new Foo);
// => { 'a': 1, 'b': 2 }

_.assign({ 'a': 1 }, _.toPlainObject(new Foo));
// => { 'a': 1, 'b': 2, 'c': 3 } 
```

# toSafeInteger

## toSafeInteger

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10633 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.tosafeinteger "See the npm package.")

```
_.toSafeInteger(value) 
```

转换 `value` 为安全整数。 安全整数可以用于比较和准确的表示。

### 参数

1.  value (*)

    要转换的值

### 返回值 (number)

返回转换后的整数

### 示例

```
_.toSafeInteger(3);
// => 3

_.toSafeInteger(Number.MIN_VALUE);
// => 0

_.toSafeInteger(Infinity);
// => 9007199254740991

_.toSafeInteger('3');
// => 3 
```

# toString

## toString

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L10657 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.tostring "See the npm package.")

```
_.toString(value) 
```

如果 `value` 不是字符串，将其转换为字符串。 `null` 和 `undefined` 将返回空字符串。

### 参数

1.  value (*)

    要转换的值

### 返回值 (string)

返回字符串

### 示例

```
_.toString(null);
// => ''

_.toString(-0);
// => '-0'

_.toString([1, 2, 3]);
// => '1,2,3' 
```