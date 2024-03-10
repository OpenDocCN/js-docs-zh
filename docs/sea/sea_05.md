# 模块系统

## 什么是系统

在生活和工作中，我们会接触到大量系统：自然界生态系统、计算机操作系统、软件办公系统，还有教育系统、金融系统、网络系统、理论系统等等。究竟什么是系统呢？

来看下维基百科的解释：

> 系统泛指由一群有关连的个体组成，根据预先编排好的规则工作，能完成个别元件不能单独完成的工作的群体。系统分为自然系统与人为系统两大类。

简言之，系统有两个基本特性：

1.  系统由个体组成。
2.  个体之间有关连，按照规则协同完成任务。

系统中的个体可称之为系统成员，这样，要构建一个系统，最基本层面需要做两件事：

1.  **定义系统成员**：确定成员是什么。
2.  **约定系统通讯**：确定成员之间如何交互，遵循的规则是什么。

只要把这两个问题描述清楚，我们就可以构建出系统。

## 模块系统

Sea.js 是一个适用于 Web 浏览器端的模块加载器。在 Sea.js 里，一切皆是模块，所有模块协同构建成模块系统。Sea.js 首要要解决的是模块系统的基本问题：

1.  模块是什么？
2.  模块之间如何交互？

在前端开发领域，一个模块，可以是 JS 模块，也可以是 CSS 模块，或是 Template 等模块。在 Sea.js 里，我们专注于 JS 模块（其他类型的模块可以转换为 JS 模块）：

1.  模块是一段 JavaScript 代码，具有统一的基本书写格式。
2.  模块之间通过基本交互规则，能彼此引用，协同工作。

把上面两点中提及的基本书写格式和基本交互规则描述清楚，就能构建出一个模块系统。对书写格式和交互规则的详细描述，就是模块定义规范（Module Definition Specification）。比如 CommonJS 社区的 [Modules 1.1.1](http://wiki.commonjs.org/wiki/Modules) 规范，以及 NodeJS 的 [Modules](http://nodejs.org/api/modules.html) 规范，还有 RequireJS 提出的 [AMD](https://github.com/amdjs/amdjs-api/wiki/AMD) 规范等等。

Sea.js 遵循的是 [CMD](https://github.com/cmdjs/specification/blob/master/draft/module.md) 规范，会在接下来的文档中详细阐述。

## 延伸阅读

*   [function / bind 的救赎](http://blog.csdn.net/myan/article/details/5928531)
*   [继承与混合，略谈系统的构建方式](http://blog.csdn.net/aimingoo/article/details/6062997)