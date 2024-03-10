# 1.2.1

[SeaJS v1.3 开发规划](https://github.com/seajs/seajs/issues/225) 中涉及的内容需要到 9 月份才能全部开发完毕，在这过程中，已经做了不少改进和 bug fix，其中有几项特别是 bug fix 非常值得立刻升级。因此先发布 1.2.1 版本，主要修改点如下：

### 插件

*   ✔ [#224](https://github.com/seajs/seajs/issues/224) 页面自动刷新：plugin-reload 插件
*   ✔ [#323](https://github.com/seajs/seajs/issues/323) 多语言支持：plugin-i18n 插件

### 优化增强

*   ✔ [#286](https://github.com/seajs/seajs/issues/286) 直接调用 jQuery 插件等非标准模块的方法
*   ✔ [#311](https://github.com/seajs/seajs/issues/311) firstModuleInPackage 代码逻辑优化
*   ✔ [#319](https://github.com/seajs/seajs/issues/319) 通过 URL 或 cookie 来自动加载插件并传参
*   ✔ [#294](https://github.com/seajs/seajs/issues/294) debug 模式下的断点调试问题
*   ✔ [#285](https://github.com/seajs/seajs/issues/285) combo 插件增加 comboExcludes 配置
*   ✔ [#263](https://github.com/seajs/seajs/issues/263) seajs.find 返回结果调整为始终返回数组

### bug fix

*   ✔ [#304](https://github.com/seajs/seajs/issues/304) 在低网速下，某些特殊使用场景时，部分模块会重复初始化
*   ✔ [#317](https://github.com/seajs/seajs/issues/317) 有 alias 存在时，plugin-base 的 id 解析问题

推荐立刻升级：[下载](http://seajs.org/docs/#downloads)