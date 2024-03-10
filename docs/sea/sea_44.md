# 2.1.0

终于赶在 6 月份的尾巴，『如期』发布 2.1 版本了。不许说我跳票，非常感谢阿里国际站 [@lianqin7](https://github.com/lianqin7) 等同事以及社区不少朋友们的给力测试，如果不是你们的『苛求』，2.1 早就发布了，但肯定不会有现在的质量这么好。感谢并感恩。

## 下载使用

赶快下载试用吧：[下载](http://seajs.org/docs/#downloads)
记得阅读一遍文档：[文档](http://seajs.org/docs/) （文档重新梳理过，多少四五点就起床了。还说不好的，帮助一起来完善吧）

Node.js 环境下，可以通过命令行下载：

```js
$ npm install spm -g
$ spm install seajs 
```

新手推荐阅读：[快速上手](http://seajs.org/docs/#quick-start)

## 核心优化

### 性能大幅提升

无论是 CPU 消耗，还是内存占用，2.1 都进行了大量优化。目前性能是 RequireJS 的两到三倍。测试页面：

1000 层依赖：

*   [`seajs.github.io/seajs/tests/speed/thousand-modules/test-seajs.html`](http://seajs.github.io/seajs/tests/speed/thousand-modules/test-seajs.html)
*   [`seajs.github.io/seajs/tests/speed/thousand-modules/test-requirejs.html`](http://seajs.github.io/seajs/tests/speed/thousand-modules/test-requirejs.html)

多层复杂依赖：

*   [`seajs.github.io/seajs/tests/speed/deps-100/test-seajs.html`](http://seajs.github.io/seajs/tests/speed/deps-100/test-seajs.html)
*   [`seajs.github.io/seajs/tests/speed/deps-100/test-requirejs.html`](http://seajs.github.io/seajs/tests/speed/deps-100/test-requirejs.html)

详见：[#731](https://github.com/seajs/seajs/issues/731) [#732](https://github.com/seajs/seajs/issues/732) [#782](https://github.com/seajs/seajs/issues/782)

### API 更加纯粹简单

Sea.js 是浏览器端的模块加载器，功能范畴应该非常清楚。2.1 中对所有功能进行了重新梳理，主要修改有：

1.  核心代码重构，内部逻辑更清晰易懂。
2.  所有插件独立成库，这样可以更灵活自由的发展。 [#794](https://github.com/seajs/seajs/issues/794) [#780](https://github.com/seajs/seajs/issues/780)
3.  去除 `data-main`、`data-config` 等语法糖功能，保持简单纯粹。 [#753](https://github.com/seajs/seajs/issues/753)

2.1 版本之后，理论上 API 已固化，不会再有大的调整。

详见讨论贴：[#713](https://github.com/seajs/seajs/issues/713)

## 致谢

感谢 Sea.js 的每一个用户，正是你的关注、使用和建议，让 Sea.js 越来越好。

### 捐赠信息公布

Sea.js 社区从 1.3.1 开始，接受大家的捐助：

![通过支付宝捐赠](https://me.alipay.com/lifesinger)

Sea.js 目前的核心开发人员来自腾讯、阿里巴巴等公司，这是一个无公司界限的开源产品，开放而自由！

## 从 2.0 到 2.1 的 API 变化

### 模块

1.  define 重新支持 `define(id, factory)` 和 `define(deps, factory)` 这两种写法。 [#754](https://github.com/seajs/seajs/issues/754)
2.  define 上增加了 `define.cmd` 空对象，用来判定 CMD 模块加载器是否存在。 [#786](https://github.com/seajs/seajs/issues/786)
3.  module 上去除了 `module.destroy` 方法，要兼容的话，可以直接从 `seajs.cache` 和 `seajs.data.fetchedList` 中删除 `module.uri` 键值。

### 加载器

1.  去除了 `data-main` 和 `data-config` 的支持。 [#753](https://github.com/seajs/seajs/issues/753)
2.  去掉了 sea.js 的异步加载方式。[#733](https://github.com/seajs/seajs/issues/733)
3.  移除对循环依赖的支持。 [#732](https://github.com/seajs/seajs/issues/732)

### 插件

1.  所有插件独立成库。 [#794](https://github.com/seajs/seajs/issues/794) [#780](https://github.com/seajs/seajs/issues/780)
2.  config 中去掉了 `plugins`，统一使用 `preload` 来加载插件。
3.  去除 shim 插件。 [#744](https://github.com/seajs/seajs/issues/744)
4.  去掉了 `seajs.log` 方法，变成独立插件： [#815](https://github.com/seajs/seajs/issues/815)

如果是从 1.3 直接升级到 2.x，还可以看下这份文档： [#543](https://github.com/seajs/seajs/issues/543)

所有修改记录请参考：[`github.com/seajs/seajs/issues?milestone=11&page=1&state=closed`](https://github.com/seajs/seajs/issues?milestone=11&page=1&state=closed)