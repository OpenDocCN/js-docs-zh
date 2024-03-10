# 与 OzJS 的探讨

1.  源码中 `forEach` 的实现，以及 `m.deps.forEach` 的用法，使得 OzJS 在 IE9 以下无法运行。是有意不支持 Old IE？如果不需要考虑 IE6-8，则 32 行的代码可以省略掉，在文档中说明就好。只支持高级浏览器的话，代码应该还可以简化。

2.  有个建议，文档上将 AMD 公共模块称呼为 AMD 具名模块，AMD 私有模块称呼为 AMD 匿名模块，这样可能更表意，呵呵。另外，对于 AMD 私有模块，模块 url 的获取，是通过串行加载来保证拿到的 url 是当前 define 的？没仔细看代码，想求证下。如果是串行的话，当开发时私有模块超过 20 多个时，豆瓣内部是怎么缩短模块加载时间的？（之前在淘宝遇到了这个问题，SeaJS 中改成并行才解决，但并行导致代码有些 hacky，不爽）

3.  异步模块的支持挺有意思，但感觉有悖模块加载器的本职工作。个人觉得模块加载器不应该涉及异步等待逻辑。如果需要等待，可以调整依赖来解决。

4.  远程模块的设计，个人觉得让 define 承担了不应该承担的职责。比如

    ```
    define("a", ["path/to/b.js"], "path/to/a.js")
    // 干了两件事情：
    // 给模块 a 动态添加了依赖 b
    // 声明模块 a 的路径是 path/to/a.js
    ```

    上面两件事情，是否通过 config 来配置会更明确？比如

    ```
    require.config({
      aliases: {
         "a": "path/to/a.js"
      },

      deps: {
         "a": ["path/to/b.js"]
      }
    })
    ```

    在 SeaJS 里，通过增加 shim 配置来实现，比如

    ```
    seajs.config({
     plugins: ["shim"], // 激活 shim 插件，有这个插件 shim 配置才生效

    shim: {
        // jQuery 的 shim 配置
        'jquery': {
          exports: function() { return jQuery; }
        },

        // jQuery 插件的 shim 配置
        'jquery-plugins': {
            match: /jquery\.[a-z].*\.js/, // 匹配所有 jquery 插件，自动化
            deps: ['jquery'], // 动态指定依赖
            exports: 'jQuery' 
        }
    }
    })
    ```

    shim 配置的方式，功能和 OzJS 的远程模块类似，但在批量处理上，感觉更方便些，比如上面 jquery-plugins 的声明方式，只要命名规则为 jquery.xxx.js 的插件，都自动添加好了依赖，使用上，直接 require 真实路径或 alias 就好。RequireJS 2.0 里，也是类似的处理方式。

5.  从源码上看，OzJS 中的 `require` 也是身兼多职。这是我一直很难接受 RequireJS 的重要原因之一。为什么不职责单一一些？全局中的 require 跟 参数中的 require 应该不一样，就像 NodeJS 中的 require 一样，每个模块的 require 是私有的，是有上下文环境的，这样相对路径的解析也更合理。可能是个人喜好，如有冒犯，请忽略。

6.  `new!` 挺有意思，赞。

7.  mo 里面的模块挺小巧实用的，和 Arale 的理念异曲同工，呵呵。有个小疑问，mo 的模块 id 都是固定的，比如 `mo/cookie`，这样，当 cookie 版本升级时，如果是一个老页面，有些功能点依赖 cookie 的老版本，但新功能点想依赖 cookie 的新版本，这种情况下，OzJS 里是如何处理的？Arale 里给每个模块都加了版本，比如 `arale/cookie/1.2.0/cookie` 这种方式，这样两个不同版本的 cookie，可以认为是完全两个不同的模块，因此可以并存。想知道豆瓣这一块是如何处理。

8.  建议 mo 里的模块可以每个模块一个独立库，这样通过简单的 transport 工具，可以和 Arale 的组件互通起来。对于生态圈，也想听听 [@dexteryy](https://github.com/dexteryy) 的想法。

先说这些，希望能对 [@dexteryy](https://github.com/dexteryy) 有所帮助，祝 Oz 能越来越好。

玉伯 / Feb 20, 2013