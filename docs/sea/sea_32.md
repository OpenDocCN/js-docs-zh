# 与 Node.js 兼容

Sea.js 的模块遵循 [CMD](https://github.com/seajs/seajs/issues/242) 规范，与 Node.js 的模块规范非常相近，两者的模块可以很容易互相迁移。

## 让 Sea.js 的模块跑在 Node 上

非常简单。首先需要安装 `seajs` 的 Node 模块：

```js
$ npm install seajs -g 
```

安装好后，在需要调用 Sea.js 模块的入口文件里，`require` 下 `seajs` ：

a.js

```js
define(function(require, exports) {
  exports.name = 'A';
});
```

main.js

```js
require('seajs');

var a = require('./a');
console.log(a.name);
```

这样就可以在 Node 环境中运行 Sea.js 的模块了：

```js
$ node main.js
A 
```

## 让 Node 的模块跑在浏览器端

这个也很简单，将 Node 的模块封装成 CMD 模块即可：

a.js

```js
exports.name = 'A';
```

封装成

```js
define(function(require, exports) {
  exports.name = 'A';
});
```

这样在浏览器端就可以通过 Sea.js 来加载使用了：

```js
seajs.use('./a', function(a) {
  console.log(a.name);
});
```

## 通用的前提条件

通过上面的例子可以看出，只要遵循 CMD 规范来书写模块代码，就可以非常方便的同时运行在浏览器端和服务器端。这是 CMD 中 C 字母的含义：Common（通用）。

这比 RequireJS 的 AMD 规范好很多。

但是，无论是 CMD 还是 AMD 规范，或者是未来的某个 Modules/Cool 规范，一个模块要想同时在不同环境下执行，就得遵循以下前提条件：

1.  **不能调用浏览器端的私有特性。**比如 `attachEvent` 之类的，除非你在 Node 端提前模拟好。
2.  **不能调用服务器端的私有特性。**比如 `process` 对象，除非你在浏览器端自己实现一个类似的 `process` 对象。
3.  **只用不同规范中的交集。**比如 CMD 中有 `module.uri` 属性，但 Node 中没有，要通用，就不能去调用这些有差异的接口。类似的，Node 端的 `__filename` 在浏览器端不存在，要通用的话，也不能调用。

其实上面这些严格要求，是 **非常自然的**。这就如浏览器兼容一样，要写出所有浏览器下都能跑的代码，最好的方式是只用那些所有浏览器都支持的特性，不然你就得用 `if ... else ...` 去搞啦。

## 附录

Node.js 与 Sea.js 在模块接口上的主要差异如下：

1.  Node.js 里，模块文件里的 `this === module.exports`；Sea.js 里，`this === window`。
2.  Node.js 里，模块文件里的 `return xx` 会被忽略；Sea.js 里，`return xx` 等价 `module.exports = xx`。
3.  Node.js 里，`require` 是懒加载 + 懒执行的。在 Sea.js 里是提前加载好 + 懒执行。
4.  Sea.js 里，`require(id)` 中的 `id` 必须是字符串直接量。Node.js 里没这个限制。

## 参考阅读

*   [从 CommonJS 到 Sea.js](https://github.com/seajs/seajs/issues/269)