# require 书写约定

使用 Sea.js 书写模块代码时，需要遵循一些简单规则。

> 只是书写和调试时的规范！！！构建后的代码完全不需要遵循下面的约定！！！！！！

### 1\. 正确拼写

模块 factory 构造方法的第一个参数 **必须** 命名为 `require` 。

```js
// 错误！
define(function(req) {
  // ...
});

// 正确！
define(function(require) {
  // ...
});
```

### 2\. 不要修改

不要重命名 `require` 函数，或在任何作用域中给 `require` 重新赋值。

```js
// 错误 - 重命名 "require"！
var req = require, mod = req("./mod");

// 错误 - 重定义 "require"!
require = function() {};

// 错误 - 重定义 "require" 为函数参数！
function F(require) {}

// 错误 - 在内嵌作用域内重定义了 "require"！
function F() {
  var require = function() {};
}
```

### 3\. 使用直接量

`require` 的参数值 **必须** 是字符串直接量。

```js
// 错误！
require(myModule);

// 错误！
require("my-" + "module");

// 错误！
require("MY-MODULE".toLowerCase());

// 正确！
require("my-module");
```

在书写模块代码时，必须遵循这些规则。其实只要把 `require` **看做是语法关键字** 就好啦。

## 关于动态依赖

有时会希望可以使用 `require` 来进行条件加载：

```js
if (todayIsWeekend)
  require("play");
else
  require("work");
```

但请牢记，从静态分析的角度来看，这个模块同时依赖 play 和 work 两个模块，加载器会把这两个模块文件都下载下来。 这种情况下，推荐使用 `require.async` 来进行条件加载。

## Why?

这些约定初看起来会有些小不爽，其实也的确可以通过每次都编译的方式来去掉这些限制。但编译的方式，会给开发调试带来麻烦，代码的实现复杂度也会增加。Sea.js 的核心设计原则是保持简单，遵循 [New Jersey Approach](http://blog.jobbole.com/19062/)：

> 简单性：设计必须简单，这既是对实现的要求，也是对接口的要求。实现的简单要比接口的简单更加重要。简单是设计中需要第一重视的因素。

因为简单，所以可靠！

## 参考文档

*   [为什么要用构建工具来压缩 CMD 模块](https://github.com/seajs/seajs/issues/426)