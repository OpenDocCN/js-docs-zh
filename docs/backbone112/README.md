# Backbone.js(1.1.2) API 中文文档

> 来源：[Backbone.js(1.1.2) API 中文文档](http://www.css88.com/doc/backbone)

![Backbone.js](img/backbone.png)

### 文档声明：

*   根据官方最新的 1.1.2 版本做了翻译
*   Backbone.js (0.5.3)文档请移步[`www.css88.com/doc/backbone-0.5.3/`](http://www.css88.com/doc/backbone-0.5.3/)；
*   翻译水平有限，如果您有任何建议，或者拍砖，欢迎在微博上[@愚人码头](http://weibo.com/148246293) 联系我。

Backbone.js 为复杂 WEB 应用程序提供模型(**models**)、集合(**collections**)、视图(**views**)的结构。其中模型用于绑定键值数据和自定义事件；集合附有可枚举函数的丰富 API； 视图可以声明事件处理函数，并通过 RESRful JSON 接口连接到应用程序。

此项目托管在 [GitHub](http://github.com/jashkenas/backbone/) 上, 并且提供 带注释的源码, 在线的 测试套件, 应用示例, [教程列表](https://github.com/jashkenas/backbone/wiki/Tutorials%2C-blog-posts-and-example-sites) 还有一个 实际应用项目的超长列表, 这些项目都使用了 Backbone. Backbone 允许在 [MIT 软件协议](http://github.com/jashkenas/backbone/blob/master/LICENSE) 下使用.

你可以在[GitHub issues 页面](http://github.com/jashkenas/backbone/issues)及`#documentcloud`频道下的 Freenode IRC 中 报告 bug 和 讨论功能, 在[Google Group](https://groups.google.com/forum/#!forum/backbonejs)合[wiki](https://github.com/jashkenas/backbone/wiki)页面中提出问题，或在 twitter 上 [@documentcloud](http://twitter.com/documentcloud)。

*Backbone 是 [DocumentCloud](http://documentcloud.org/) 的一个开源组件.*

### 下载&依赖 (右键另存为)

|  |  |
| --- | --- |
| [开发版本 (1.1.2)](http://www.css88.com/doc/backbone/backbone.js) | *60kb, 完整的源代码，大量的注释* |
| [生产版本 (1.1.2)](http://www.css88.com/doc/backbone/backbone-min.js) | *6.5kb, 打包和 gzip 压缩* (Source Map) |
| [Edge Version (master)](https://raw.github.com/jashkenas/backbone/master/backbone.js) | *未发布版本,使用风险自负* ![](https://travis-ci.org/jashkenas/backbone) |

Backbone 唯一重度依赖的是[Underscore.js](http://www.css88.com/doc/underscore/)( >= 1.5.0)（愚人码头注：Underscore.js 中文文档请查看 [`www.css88.com/doc/underscore/`](http://www.css88.com/doc/underscore/)）。基于 RESTful（一个架构样式的网络系统）的约束，histroy 的支持依赖于 Backbone.Router ，DOM 处理依赖于 Backbone.View，包括**[jQuery](http://jquery.com)** ( >= 1.11.0), 和 **[json2.js](https://github.com/douglascrockford/JSON-js)**对旧的 IE 浏览器的支持。*（模仿 Underscore 和 jQuery 的 APIs，例如 [Lo-Dash](http://lodash.com) 和 [Zepto](http://zeptojs.com)，在不同的兼容性下也一样能运行）*