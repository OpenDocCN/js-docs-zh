# 如何参与开发

Sea.js 的理念是海纳百川、有容乃大，非常欢迎大家一起参与开发。

## 阅读源码

要参于开发，还是得阅读下源码。
Sea.js 的源码采用了原始的模块化方式来组织，存放在 src 目录：[seajs/src](https://github.com/seajs/seajs/tree/master/src)

建议按照以下顺序阅读：

```
intro.js
sea.js

util-lang.js
util-events.js
util-path.js
util-request.js
util-deps.js

module.js
config.js

outro.js 
```

上面的文件在合并处理后，就是 `dist` 目录下的 `sea-debug.js` 文件，也可以直接阅读这个文件。`tests` 目录下存放的是测试集，很多疑惑可以在 `research` 和 `specs` 中找到答案。

遇到疑问时，可以通过 [社区](https://github.com/seajs/seajs/issues/271) 讨论交流。

## 贡献代码

建议通过 GitHub fork 一份 Sea.js 项目的源码，然后 `git clone` 到本地阅读。

1.  在阅读源码过程中，发现某些地方能优化时，请毫不犹豫修改之。
2.  修改代码后，运行 `make build` 命令进行构建。
3.  构建好后，浏览器中打开 `tests/runner.html` 进行测试，确保修改的代码不会影响既有功能。

一切 OK 后，提交代码到 GitHub 上，并发 `Pull Request` 给我们。

对于优秀的 `Pull Request`，我们会毫不犹豫 merge 之，这样你就能成为 Sea.js 的贡献者，你的名字将永远留在贡献者列表里：[Contributors](https://github.com/seajs/seajs/graphs/contributors)

* * *

欢迎参与，期待精彩。