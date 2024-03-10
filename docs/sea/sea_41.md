# 2.3.0

对当前页面的模块和模块关系感到混乱？模块依赖图插件轻松一点让你一目了然！

![preview](img/b0e98e8b42b1495adc7fb0a203eb50c6.jpg)

只需在 chrome 上安装一个插件，就可以绘制出有向图，模块根路径、列表、名称、依赖关系尽收眼底。

相对于上个版本，Sea.js 的体积又有进一步缩减，这一切归功于将 css 功能部分提取出作为一个插件存在。

*   Sea.js 2.2

    > sea-debug.js 20,671 bytes
    > sea.js 6,769 bytes
    > gzip 3.0 KB
    > LOC 947

*   Sea.js 2.3

    > sea-debug.js 18,177 bytes
    > sea.js 6,064 bytes
    > gzip 2.8 KB
    > LOC 846

测试用例增加到了`505`个！这一切都保障了 Sea.js 拥有十分强大的健壮性。

### 下载更新

推荐使用 [spm](http://spmjs.io)

```
spm install seajs
npm install seajs 
```

### BUG 修复

*   IE9 下本地 url document.URL 与之前版本使用的 location.href 输出不一致导致模块 id 不能正确 resolve [#1154](https://github.com/seajs/seajs/issues/1154)
*   Android 中的 webview 当 location.href 为空时报错 [#1225](https://github.com/seajs/seajs/issues/1225)
*   realpath method in util-path.js：[#1193](https://github.com/seajs/seajs/pull/1193)

### 移除特性

*   去掉 css 支持，推荐 link 标签同步引入。如果实在要用，可以用 seajs-css 插件来完成。
*   preload 移除，推荐 script 标签同步引入。如果实在要用，可以用 seajs-preload 插件来完成。
*   去掉根据 sea.js 路径自动猜测 base 路径的功能。交给用户自己配置。
*   CommonJS 规范书写，这其实是 spm3 的功能：[spmjs/spm#819](https://github.com/spmjs/spm/issues/819)

> [`spmjs.io`](http://spmjs.io)

### 改进增强

*   seajs-css 插件：[`github.com/seajs/seajs-css`](https://github.com/seajs/seajs-css)
*   seajs-preload 插件：[`github.com/seajs/seajs-preload`](https://github.com/seajs/seajs-preload)
*   seajs-circular 插件，支持循环依赖：[`github.com/seajs/seajs-circular`](https://github.com/seajs/seajs-circular)
*   seamap 插件，模块依赖图，绘制出当前页面上的模块和依赖关系图：[`github.com/seajs/seamap`](https://github.com/seajs/seamap)

> 插件目前分为 2 种：1 是 seajs 插件，以 seajs-xxx 形式命名；2 是开发者工具，以 seaxxx 命名。

### 其它调整

*   模块保存时增加了 save 事件
*   细微的性能改进
*   CommonJS/AMD/CMD/Other 脚本之间的互相转换：[`github.com/army8735/ranma`](https://github.com/army8735/ranma)
*   pass-entry 分支中尝试启用新算法，在体积不变的情况原生支持循环依赖。由于取消了回溯，初始化性能也提升了一倍
*   构建工具 seatools 更新部分 bug：[`github.com/seajs/seatools`](https://github.com/seajs/seatools)
*   增加了英文文档：[`seajs.org/docs/en.html`](http://seajs.org/docs/en.html)
*   同步发布 spm3：[spmjs/spm#819](https://github.com/spmjs/spm/issues/819)

有任何问题，欢迎反馈。