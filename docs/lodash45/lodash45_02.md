# 版本定制

# 版本定制

通过版本定制可以很轻松的定制仅包含你所需功能的 lodash 版本 。更棒的是，我们已经帮你处理好了函数依赖和别名对应，查看 [版本区别](https://github.com/lodash/lodash/wiki/build-differences) & 选择一个适合你的版本。

使用 Grunt? 我们准备了 [Grunt plugin](https://npmjs.org/package/grunt-lodash) 协助构建 lodash。

安装 [lodash-cli](https://npmjs.org/package/lodash-cli) 来作为 `lodash` 全局命令行工具:

```
$ {sudo -H} npm i -g npm
$ {sudo -H} npm i -g lodash-cli
$ lodash -h 
```

**注意:** 请先卸载旧版本，再安装 `lodash-cli`。

*   兼容版本构建，同时支持新旧运行环境，使用 `compat` 修饰。 *(默认)*

```
lodash compat 
```

*   现代版本构建，针对新的环境，包括 [ES5](https://es5.github.io/)/ES6 支持，使用 `modern` 修饰。

```
lodash modern 
```

*   严格模式版本构建, 开启 [ES 严格模式](https://es5.github.io/#C)，使用 `strict` 修饰。

```
lodash strict 
```

*   模块化版本构建，拆散 lodash 为各个模块，使用 `modularize` 修饰。

```
lodash modularize 
```

构建命令:

*   使用 `category` 命令以逗号分隔的方式传入需要的函数分类。可用的函数分类有： *“array”*, *“chain”*, *“collection”*, *“date”*, *“function”*, *“lang”*, *“object”*, *“number”*, *“string”*, & *“utility”*=。

```
lodash category=collection,function 
```

*   使用 `exports` 命令以逗号分隔的方式传入导出 `lodash` 函数的方式，可用的方式有： *“amd”*, *“commonjs”*, *“es”*, *“global”*, *“iojs”*, *“node”*, *“npm”*, *“none”*, & *“umd”*.

```
lodash exports=amd,commonjs,iojs 
```

*   使用 `iife` 命令指定代码替换 包裹 lodash 的 [IIFE](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)。

```
lodash iife="!function(window,undefined){%output%}(this)" 
```

*   使用 `include` 命令以逗号分隔的方式传入需要包含的函数。

```
lodash include=each,filter,map 
```

*   使用 `minus` 命令以逗号分隔的方式传入需要删减的函数/分类。

```
lodash modern minus=result,shuffle 
```

*   使用 `plus` 命令以逗号分隔的方式传入需要补充的函数/分类。

```
lodash category=array plus=random,template 
```

*   使用 `template` 命令传入路径相匹配的文件生成预编译模板。 **注意:** 预编译模板分配在 `_.templates` 对象上。

```
lodash template="./*.jst" 
```

*   使用 `settings` 命令设置预编译模板时的模板语法。

```
lodash settings="{interpolate:/\{\{([\s\S]+?)\}\}/g}" 
```

*   使用 `moduleId` 命令指定 lodash 的 AMD module ID 或 包含 lodash 的编译模板的 module ID。指定为 `none` 表示创建编译模板不依赖 lodash。

```
lodash moduleId=underscore 
```

**注意:**

*   所有命令可以组合（除了 `compat` & `modern`）
*   `exports` 的值 *“es”* & *“npm”* 只能与 `modularize` 命令联用。
*   `modularize` 命令使用最先的 `exports` 的值作为模块格式，忽略后续的值。
*   除非指定 `-o` 或 `--output`，不然所有文件会保存在当前工作目录。
*   Node.js 0.10.8-0.10.11 [存在](https://github.com/joyent/node/issues/5622) [bugs](https://github.com/joyent/node/issues/5688) 导致无法最小化构建。

另外还支持以下选项：

```
-c, --stdout .......... 输出到 stdout(译注：类似直接输出在终端那样)
-d, --development ..... 输出非最小化的开发代码
-h, --help ............ 显示帮助信息
-m, --source-map ...... 生成 source-map 文件
-o, --output .......... 指定输出的路径/文件名
-p, --production ...... 输出最小化后的产品代码
-s, --silent .......... 不显示常规的日志输出
-V, --version ......... 显示当前的 lodash 版本号 
```