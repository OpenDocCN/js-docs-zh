# 插件开发指南

Sea.js 通过事件提供可扩展接口。要给 Sea.js 开发插件，需要了解 Sea.js 内部所提供的事件类型。

## 事件机制

Sea.js 内置了一个非常小巧的 Pub-Sub 机制。API 简要如下：

### seajs.on `seajs.on(event, callback)`

用来添加事件回调。

```js
// 给 fetch 事件添加一个回调
seajs.on('fetch', function(data) {
  ...
});
```

### seajs.off `seajs.off(event?, callback?)`

用来移除事件回调。

```js
// 从 fetch 事件的回调中移除掉 fn 函数
seajs.off('fetch', fn);

// 移除掉 fetch 事件的所有回调
seajs.off('fetch');

// 移除掉所有事件的所有回调
seajs.off();
```

### seajs.emit `seajs.emit(event, data)`

用来触发事件。

```js
// 触发 fetch 事件
seajs.emit('fetch', { uri: uri, fetchedList: fetchedList });
```

利用以上三个方法，我们就可以给 Sea.js 添加事件来实现扩展了。

### 事件类型

Sea.js 内部提供了 8 种事件。

```js
resolve       -- 将 id 解析成为 uri 时触发
load          -- 开始加载文件时触发
fetch         -- 具体获取某个 uri 时触发
request       -- 发送请求时触发
define         -- 执行 define 方法时触发
exec         -- 执行 module.factory 时触发
config         -- 调用 seajs.config 时触发
error          -- 加载脚本文件出现 404 或其他错误时触发 
```

每个事件触发时会带上相关联的数据，比如

```js
  // Emit `fetch` event for plugins such as plugin-combo
  var data = { uri: uri }
  emit("fetch", data)
```

上面是触发 `fetch` 事件的源码。订阅的 `callback` 回调会接受到 data 参数：

```js
seajs.on('fetch', function(data) {
  if (data.uri) {
    data.requestUri = data.uri + '?t=' + new Date().getTime()
  }
});
```

上面就实现了一个最简单的 nocache 插件。

每一个事件发送的具体数据参数，请在源码中用事件名搜索相关代码就好。

## 内部数据与方法

### seajs.data `Object`

通过 `data` 接口，你几乎可以获取了 Sea.js 内部的所有配置数据和核心内部数据。

### seajs.Module `Object`

通过 `Module` 接口，你几乎可以获取了 Sea.js 内部的所有核心方法。

有了 `data` 和 `Module`，以及前面的事件接口，插件开发者就可以开发出各种插件了。推荐访问 [`github.com/seajs`](https://github.com/seajs) 查看所有插件。看一两个插件的源码后，我相信你很快也就能开发出自己的插件。

## 插件的加载方式

[#794](https://github.com/seajs/seajs/issues/794)

## 小结

事件机制非常灵活。如果在实际使用中发现有什么不妥，欢迎提供建议一起来完善。