# Function

# after

## after

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8326 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.after "See the npm package.")

```js
_.after(n, func) 
```

反向版 `_.before`。 这个方法创建一个新函数，当调用 `N` 次或者多次之后将触发 `func` 方法。

### 参数

1.  n (number)

    `func` 方法应该在调用多少次后才执行

2.  func (Function)

    指定的触发方法

### 返回值 (Function)

返回限定的函数

### 示例

```js
var saves = ['profile', 'settings'];

var done = _.after(saves.length, function() {
  console.log('done saving!');
});

_.forEach(saves, function(type) {
  asyncSave({ 'type': type, 'complete': done });
});
// => 2 次 `asyncSave`之后，输出 'done saving!'。 
```

# ary

## ary

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8353 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.ary "See the npm package.")

```js
_.ary(func, [n=func.length]) 
```

创建一个最多接受 `N` 个参数，忽略多余参数的方法。

### 参数

1.  func (Function)

    需要被限制参数个数的函数

2.  [n=func.length] (number)

    限制的参数数量

### 返回值 (Function)

返回新的函数

### 示例

```js
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// => [6, 8, 10] 
```

# before

## before

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8375 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.before "See the npm package.")

```js
_.before(n, func) 
```

创建一个调用 `func` 的函数。 调用次数不超过 `N` 次。 之后再调用这个函数，将返回最后一个调用的结果。

### 参数

1.  n (number)

    超过多少次不再调用 `func`

2.  func (Function)

    指定的触发的函数

### 返回值 (Function)

返回限定的函数

### 示例

```js
jQuery(element).on('click', _.before(5, addContactToList));
// => 最多允许添加 4 个联系人到列表里 
```

# bind

## bind

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8423 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.bind "See the npm package.")

```js
_.bind(func, thisArg, [partials]) 
```

创建一个函数 `func`，这个函数的 `this` 会被绑定在 `thisArg`。 并且任何附加在 `_.bind` 的参数会被传入到这个绑定函数上。 这个 `_.bind.placeholder` 的值，默认是以 `_` 作为附加部分参数的占位符。

**注意:** 不同于原生的 Function#bind，这个方法不会设置绑定函数的 length 属性。

### 参数

1.  func (Function)

    要绑定的函数

2.  thisArg (*)

    这个 `this` 会被绑定给 `func`。

3.  [partials] (...*)

    附加的部分参数

### 返回值 (Function)

返回新的绑定函数

### 示例

```js
var greet = function(greeting, punctuation) {
  return greeting + ' ' + this.user + punctuation;
};

var object = { 'user': 'fred' };

var bound = _.bind(greet, object, 'hi');
bound('!');
// => 'hi fred!'

// 使用了占位符
var bound = _.bind(greet, object, _, '!');
bound('hi');
// => 'hi fred!' 
```

# bindKey

## bindKey

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8475 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.bindkey "See the npm package.")

```js
_.bindKey(object, key, [partials]) 
```

创建一个函数。 该方法绑定 `object[key]` 的方法。 任何附加在 `_.bindKey` 的参数会预设到该绑定函数上。

这个方法与 `_.bind` 的不同之处在于允许重写绑定函数即使它还不存在。 浏览 [Peter Michaux's article](http://peter.michaux.ca/articles/lazy-function-definition-pattern) 了解更多详情。

这个 `_.bindKey.placeholder` 的值，默认是以 `_` 作为附加部分参数的占位符。

### 参数

1.  object (Object)

    需要绑定函数的对象

2.  key (string)

    需要绑定函数对象的键

3.  [partials] (...*)

    附加的部分参数

### 返回值 (Function)

返回新的绑定函数

### 示例

```js
var object = {
  'user': 'fred',
  'greet': function(greeting, punctuation) {
    return greeting + ' ' + this.user + punctuation;
  }
};

var bound = _.bindKey(object, 'greet', 'hi');
bound('!');
// => 'hi fred!'

object.greet = function(greeting, punctuation) {
  return greeting + 'ya ' + this.user + punctuation;
};

bound('!');
// => 'hiya fred!'

// 使用了占位符
var bound = _.bindKey(object, 'greet', _, '!');
bound('hi');
// => 'hiya fred!' 
```

# curry

## curry

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8522 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.curry "See the npm package.")

