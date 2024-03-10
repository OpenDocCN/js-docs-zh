# 2.1.1

Sea.js `2.1.0` 的发布文档：[#813](https://github.com/seajs/seajs/issues/813)

Sea.js 2.1.0 发布后，很多用户已直接升级。根据用户的使用反馈，做了一些修改：

### BUG 修复

*   require.resolve 参数为目录时结果有误 [#839](https://github.com/seajs/seajs/issues/839)
*   require 一个未提取到依赖参数中的 id 时，直接报错 [#824](https://github.com/seajs/seajs/issues/824)

### 改进增强

*   为性能优化 resolve 提供接口[#818](https://github.com/seajs/seajs/issues/818) [#833](https://github.com/seajs/seajs/issues/833) [#821](https://github.com/seajs/seajs/pull/821)

### 讨论

*   是否需要 Sea.js 精简版 [#834](https://github.com/seajs/seajs/issues/834)

### 插件升级

*   seajs-text 插件升级到 1.0.1 版本，修复 BUG： [seajs/seajs-text#2](https://github.com/seajs/seajs-text/issues/2)
*   seajs-flush 插件升级到 1.0.1 版本，修复 BUG： [seajs/seajs-flush#9](https://github.com/seajs/seajs-flush/issues/9) [seajs/seajs-flush#10](https://github.com/seajs/seajs-flush/issues/10) [seajs/seajs-flush#11](https://github.com/seajs/seajs-flush/pull/11)

## 下载更新

推荐通过 spm 下载最新版本：

```js
$ spm install seajs
$ spm install seajs/seajs-text
$ spm install seajs/seajs-flush 
```

有任何问题，欢迎反馈。