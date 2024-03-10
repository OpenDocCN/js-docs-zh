# Sea.js 的调试接口

使用 Sea.js，无论开发时还是上线后，调试都很方便。下面一一阐述。

## seajs.cache `Object`

通过 `seajs.cache`，可以查阅当前模块系统中的所有模块信息。

比如，打开 [seajs.org](http://seajs.org/)，然后在 WebKit Developer Tools 的 Console 面板中输入 `seajs.cache`，可以看到：

```
Object
  > http://seajs.org/docs/assets/main.js: x
  > https://a.alipayobjects.com/jquery/jquery/1.10.1/jquery.js: x
  > __proto__: Object 
```

这些就是文档首页用到的模块。展开某一项可以看到模块的具体信息，含义可参考：[CMD 模块定义规范](https://github.com/seajs/seajs/issues/242) 中的 module 小节。

## seajs.resolve `Function`

类似 `require.resolve`，会利用模块系统的内部机制对传入的字符串参数进行路径解析。

```
seajs.resolve('jquery');
// => http://path/to/jquery.js

seajs.resolve('./a', 'http://example.com/to/b.js');
// => http://example.com/to/a.js

```

`seajs.resolve` 方法不光可以用来调试路径解析是否正确，还可以用在插件开发环境中。

## seajs.require `Function`

全局的 `require` 方法，可用来直接获取模块接口，比如

```
seajs.use(['a', 'b'], function() {

  var a = seajs.require('a')
  var b = seajs.require('b')

  // do something...
})
```

## seajs.data `Object`

通过 `seajs.data`，可以查看 `seajs` 所有配置以及一些内部变量的值，可用于插件开发。当加载遇到问题时，也可用于调试。

## seajs.log `Function`

由 seajs-log 插件提供，详见：[`github.com/seajs/seajs-log`](https://github.com/seajs/seajs-log)

## seajs.find `Function`

由 seajs-debug 插件提供，详见：[`github.com/seajs/seajs-debug`](https://github.com/seajs/seajs-debug)

* * *

Sea.js 还有 debug 插件：[seajs-debug](https://github.com/seajs/seajs-debug)

有了这些方法和插件，能极大地方便开发维护，赶快试试吧。