```js
_.curry(func, [arity=func.length]) 
```

创建一个函数，该函数接收一个或多个 func 的参数。 当该函数被调用时,如果 func 所需要传递的所有参数都被提供，则直接返回 func 所执行的结果。 否则继续返回该函数并等待接收剩余的参数。 可以使用 func.length 强制需要累积的参数个数。

这个 `_.curry.placeholder` 的值，默认是以 `_` 作为附加部分参数的占位符。

**注意:** 这个方法不会设置 "length" 到 curried 函数上。

### 参数

1.  func (Function)

    需要 curry 的函数

2.  [arity=func.length] (number)

    需要提供给 `func` 的参数数量

### 返回值 (Function)

返回 curry 后的函数

### 示例

```js
var abc = function(a, b, c) {
  return [a, b, c];
};

var curried = _.curry(abc);

curried(1)(2)(3);
// => [1, 2, 3]

curried(1, 2)(3);
// => [1, 2, 3]

curried(1, 2, 3);
// => [1, 2, 3]

// 使用了占位符
curried(1)(_, 3)(2);
// => [1, 2, 3] 
```

# curryRight

## curryRight

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8565 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.curryright "See the npm package.")

```js
_.curryRight(func, [arity=func.length]) 
```

这个方法类似 `_.curry`。 除了它接受参数的方式用 `_.partialRight` 代替了 `_.partial`。

这个 `_.curry.placeholder` 的值，默认是以 `_` 作为附加部分参数的占位符。

**注意:** 这个方法不会设置 "length" 到 curried 函数上。

### 参数

1.  func (Function)

    需要 curry 的函数

2.  [arity=func.length] (number)

    需要提供给 `func` 的参数数量

### 返回值 (Function)

返回 curry 后的函数

### 示例

```js
var abc = function(a, b, c) {
  return [a, b, c];
};

var curried = _.curryRight(abc);

curried(3)(2)(1);
// => [1, 2, 3]

curried(2, 3)(1);
// => [1, 2, 3]

curried(1, 2, 3);
// => [1, 2, 3]

// 使用了占位符
curried(3)(1, _)(2);
// => [1, 2, 3] 
```

# debounce

## debounce

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8616 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.debounce "See the npm package.")

```js
_.debounce(func, [wait=0], [options]) 
```

创建一个防抖动函数。 该函数会在 `wait` 毫秒后调用 `func` 方法。 该函数提供一个 `cancel` 方法取消延迟的函数调用以及 `flush` 方法立即调用。 可以提供一个 `options` 对象决定如何调用 `func` 方法， options.leading 与|或 options.trailing 决定延迟前后如何触发。 `func` 会传入最后一次传入的参数给防抖动函数。 随后调用的防抖动函数返回是最后一次 `func` 调用的结果。

**注意:** 如果 `leading` 和 `trailing` 都设定为 true。 则 func 允许 trailing 方式调用的条件为: 在 wait 期间多次调用防抖方法。

查看 [David Corbacho's article](http://drupalmotion.com/article/debounce-and-throttle-visual-explanation) 了解 `_.debounce` 与 `_.throttle` 的区别。

### 参数

1.  func (Function)

    要防抖动的函数

2.  [wait=0] (number)

    需要延迟的毫秒数

3.  [options] (Object)

    选项对象

4.  [options.leading=false] (boolean)

    指定调用在延迟开始前

5.  [options.maxWait] (number)

    设置 `func` 允许被延迟的最大值

6.  [options.trailing=true] (boolean)

    指定调用在延迟结束后

### 返回值 (Function)

返回具有防抖动功能的函数

### 示例

```js
// 避免窗口在变动时出现昂贵的计算开销。
jQuery(window).on('resize', _.debounce(calculateLayout, 150));

// 当点击时 `sendMail` 随后就被调用。
jQuery(element).on('click', _.debounce(sendMail, 300, {
  'leading': true,
  'trailing': false
}));

// 确保 `batchLog` 调用 1 次之后，1 秒内会被触发。
var debounced = _.debounce(batchLog, 250, { 'maxWait': 1000 });
var source = new EventSource('/stream');
jQuery(source).on('message', debounced);

// 取消一个 trailing 的防抖动调用
jQuery(window).on('popstate', debounced.cancel); 
```

# defer

## defer

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8751 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.defer "See the npm package.")

