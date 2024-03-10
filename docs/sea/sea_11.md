# 构建工具

## 标准构建

> spm3 已经发布，建议使用最新的构建工具。[`spmjs.io/documentation/develop-a-package#build`](http://spmjs.io/documentation/develop-a-package#build)

* * *

如果项目遵循推荐的标准目录结构：

```js
foo-module/
  |-- dist                    存放构建好的文件
  |-- src                     存放 js、css 等源码
  |     |-- foo.js
  |     `-- style.css
  `-- package.json      模块信息 
```

那么构建很简单。首先安装 spm 工具（spm2）：

```js
$ npm install spm@2.x -g
$ npm install spm-build@0.x -g 
```

然后运行构建命令：

```js
$ cd foo-module
$ spm build 
```

这样，就会根据 `package.json` 中的信息，将文件自动构建到 `dist` 目录下。构建后，还需要将 dist 目录下的文件部署到 `sea-modules` 目录中，比如 examples 中的 `make deploy` 命令：[Makefile](https://github.com/seajs/examples/blob/master/static/hello/Makefile)

详细可参考 [`docs.spmjs.org/`](http://docs.spmjs.org/)

推荐将 [seajs/examples](https://github.com/seajs/examples) clone 到本地，实际操作一下就清楚。

## 自定义构建

如果标准构建无法满足需求，可以直接使用 Grunt 来完成。Grunt 是一个非常优秀的构建工具，详见：[`gruntjs.com/`](http://gruntjs.com/)

利用 Grunt 来构建 CMD 模块需要使用到以下 Grunt Tasks：

*   [grunt-cmd-transport](https://github.com/spmjs/grunt-cmd-transport)
*   [grunt-cmd-concat](https://github.com/spmjs/grunt-cmd-concat)

这一块真的很简单，只要你熟悉 Grunt，因此先阅读 Grunt 的文档吧，然后有任何问题，欢迎回复。

推荐几篇社区贡献的文章：

*   [CMD 模块构建，从认识 Grunt 开始](https://github.com/seajs/seajs/issues/670)
*   [如何使用 Grunt 构建一个中型项目](https://github.com/seajs/seajs/issues/672)
*   [使用 spm 构建业务模块的个人经验](https://github.com/seajs/seajs/issues/690)

非常欢迎大家的使用经验总结。

* * *

有任何问题，欢迎留言交流。
注意：已解决的问题，会在整理后删除掉。