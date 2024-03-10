# 入门指南

# 下载

## 下载

查看 [版本区别](https://github.com/lodash/lodash/wiki/build-differences) 来选择适合你的版本

*   [现代版本](https://raw.github.com/lodash/lodash/3.10.1/lodash.js) ([压缩版](https://raw.github.com/lodash/lodash/3.10.1/lodash.min.js)) 适合现代浏览器（运行环境），例如：Chrome, Firefox, IE ≥ 9, & Safari ≥ 5.1
*   [兼容版本](https://raw.github.com/lodash/lodash-compat/3.10.1/lodash.js) ([压缩版](https://raw.github.com/lodash/lodash-compat/3.10.1/lodash.min.js)) 同时兼容旧的浏览器（运行环境），例如：IE ≤ 8 & PhantomJS

# 引入

## 引入

浏览器中使用:

```js
<script src="lodash.js"></script> 
```

AMD 规范中使用:

```js
require(['lodash'], function(_) {}); 
```

使用 npm 安装:

```js
$ {sudo -H} npm i -g npm$ npm i --save lodash 
```

Node.js/io.js 中使用:

```js
// 直接引用现代版本
var _ = require('lodash');

// 或引用某分类下的所有方法
var array = require('lodash/array');

// 或者引用具体方法 (很适合在 browserify/webpack 中做最小化打包)
var chunk = require('lodash/array/chunk'); 
```

查看 [源码包](https://github.com/lodash/lodash/tree/3.0.0-npm) 了解更多详情

**注意:** 在 REPL 中不要声明 [特殊变量](http://nodejs.org/api/repl.html#repl_repl_features) "`_`"，安装 [n_](https://www.npmjs.com/package/n_) 来代替。

# 模块格式

## 模块格式

lodash 还有多种构建模块的格式

*   npm 构建格式: [现代](https://www.npmjs.com/package/lodash), [兼容](https://www.npmjs.com/package/lodash-compat), & [单个方法](https://www.npmjs.com/browse/keyword/lodash-modularized)
*   AMD 构建格式: [现代](https://github.com/lodash/lodash/tree/3.10.1-amd) & [兼容](https://github.com/lodash/lodash-compat/tree/3.10.1-amd)
*   ES 构建格式: [现代](https://github.com/lodash/lodash/tree/3.10.1-es)

CDN 服务在 [cdnjs](https://cdnjs.com/) & [jsDelivr](http://www.jsdelivr.com/)，通过 版本定制 构建你需要的模块，在找更多的功能用法? 试试 [lodash-fp](https://www.npmjs.com/package/lodash-fp)

# 深入了解

## 深入了解

查看我们的 [更新日志](https://github.com/lodash/lodash/wiki/Changelog), [路线图](https://github.com/lodash/lodash/wiki/Roadmap), 以及 [社区里的播客、文章、视频](https://github.com/lodash/lodash/wiki/Resources).

# 兼容性

## 兼容性

在 Chrome 43-44, Firefox 38-39, IE 6-11, MS Edge, Safari 5-8, ChakraNode 0.12.2, Node.js 0.8.28, 0.10.40, 0.12.7, & 4.0.0, PhantomJS 1.9.8, RingoJS 0.11, & Rhino 1.7.6 测试通过

[自动化测试](https://saucelabs.com/u/lodash) & [持续集成](https://travis-ci.org/lodash/) 已在运作， 特别感谢 [Sauce Labs](https://saucelabs.com/) 提供的浏览器自动化测试。