```js
_.defer(func, [args]) 
```

延迟调用 `func` 直到当前堆栈清理完毕。 任何附加的参数会传入到 `func`。

### 参数

1.  func (Function)

    要延迟的函数

2.  [args] (...*)

    会在调用时传入到 `func` 的参数

### 返回值 (number)

返回计时器 id

### 示例

```js
_.defer(function(text) {
  console.log(text);
}, 'deferred');
// 一毫秒或更久一些输出 'deferred'。 
```

# delay

## delay

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8773 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.delay "See the npm package.")

```js
_.delay(func, wait, [args]) 
```

延迟 `wait` 毫秒后调用 `func`。 任何附加的参数会传入到 `func`。

### 参数

1.  func (Function)

    要延迟的函数

2.  wait (number)

    要延迟的毫秒数

3.  [args] (...*)

    会在调用时传入到 `func` 的参数

### 返回值 (number)

返回计时器 id

### 示例

```js
_.delay(function(text) {
  console.log(text);
}, 1000, 'later');
// => 一秒后输出 'later'。 
```

# flip

## flip

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8794 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.flip "See the npm package.")

```js
_.flip(func) 
```

创建一个翻转接收参数的 `func` 函数。

### 参数

1.  func (Function)

    要翻转参数的函数

### 返回值 (Function)

返回新的函数

### 示例

```js
var flipped = _.flip(function() {
  return _.toArray(arguments);
});

flipped('a', 'b', 'c', 'd');
// => ['d', 'c', 'b', 'a'] 
```

# memoize

## memoize

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8839 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.memoize "See the npm package.")

```js
_.memoize(func, [resolver]) 
```

创建一个会缓存 `func` 结果的函数。 如果提供了 `resolver`，就用 `resolver` 的返回值作为 key 缓存函数的结果。 默认情况下用第一个参数作为缓存的 key。 `func` 在调用时 this 会绑定在缓存函数上。

**注意:** 缓存会暴露在缓存函数的 `cache` 上。 它是可以定制的，只要替换了 _.memoize.Cache 构造函数，或实现了 [`Map`](http://ecma-international.org/ecma-262/6.0/#sec-properties-of-the-map-prototype-object) 的 `delete`， `get`， `has`， 以及 `set`方法。

### 参数

1.  func (Function)

    需要缓存化的函数

2.  [resolver] (Function)

    这个函数的返回值作为缓存的 key

### 返回值 (Function)

返回缓存化后的函数

### 示例

```js
var object = { 'a': 1, 'b': 2 };
var other = { 'c': 3, 'd': 4 };

var values = _.memoize(_.values);
values(object);
// => [1, 2]

values(other);
// => [3, 4]

object.a = 2;
values(object);
// => [1, 2]

// 修改结果缓存
values.cache.set(object, ['a', 'b']);
values(object);
// => ['a', 'b']

// 替换 `_.memoize.Cache`
_.memoize.Cache = WeakMap; 
```

# negate

## negate

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8877 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.negate "See the npm package.")

```js
_.negate(predicate) 
```

创建一个对 `func` 结果 取反的函数。 用 predicate 对 `func` 检查的时候，`this` 绑定到创建的函数，并传入对应参数。

### 参数

1.  predicate (Function)

    需要对结果取反的函数

### 返回值 (Function)

返回一个新函数

### 示例

```js
function isEven(n) {
  return n % 2 == 0;
}

_.filter([1, 2, 3, 4, 5, 6], _.negate(isEven));
// => [1, 3, 5] 
```

# once

