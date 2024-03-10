# 从 Common.JS 到 Sea.JS

## CommonJS 是什么

[CommonJS](http://wiki.commonjs.org/) 是一个有志于构建 JavaScript 生态圈的组织。它有一个 [邮件列表](http://groups.google.com/group/commonjs)，很多开发者参与其中。 整个社区致力于提高 JavaScript 程序的可移植性和可交换性，无论是在服务端还是浏览器端。

## CommonJS 模块是什么

JavaScript 并没有内置模块系统（反正现在没有，需要等到 ES6 的普遍支持，不知还需要多少年），于是 CommonJS 创造了自己的。 传统的 CommonJS 模块如下：

math.js

```
exports.add = function() {
  var sum = 0, i = 0, args = arguments, l = args.length;
  while (i < l) {
    sum += args[i++];
  }
  return sum;
};
```

increment.js

```
var add = require('math').add;
exports.increment = function(val) {
  return add(val, 1);
};
```

program.js

```
var inc = require('increment').increment;
var a = 1;
inc(a); // 2
```

## CommonJS 与浏览器

仔细看上面的代码，您会注意到 `require` 是同步的。模块系统需要同步读取模块文件内容，并编译执行以得到模块接口。

然而， **这在浏览器端问题多多**。

浏览器端，加载 JavaScript 最佳、最容易的方式是在 `document` 中插入`<script>` 标签。但脚本标签天生异步，传统 CommonJS 模块在浏览器环境中无法正常加载。

解决思路之一是，开发一个服务器端组件，对模块代码作静态分析，将模块与它的依赖列表一起返回给浏览器端。 这很好使，但需要服务器安装额外的组件，并因此要调整一系列底层架构。

另一种解决思路是，用一套标准模板来封装模块定义：

```
define(function(require, exports, module) {

  // The module code goes here

});
```

这套模板代码为模块加载器提供了机会，使其能在模块代码执行之前，对模块代码进行静态分析，并动态生成依赖列表。

为了让静态分析可行，需要遵守一些简单的 [规则](https://github.com/seajs/seajs/issues/259)。

把上面例子中的模块封装起来，可得到：

math.js

```
define(function(require, exports, module) {
  exports.add = function() {
    var sum = 0, i = 0, args = arguments, l = args.length;
    while (i < l) {
      sum += args[i++];
    }
    return sum;
  };
});
```

increment.js

```
define(function(require, exports, module) {
  var add = require('math').add;
  exports.increment = function(val) {
    return add(val, 1);
  };
});
```

program.js

```
define(function(require, exports, module) {
  var inc = require('increment').increment;
  var a = 1;
  inc(a); // 2
});
```

上面是一种封装方案，还有各种各样的封装方案，比如 AMD、Modules/Wrappings、CommonJS/Modules 2.0 等等模块定义规范。

Sea.js 的封装方案就是 CMD 规范：[CMD 模块定义规范](https://github.com/seajs/seajs/issues/242)

## CommonJS 与 Sea.js

从上面可以看出，Sea.js 的初衷是为了让 CommonJS Modules/1.1 的模块能运行在浏览器端，但由于浏览器和服务器的实质差异，实际上这个梦无法完全达成，也没有必要去达成。

更好的一种方式是，Sea.js 专注于 Web 浏览器端，CommonJS 则专注于服务器端，但两者有共通的部分。对于需要在两端都可以跑的模块，可以 **有便捷的方案来快速迁移**。

目前 Sea.js 的模块，如果没有用到浏览器环境下的特有属性，可以很方便跑在 NodeJS 端。只要在入口文件处，引入 Sea.js 的 Node.js 版本即可：

```
// 让 Node 环境可以加载执行 CMD 模块
require('seajs');
var a = require('./a');
```

这样，`a.js` 就可以是一个用 `define` 包裹起来的 CMD 模块了。

CommonJS 的模块需要跑在浏览器端时，通过简单封装就行：

a.js

```
define(function(require, exports, module) {
   // a.js 原来的代码
});
```

这样 `a.js` 就可以在浏览器端通过 Sea.js 加载运行。当然前提是 `a.js` 没有利用到服务器特有属性和模块，比如 `__dirname`、`process` 等。

通过上面的方案，我们就实现了 CommonJS 与 Sea.js 两个生态圈的融合，可以彼此互通，让我们书写的 JavaScript 模块可移植，可在不同平台上运行。