# 安装

Koa 目前需要 >=0.11.x 版本的 node 环境。并需要在执行 node 的时候附带 --harmony 来引入 generators 。 如果您安装了较旧版本的 node ，您可以安装 [n](https://github.com/visionmedia/n) (node 版本控制器)，来快速安装 0.11.x

```js
$ npm install -g n
$ n 0.11.12
$ node --harmony my-koa-app.js 
```