## once

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8903 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.once "See the npm package.")

```js
_.once(func) 
```

创建一个只能调用一次的函数。 重复调用返回第一次调用的结果。 `func` 调用时，this 绑定到创建的函数，并传入对应参数。

### 参数

1.  func (Function)

    指定的触发的函数

### 返回值 (Function)

返回受限的函数

### 示例

```js
var initialize = _.once(createApplication);
initialize();
initialize();
// `initialize` 只能调用 `createApplication` 一次。 
```

# overArgs

## overArgs

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8936 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.overargs "See the npm package.")

```js
_.overArgs(func, [transforms]) 
```

创建一个函数，调用时`func` 参数会先一对一的改变。

### 参数

1.  func (Function)

    要包裹的函数

2.  [transforms] (...(Function|Function[])

    这个函数会改变传参，单独指定或者指定在数组中

### 返回值 (Function)

返回新函数

### 示例

```js
function doubled(n) {
  return n * 2;
}

function square(n) {
  return n * n;
}

var func = _.overArgs(function(x, y) {
  return [x, y];
}, square, doubled);

func(9, 3);
// => [81, 6]

func(10, 5);
// => [100, 10] 
```

# partial

## partial

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8980 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.partial "See the npm package.")

```js
_.partial(func, [partials]) 
```

创建一个函数。 该函数调用 func，并传入预设的参数。 这个方法类似 `_.bind`，除了它不会绑定 `this`。 这个 `_.partial.placeholder` 的值，默认是以 `_` 作为附加部分参数的占位符。

**注意:** 这个方法不会设置 "length" 到函数上。

### 参数

1.  func (Function)

    需要预设的函数

2.  [partials] (...*)

    预设的参数

### 返回值 (Function)

返回预设参数的函数

### 示例

```js
var greet = function(greeting, name) {
  return greeting + ' ' + name;
};

var sayHelloTo = _.partial(greet, 'hello');
sayHelloTo('fred');
// => 'hello fred'

// 使用了占位符
var greetFred = _.partial(greet, _, 'fred');
greetFred('hi');
// => 'hi fred' 
```

# partialRight

## partialRight

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9012 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.partialright "See the npm package.")

```js
_.partialRight(func, [partials]) 
```

这个函数类似 `_.partial`，除了它是从右到左预设参数的。 这个 *.partialRight.placeholder 的值，默认是以* 作为附加部分参数的占位符。

**注意:** 这个方法不会设置 "length" 到函数上。

### 参数

1.  func (Function)

    需要预设的函数

2.  [partials] (...*)

    预设的参数

### 返回值 (Function)

返回预设参数的函数

### 示例

```js
var greet = function(greeting, name) {
  return greeting + ' ' + name;
};

var greetFred = _.partialRight(greet, 'fred');
greetFred('hi');
// => 'hi fred'

// 使用了占位符
var sayHelloTo = _.partialRight(greet, 'hello', _);
sayHelloTo('fred');
// => 'hello fred' 
```

# rearg

## rearg

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9037 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.rearg "See the npm package.")

```js
_.rearg(func, indexes) 
```

创建一个调用 `func` 的函数。 所传递的参数根据 indexes 调整到对应位置。 第一个 index 对应到第一个传参，第二个 index 对应到第二个传参，以此类推。

### 参数

1.  func (Function)

    待调用的函数

2.  indexes (...(number|number[])

    重新排列参数的位置，单独指定或者指定在数组中

### 返回值 (Function)

返回新的函数

### 示例

```js
var rearged = _.rearg(function(a, b, c) {
  return [a, b, c];
}, 2, 0, 1);

rearged('b', 'c', 'a')
// => ['a', 'b', 'c'] 
```

# rest

## rest

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9063 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.rest "See the npm package.")

```js
_.rest(func, [start=func.length-1]) 
```

创建一个调用 `func` 的函数。 `this` 绑定到这个函数 并且 从 `start` 之后的参数都作为数组传入。

