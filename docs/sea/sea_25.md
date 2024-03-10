# ID 和路径匹配原则

> **首先声明这是个万人坑，不要怨恨苦恼，不要垂头丧气，一定要相信希望就在前方，未来一片光明！**

经常收到 `seajs.use` 某具名模块时发现其引用为 null 的问题，或是移动了文件位置导致`引用为 null` 或者 `object is not function` 的问题。比如这个 [#954](https://github.com/seajs/seajs/issues/954) ，这个 [#888](https://github.com/seajs/seajs/issues/888) ，这个 [#879](https://github.com/seajs/seajs/issues/879) ，这个 [#739](https://github.com/seajs/seajs/issues/739) ，这个 [#696](https://github.com/seajs/seajs/issues/696) ，还有这个 [seajs/examples#12](https://github.com/seajs/examples/issues/12) 。

这些问题都指向 Sea.js 的一个基本约定原则：`ID 和路径匹配原则`。

## 这是什么

所谓 `ID 和路径匹配原则` 是指，使用 `seajs.use` 或 `require` 进行引用的文件，如果是具名模块（即定义了 ID 的模块），会把 ID 和 `seajs.use` 的路径名进行匹配，如果一致，则正确执行模块返回结果。反之，则返回 `null`。例如：

```
seajs.use('lib/jquery', function($) {
    // use $
});
```

或者在模块中 require ：

```
define(function(require, exports, module) {
    var $ = require('lib/jquery');
    // use $
});
```

当 jQuery 文件是下面的情况时，上述的变量 `$` 能拿到正确的返回结果。

```
// 文件路径是 lib/jquery.js
// ID 和实际路径匹配了（.js 后缀会自动补上）
define('lib/jquery', function(require, exports, module) {
    // jquery code
});
```

下面的代码则返回 null：

```
// 文件路径是 lib/jquery.js
// 但是 ID 是 lib/jquery.min.js
// ID 和路径不匹配
define('lib/jquery.min', function(require, exports, module) {
    // jquery code
});
```

而匿名模块始终能正确返回结果：

```
// lib/jquery.js
// 匿名模块，不需要进行匹配
// 但是文件中只能有一个 define 块
define(function(require, exports, module) {
    // jquery code
});
```

> 注意这里用于匹配的 ID 都是经过 alias 和 path 解析并且补完后缀之后的。

## 为什么要有这个原则

回答这个问题前，请先阅读这篇文章：[#426](https://github.com/seajs/seajs/issues/426) 。

首先，Sea.js 的模块启动接口秉承的是路径即 ID 的设计原则。`seajs.use` 的方法的第一个参数被规定为文件路径（而不是 ID），这样的设计减轻了记忆模块 ID 的负担，无论是匿名模块还是具名模块，开发者只需要知道文件放在哪儿就行了。

进一步的，之所以有这个 `ID 和路径匹配原则`，是因为在 CMD 的书写规范中，一个文件对应一个模块，所有的模块都是匿名模块（即 `define(factory)` 的形式）。那么当 `seajs.use` 某模块时，这个模块对应的文件里的唯一的 define 方法理所当然的是这个模块的执行代码，这时可以正确返回结果。

但是在生产环境下，静态文件不可避免地需要进行合并打包或者进行 combo，以优化请求数提高页面性能。这时，一个 js 文件可能有很多 `define()` 方法。

```
define(funtion(require, exports, module) {
    // module a
});

define(funtion(require, exports, module) {
    // module b
});

define(funtion(require, exports, module) {
    // module c
});
```

那么请问，当 `seajs.use` 这个文件时，应该返回哪个模块？

所以这时候 ID 就派上了用场，我们可以这样写：

```
// path/a.js

define('path/a', funtion(require, exports, module) {
    // module a
});

define('path/b', funtion(require, exports, module) {
    // module b
});

define('path/c', funtion(require, exports, module) {
    // module c
});
```

我们定义好每个模块的 id ，在 Sea.js 里，那个和文件路径匹配的 ID 的模块就是这个文件的主模块。此时：

```
seajs.use('path/a', function(a) {
    // got a, not b or c
});
```

这个原则保证了我们能够自由合并模块来优化性能，[seajs-combo](https://github.com/seajs/seajs-combo) 和 [spm-build](https://github.com/spmjs/spm-build) 的构建机制都是基于此原则。

在 RequireJS 中，也有类似的原则：[`requirejs.org/docs/errors.html#mismatch`](http://requirejs.org/docs/errors.html#mismatch)

## 更深一步

可能有人要问为啥一定要把 ID 定为文件路径，Sea.js 不是可以自定义 ID 吗，像下面这样：

```
define('module-id', funtion(require, exports, module) {
    // module id
});

// 然后就可以
seajs.use('module-id', function(Module) {
    // Module
});
```

上面的代码当然可以运行。但是有一点，任何一个模块的运行都涉及到两个步骤：`模块定义` 和 `模块执行`，上面的代码两个步骤都包括在内。而使用了 Sea.js ，我们不希望用户去手动写 `script` 标签引用模块。希望只需要 `seajs.use` 模块的文件路径即可（入口唯一）：

```
seajs.use('path/to/module', function(Module) {
    // Module
});
```

Sea.js 会自动插入 script 标签，完成定义步骤，然后执行模块，拿到模块的输出。所以当一个文件里有多个 define 时，只能用 ID 是否匹配 use 中的路径来判断是否主模块。

当然可以回避掉这个原则，你只需要自己负责模块的定义部分，再自己 `seajs.use` 之前定义好的模块 ID 就行。

```
<!-- 各种模块的定义 define define define -->
<script src="http://example.com/modules.js"></script>

<script>
// 这时 use 的第一个参数就可以不必是文件路径了，因为已经有定义好的模块 ID 了
seajs.use('jquery', function($) {
    // $
});
</script>
```

或者通过 alias 来帮助 ID 匹配上最终的路径，这样就和 RequireJS 的方案基本一致了。

```
  // lib/jquery-1.7.2.js 的内容如下
define('$', funtion(require, exports, module) {
  // jQuery
});
```

这样就不需要自己去引用上面的文件，可以直接通过 seajs.use 调用。

```
seajs.config({
  alias: {
    $: 'lib/jquery-1.7.2.js'
  }
});

seajs.use('$', function() {
  // Got $ !
});
```

## 使用 spm-build 和 grunt 进行打包

我们推荐使用配套的[构建工具](https://github.com/seajs/seajs/issues/538)来打包模块。

在 spm-build 中，所有的匿名模块通过[标准的 transport 流程](http://docs.spmjs.org/doc/build-task#js-%E6%96%87%E4%BB%B6)，会打包成具有实际 ID 的具名模块，而主模块（在 package.json 中指定输出的文件）的 ID 和实际路径是匹配的，符合`ID 和路径匹配原则`。

如果没有使用官方工具，你需要在自己的打包和部署过程中保证这个原则。

## 历史

实际上在版本 `1.3.1` 之前，有一个特性叫做 `firstModuleInPackage`，即当一个文件里有多个 define 时，默认将第一个 define 里的模块作为主模块进行返回。由于各种原因我们去掉了这个特性，可以参见：[#438](https://github.com/seajs/seajs/issues/438)。

## 小结

`ID 和路径匹配原则` 是 Sea.js 实现中的一个约定，这个约定帮助我们减少了对 ID 的记忆负担，同时增加了构建的复杂度。

同样的，这也是一把双刃剑，目前还没有『完美』的处理方案，都会在某些地方存在取舍和权衡。如果这方面你有好的想法，欢迎与我们交流。

> PS：对这个问题，也可以看看这篇[《为什么 SeaJS 模块的合并这么麻烦》](http://chaoskeh.com/blog/why-its-hard-to-combo-seajs-modules.html)的解释。