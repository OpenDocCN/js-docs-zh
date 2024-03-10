# 为什么要有约定和构建工具

在书写 CMD 模块时，需要遵守 [require 书写约定](https://github.com/seajs/seajs/issues/259) 。
在压缩 CMD 模块时，推荐使用配套的 [构建工具](https://github.com/seajs/seajs/issues/538) 来压缩。

为什么要这么做呢？

## CMD 模块的构建过程

CMD 模块在构建时，有两个基本操作：

1.  **提取操作**，用来提取模块的标识 `id` 和依赖 `dependencies`。假设模块代码为：

    a.js

    ```
    define(function(require, exports) {
      var b = require('./b');
    })
    ```

    经过提取操作后，a.js 的源码会转换成临时文件：

    ```
    define('xxx/1.0.0/a', ['./b'], function(require, exports) {
      var b = require('./b');
    })
    ```

2.  **压缩操作**。经过上面的提取操作后，构建工具就可以调用任何 JS 压缩工具来进行压缩了，`require` 参数也可以被压缩成任意字符。

可以看出，和普通压缩工具相比，CMD 模块的构建过程中增加了 `id` 和 `dependencies` 的提取操作。下面说明为什么需要预先提取这两个信息。

## 为什么要提取 `id`

默认情况下，书写 CMD 模块时，不需要手写 `id`：

a.js

```
define(function(require, exports) {
  ...
});
```

b.js

```
define(function(require, exports) {
  ...
});
```

上面两个模块，如果直接合并，会变成：

a+b.js

```
define(function(require, exports) {
  ...
});
define(function(require, exports) {
  ...
});
```

这会导致无法区分 `define` 对应哪个模块。因此在合并前，我们需要通过工具将 `id` 提取出来。

a+b.js:

```
define('a', function(require, exports) {
  ...
});
define('b', function(require, exports) {
  ...
});
```

此外，即便不合并，保持一个文件一个模块，如果压缩时不提取 `id`，那么在 IE6-9 下也有可能会出现问题。这是实现上的困难，具体请看[源码](https://github.com/seajs/seajs/blob/2.2.1/dist/sea-debug.js#L415)。如果要确保上线后在 IE 下没问题，请务必要手写或通过工具提取 `id`。

## 为什么 `require` 要有书写约定

在开发时，Sea.js 是如何知道一个模块的具体依赖呢？

a.js

```
define(function(require, exports) {
  var b = require('./b');
  var c = require('./c');
});
```

Sea.js 在运行 `define` 时，接受 `factory` 参数，可以通过 `factory.toString()` 拿到源码，再通过正则匹配 `require` 的方式来得到依赖信息。依赖信息是一个数组，比如上面 a.js 的依赖数组是：`['./b', './c']`

由于 Sea.js 的这个实现原理，使得书写 CMD 模块代码时，必须遵守 [require 书写约定](https://github.com/seajs/seajs/issues/259)，否则获取不到依赖数组，Sea.js 也就无法正确运行。

而且`正则匹配取依赖`的实现方案并非百分百可靠，除了 require 关键字被压缩的问题以外，对于一些极端情况无法保证正确性，特别对于压缩后的代码。有兴趣的可以看看社区里[关于 require 正则提取依赖的有奖挑战](https://github.com/seajs/seajs/issues/478)。

## 为什么要提取依赖数组 `dependencies`

为了保证压缩工具可以随意压缩代码，构建工具在提取 `id` 字符串时，同时也会提取 `dependencies` 数组。提取过后的代码变成：

```
define('xxx/1.0.0/a', ['./b', './c'], function(require, exports) {
  var b = require('./b');
  var c = require('./c');
});
```

这样，Sea.js 就不需要通过 `factory.toString()` 和正则匹配的方式来获取依赖，直接从第二个参数中就可以拿到依赖数组。

这意味着，提取过 `id` 和 `dependencies` 的模块代码，就可以用任何压缩工具压缩了。

> 注意，一旦设置了 `define` 的第二个参数 `dependencies`，Sea.js 将不会用正则匹配的方式来获取依赖，而直接将 `dependencies` 作为所有的依赖。

## 用普通压缩工具如何压缩 CMD 模块

由于各种原因，暂时无法使用 Sea.js 配套的构建工具来压缩时，需要注意以下几点：

1.  如果项目需要支持 IE，请手写 `id`，即定义模块时，需要人肉写上第一个参数，比如：

    ```
    define('a', function(require, exports) {
      ...
    });
    ```

    如果项目对性能有要求，上线后需要合并文件，也请确保手工写上 `id` 参数。

2.  压缩时，不要压缩 `require` 参数，目前 UglifyJS 支持通过参数来指定保留名字：

    ```
    $ uglifyjs --reserved 'require' -o test-min.js test.js 
    ```

或者自己写工具来保证 `id` 和 `dependencies` 的预先提取。

## 小结

**如果使用 Sea.js，强烈推荐采用配套的构建工具来压缩、合并代码。如果不这么做，可能会带来不少额外的工作甚至隐患。**

这是一把双刃剑，目前业界还没有『完美』的处理方案，都会在某些地方存在取舍和权衡。
如果这方面你有好的想法，欢迎与我们交流。

## 备注：

*   [社区关于 require 正则有奖征集的精彩讨论](https://github.com/seajs/seajs/issues/478)