**注意:** 这个方法基于[rest parameter](https://mdn.io/rest_parameters)

### 参数

1.  func (Function)

    要应用的函数

2.  [start=func.length-1] (number)

    从第几个参数开始应用

### 返回值 (Function)

返回新的函数

### 示例

```js
var say = _.rest(function(what, names) {
  return what + ' ' + _.initial(names).join(', ') +
    (_.size(names) > 1 ? ', & ' : '') + _.last(names);
});

say('hello', 'fred', 'barney', 'pebbles');
// => 'hello fred, barney, & pebbles' 
```

# spread

## spread

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9125 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.spread "See the npm package.")

```js
_.spread(func) 
```

创建一个调用 `func` 的函数。 `this` 绑定到这个函数上。 把参数作为数组传入，类似于 [`Function#apply`](https://es5.github.io/#x15.3.4.3)

**注意:** 这个方法基于 [spread operator](https://mdn.io/spread_operator)

### 参数

1.  func (Function)

    要应用的函数

### 返回值 (Function)

返回新的函数

### 示例

```js
var say = _.spread(function(who, what) {
  return who + ' says ' + what;
});

say(['fred', 'hello']);
// => 'fred says hello'

var numbers = Promise.all([
  Promise.resolve(40),
  Promise.resolve(36)
]);

numbers.then(_.spread(function(x, y) {
  return x + y;
}));
// => 返回 76 
```

# throttle

## throttle

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9172 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.throttle "See the npm package.")

```js
_.throttle(func, [wait=0], [options]) 
```

创建一个节流函数，在 `wait` 秒内最多执行 `func` 一次的函数。 该函数提供一个 cancel 方法取消延迟的函数调用以及 flush 方法立即调用。 可以提供一个 options 对象决定如何调用 func 方法， options.leading 与|或 options.trailing 决定 `wait` 前后如何触发。 func 会传入最后一次传入的参数给这个函数。 随后调用的函数返回是最后一次 func 调用的结果。

**注意:** 如果 leading 和 trailing 都设定为 true。 则 func 允许 trailing 方式调用的条件为: 在 wait 期间多次调用。

查看 [David Corbacho's article](http://drupalmotion.com/article/debounce-and-throttle-visual-explanation) 了解 `_.throttle` 与 `_.debounce` 的区别

### 参数

1.  func (Function)

    要节流的函数

2.  [wait=0] (number)

    需要节流的毫秒

3.  [options] (Object)

    选项对象

4.  [options.leading=true] (boolean)

    指定调用在节流开始前

5.  [options.trailing=true] (boolean)

    指定调用在节流结束后

### 返回值 (Function)

返回节流的函数

### 示例

```js
// 避免在滚动时过分的更新定位
jQuery(window).on('scroll', _.throttle(updatePosition, 100));

// 点击后就调用 `renewToken`，但 5 分钟内超过 1 次。
var throttled = _.throttle(renewToken, 300000, { 'trailing': false });
jQuery(element).on('click', throttled);

// 取消一个 trailing 的节流调用
jQuery(window).on('popstate', throttled.cancel); 
```

# unary

## unary

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9199 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.unary "See the npm package.")

```js
_.unary(func) 
```

创建一个最多接受一个参数的函数，忽略多余的参数。

### 参数

1.  func (Function)

    要处理的函数

### 返回值 (Function)

返回新函数

### 示例

```js
_.map(['6', '8', '10'], _.unary(parseInt));
// => [6, 8, 10] 
```

# wrap

## wrap

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L9223 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.wrap "See the npm package.")

```js
_.wrap(value, wrapper) 
```

创建一个函数。提供的 `value` 包装在 wrapper 函数的第一个参数里。 任何附加的参数都提供给 wrapper 函数。 被调用时 `this` 绑定在创建的函数上。

### 参数

1.  value (*)

    要包装的值

2.  wrapper (Function)

    包装函数

### 返回值 (Function)

返回新的函数

### 示例

```js
var p = _.wrap(_.escape, function(func, text) {
  return '<p>' + func(text) + '</p>';
});

p('fred, barney, & pebbles');
// => '<p>fred, barney, &amp; pebbles</p>' 
```