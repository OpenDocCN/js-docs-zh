# 模块的加载启动

Sea.js 是一个模块加载器，模块加载器需要实现两个基本功能：

1.  实现模块定义规范，这是模块系统的基础。
2.  模块系统的启动与运行。

### 模块定义规范的实现

这就是 `define`，`require`，`exports`，`module` 的实现。具体实现细节，有兴趣的可以看 Sea.js 的源码：[seajs/src](https://github.com/seajs/seajs/tree/master/src)。可以按照 [Gruntfile.js](https://github.com/seajs/seatools/blob/master/Gruntfile.js#L98) 中声明的合并顺序阅读，核心是 `module.js` 文件。

`define` 等方法的具体使用，请阅读：[CMD 模块定义规范](https://github.com/seajs/seajs/issues/242)

### 模块系统的启动

有了 `define` 等模块定义规范的实现，我们可以开发出很多模块。但光有一堆模块不管用，我们还得让它们能跑起来。

首先就是启动问题。比如在 Node 中，启动很简单：

```
$ node main.js 
```

这就是启动。

再举一个例子，操作系统的启动：大家都知道的，按一下开机键就好。

在 Sea.js 里，要启动模块系统很简单：

```
<script src="path/to/sea.js"></script>
<script>
 seajs.use('./main');
</script>
```

## seajs.use `Function`

用来在页面中加载模块。

### seajs.use `seajs.use(id, callback?)`

通过 `use` 方法，可以在页面中加载任意模块：

```
// 加载模块 main，并在加载完成时，执行指定回调
seajs.use('./main', function(main) {
  main.init();
});
```

`use` 方法还可以一次加载多个模块：

```
// // 并发加载模块 a 和模块 b，并在都加载完成时，执行指定回调
seajs.use(['./a', './b'], function(a, b) {
  a.init();
  b.init();
});
```

`callback` 参数可选，省略时，表示无需回调。

### 与 DOM ready 的关系

**注意**：`seajs.use` 与 `DOM ready` 事件没有任何关系。如果某些操作要确保在 `DOM ready` 后执行，需要使用 `jquery` 等类库来保证，比如：

```
seajs.use(['jquery', './main'], function($, main) {
  $(document).ready(function() {
    main.init();
  });
});
```

## sea.js 的引入

在调用 `seajs.use` 之前，需要先引入 `sea.js` 文件，推荐直接使用 `script` 标签同步引入：

```
<script src="path/to/sea.js"></script>
```

为了满足某些场景下的性能优化需求，也可以将 `sea.js` 的源码内嵌：

```
<script>
// sea.js 的源码
</script>
```

注意：代码内嵌时，需要通过 `seajs.config` 手动配置 `base` 路径。

## 最佳实践

1.  `seajs.use` 理论上只用于加载启动，不应该出现在 `define` 中的模块代码里。在模块代码里需要异步加载其他模块时，推荐使用 `require.async` 方法。

2.  引入 `sea.js` 时，可以把 `sea.js` 与其他文件打包在一起，可提前合并好，或利用 combo 服务动态合并。无论哪一种方式，为了让 `sea.js` 内部能快速获取到自身路径，推荐手动加上 `id` 属性：

```
<script src="path/to/sea.js" id="seajsnode"></script>
```

加上 `seajsnode` 值，可以让 `sea.js` 直接获取到自身路径，而不需要通过其他机制去自动获取。这对性能和稳定性会有一定提升，推荐默认都加上。

## 小结

`seajs.use` 是模块加载器必备的一个接口。在 `seajs` 上，还有用于配置的 `config` 方法、方便调试的 `cache` 等接口，这些会在接下来的文档中详细阐述。