# 2.2.0

> Sea.js `2.1.1` 的发布文档：[#842](https://github.com/seajs/seajs/issues/842)

经过一段时间的积累，如今 Sea.js 发布 2.2.0 版本。主要在插件工具和 SourceMap 方面进行改进。

### 下载更新

推荐使用 spm

```
spm install seajs
npm install seajs 
```

### 独立的构建测试工具

*   seatools 工具主页 [`github.com/seajs/seatools`](https://github.com/seajs/seatools)
*   说明 [#924](https://github.com/seajs/seajs/issues/924)

全局安装

```
npm install seatools -g 
```

插件测试需要和 seajs 目录保持同级。

### 插件升级

*   seajs-debug 1.1.1 [`github.com/seajs/seajs-debug`](https://github.com/seajs/seajs-debug)
*   seajs-text 1.0.2 [`github.com/seajs/seajs-text`](https://github.com/seajs/seajs-text)
*   seajs-style 1.0.2 [`github.com/seajs/seajs-style`](https://github.com/seajs/seajs-style)
*   seajs-log 1.0.1 [`github.com/seajs/seajs-log`](https://github.com/seajs/seajs-log)
*   seajs-flush 1.0.1 [`github.com/seajs/seajs-flush`](https://github.com/seajs/seajs-flush)
*   seajs-combo 1.0.1 [`github.com/seajs/seajs-combo`](https://github.com/seajs/seajs-combo)
*   seajs-health 0.1.1 [`github.com/seajs/seajs-health`](https://github.com/seajs/seajs-health)

### BUG 修复

*   IE10 中 iframe 下缓存导致模块加载失败 [#917](https://github.com/seajs/seajs/issues/917)
*   base url 协议问题 [#927](https://github.com/seajs/seajs/issues/927)

### 移除特性

*   去除对 source map 的支持 [#919](https://github.com/seajs/seajs/issues/919)

### 改进增强

*   允许 paths 以 "/" 字符结尾 [#926](https://github.com/seajs/seajs/issues/926)
*   seajs.require 功能增强 [#944](https://github.com/seajs/seajs/issues/944)

### 其它调整

*   将 request 方法也暴露出来 [#945](https://github.com/seajs/seajs/issues/945)
*   调整 error 事件的触发时机（非向下兼容） [#921](https://github.com/seajs/seajs/issues/921)

### 增加文档

*   如何改造现有文件为 CMD 模块 [#971](https://github.com/seajs/seajs/issues/971)
*   ID 和路径匹配原则 [#930](https://github.com/seajs/seajs/issues/930)

### 讨论

*   Sea.js 3.0 想法探讨 [#1060](https://github.com/seajs/seajs/issues/1060)
*   可否支持 index.js [#939](https://github.com/seajs/seajs/issues/939)

### 3.0 规划

*   开发时只支持 Chrome / Firefox 等现代浏览器，不支持 IE6-8\. 需要在 Old IE 下运行的话，需要先构建，生成 id 和 deps 后才能在 IE 下正常运行。
*   去掉 preload 功能。需要 preload 的组件，建议直接用 script 同步引入。preload 的初衷，是希望通过异步并行下载提高性能，但在非 IE 下，这种异步带来的性能优化已不明显。在移动端更意义不大。
*   细节调整：去掉根据 sea.js 路径自动猜测 base 路径的功能。交给用户自己配置。
*   去掉对老旧版本 Safari 和 Firefox 中，加载 css 的支持。目前针对这种场景保留着一些兼容代码。
*   CommonJS 规范书写，和 NodeJS 保持一致，构建后或调试时分析包裹 define。
*   考虑循环依赖的设计实现。

有任何问题，欢迎反馈。