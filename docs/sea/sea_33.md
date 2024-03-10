# 与 Require.JS 的异同

## 相同之处

RequireJS 和 Sea.js 都是模块加载器，倡导模块化开发理念，核心价值是让 JavaScript 的模块化开发变得简单自然。

## 不同之处

两者的主要区别如下：

1.  **定位有差异**。RequireJS 想成为浏览器端的模块加载器，同时也想成为 Rhino / Node 等环境的模块加载器。Sea.js 则专注于 Web 浏览器端，同时通过 Node 扩展的方式可以很方便跑在 Node 环境中。

2.  **遵循的规范不同**。RequireJS 遵循 AMD（异步模块定义）规范，Sea.js 遵循 CMD （通用模块定义）规范。规范的不同，导致了两者 API 不同。Sea.js 更贴近 CommonJS Modules/1.1 和 Node Modules 规范。

3.  **推广理念有差异**。RequireJS 在尝试让第三方类库修改自身来支持 RequireJS，目前只有少数社区采纳。Sea.js 不强推，采用自主封装的方式来“海纳百川”，目前已有较成熟的封装策略。

4.  **对开发调试的支持有差异**。Sea.js 非常关注代码的开发调试，有 nocache、debug 等用于调试的插件。RequireJS 无这方面的明显支持。

5.  **插件机制不同**。RequireJS 采取的是在源码中预留接口的形式，插件类型比较单一。Sea.js 采取的是通用事件机制，插件类型更丰富。

还有不少差异，涉及具体使用方式和源码实现，欢迎有兴趣者研究并发表看法。

总之，如果说 RequireJS 是 Prototype 类库的话，则 Sea.js 致力于成为 jQuery 类库。

## 最重要的

最后，向 RequireJS 致敬！RequireJS 和 Sea.js 是好兄弟，一起努力推广模块化开发思想，这才是最重要的。

## 更新

*   2013.06.30 推荐一篇图片并茂的文章：[Sea.js 与 RequireJS 最大的区别](http://www.douban.com/note/283566440/)

## 参考

*   [LABjs、RequireJS、Sea.js 哪个最好用？为什么？](http://www.zhihu.com/question/20342350)
*   从 RequireJS 到 Sea.js 系列：[（1）](http://lifesinger.wordpress.com/2011/10/30/comparing-requirejs-with-seajs-1/) [（2）](http://lifesinger.wordpress.com/2011/10/30/comparing-requirejs-with-seajs-2/) [（3）](http://lifesinger.wordpress.com/2011/10/30/comparing-requirejs-with-seajs-3/) [（4）](http://lifesinger.wordpress.com/2011/10/30/comparing-requirejs-with-seajs-4/) [（5）](http://lifesinger.wordpress.com/2011/10/30/comparing-requirejs-with-seajs-5/) （要翻墙）
*   [Sea.js 和 RequireJS 的异同](http://lifesinger.wordpress.com/2011/05/17/the-difference-between-seajs-and-requirejs/)（要翻墙）
*   [AMD 与 CMD 的区别](http://www.zhihu.com/question/20351507)