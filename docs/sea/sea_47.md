# 1.3.0

✔ 已完成 ➠ 进行中

该版本主要是优化增强，核心更加稳定、健壮。
理论上可以从 1.2 直接升级，强烈推荐升级。

文档：[seajs.org](http://seajs.org/docs/?20121113)
下载：[seajs.org/docs/#downloads](http://seajs.org/docs/?20121113#downloads)

* * *

### 新增插件

*   ✔ [#224](https://github.com/seajs/seajs/issues/224) 自动刷新插件 reload
*   ✔ [#323](https://github.com/seajs/seajs/issues/323) 多语言支持插件 i18n
*   ✔ [#352](https://github.com/seajs/seajs/issues/352) 警告提示插件 warning

### 优化增强

*   ✔ [#286](https://github.com/seajs/seajs/issues/286) 直接调用 jQuery 插件等非标准模块的方法
*   ✔ [#319](https://github.com/seajs/seajs/issues/319) 通过 URL 或 cookie 来自动加载插件并传参
*   ✔ [#294](https://github.com/seajs/seajs/issues/294) debug 模式下的断点调试问题
*   ✔ [#386](https://github.com/seajs/seajs/pull/386) preload 的限制放宽说明
*   ✔ [#285](https://github.com/seajs/seajs/issues/285) combo 插件增加 comboExcludes 配置
*   ✔ [#263](https://github.com/seajs/seajs/issues/263) seajs.find 返回结果调整为始终返回数组
*   ✔ [#348](https://github.com/seajs/seajs/issues/348) 去掉 "It is not a vailid CMD module" 的 console 提示
*   ✔ [#311](https://github.com/seajs/seajs/issues/311) firstModuleInPackage 代码逻辑优化

### bug fix

*   ✔ [#304](https://github.com/seajs/seajs/issues/304) 在低网速下，某些特殊使用场景时，部分模块会重复初始化
*   ✔ [#317](https://github.com/seajs/seajs/issues/317) 有 alias 存在时，plugin-base 的 id 解析有问题
*   ✔ [#353](https://github.com/seajs/seajs/pull/353) Fix loaderScript bug in PhantomJS
*   ✔ [#349](https://github.com/seajs/seajs/issues/349) [#343](https://github.com/seajs/seajs/issues/343) [#332](https://github.com/seajs/seajs/issues/332) seajs.log 在 IE 下报错，并且与 console 不全等
*   ✔ [#342](https://github.com/seajs/seajs/issues/342) 在 IE 下，当 map 映射中有相对路径时，在 IE 下加载有问题

### 文档与社区

*   ✔ [#324](https://github.com/seajs/seajs/issues/324) 发布 SeaJS v1.2.1
*   ✔ [#291](https://github.com/seajs/seajs/issues/291) SeaJS 使用经验交流之有奖活动一期
*   ✔ [#377](https://github.com/seajs/seajs/issues/377) 文档梳理与优化

所有 issues 列表：[milestone issues](https://github.com/seajs/seajs/issues?milestone=8&page=1&state=closed)

### 取消不做的事项

*   [#167](https://github.com/seajs/seajs/issues/167) 小巧简洁的 runtime 版本（性价比不高）
*   [#280](https://github.com/seajs/seajs/issues/280) node 端的 seajs 支持 coffee script（暂时不做，需求不高）
*   [#316](https://github.com/seajs/seajs/issues/316) Wind.js 异步编程：plugin-wind 插件（等 Wind.js 下一个正式版本）
*   [#121](https://github.com/seajs/seajs/issues/121) 具有直接编辑功能的 plugin-debug（需求不高）
*   [#239](https://github.com/seajs/seajs/issues/239) 优化 test runner 页面，改成并发（目前不是问题）

### 预期时间

*   ✔ 8 月 15 日发布 1.2.1
*   ✔ 11 月 13 日发布 1.3.0