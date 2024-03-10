# 模块标识

模块标识是一个字符串，用来标识模块。在 `require`、 `require.async` 等加载函数中，第一个参数都是模块标识。

Sea.js 中的模块标识是 [CommonJS 模块标识](http://wiki.commonjs.org/wiki/Modules/1.1.1) 的超集:

1.  一个模块标识由斜线（`/`）分隔的多项组成。
2.  每一项必须是小驼峰字符串、 `.` 或 `..` 。
3.  模块标识可以不包含文件后缀名，比如 `.js` 。
4.  模块标识可以是 **相对** 或 **顶级** 标识。如果第一项是 `.` 或 `..`，则该模块标识是相对标识。
5.  顶级标识根据模块系统的基础路径来解析。
6.  相对标识相对 `require` 所在模块的路径来解析。

注意，符合上述规范的标识肯定是 Sea.js 的模块标识，但 Sea.js 能识别的模块标识不需要完全符合以上规范。 比如，除了大小写字母组成的小驼峰字符串，Sea.js 的模块标识字符串还可以包含下划线（`_`）和连字符（`-`）， 甚至可以是 `http://`、`https://`、`file:///` 等协议开头的绝对路径。

## 相对标识

相对标识以 `.` 开头，只出现在模块环境中（`define` 的 `factory` 方法里面）。相对标识永远相对当前模块的 URI 来解析：

```js
// 在 http://example.com/js/a.js 的 factory 中：
require.resolve('./b');
  // => http://example.com/js/b.js

// 在 http://example.com/js/a.js 的 factory 中：
require.resolve('../c');
  // => http://example.com/c.js
```

## 顶级标识

顶级标识不以点（`.`）或斜线（`/`）开始， 会相对模块系统的基础路径（即 Sea.js 的 `base` 路径）来解析：

```js
// 假设 base 路径是：http://example.com/assets/

// 在模块代码里：
require.resolve('gallery/jquery/1.9.1/jquery');
  // => http://example.com/assets/gallery/jquery/1.9.1/jquery.js
```

模块系统的基础路径即 `base` 的默认值，与 `sea.js` 的访问路径相关：

```js
如果 sea.js 的访问路径是：
  http://example.com/assets/sea.js

则 base 路径为：
  http://example.com/assets/ 
```

当 `sea.js` 的访问路径中含有版本号时，`base` 不会包含 `seajs/x.y.z` 字串。 当 `sea.js` 有多个版本时，这样会很方便。

```js
如果 sea.js 的路径是：
  http://example.com/assets/seajs/1.0.0/sea.js

则 base 路径是：
  http://example.com/assets/ 
```

当然，也可以手工配置 `base` 路径：

```js
seajs.config({
  base: 'http://code.jquery.com/'
});

// 在模块代码里：
require.resolve('jquery');
  // => http://code.jquery.com/jquery.js
```

## 普通路径

除了相对和顶级标识之外的标识都是普通路径。普通路径的解析规则，和 HTML 代码中的 `<script src="..."></script>` 一样，会相对当前页面解析。

```js
// 假设当前页面是 http://example.com/path/to/page/index.html

// 绝对路径是普通路径：
require.resolve('http://cdn.com/js/a');
  // => http://cdn.com/js/a.js

// 根路径是普通路径：
require.resolve('/js/b');
  // => http://example.com/js/b.js

// use 中的相对路径始终是普通路径：
seajs.use('./c');
  // => 加载的是 http://example.com/path/to/page/c.js

seajs.use('../d');
  // => 加载的是 http://example.com/path/to/d.js
```

**提示**：

1.  顶级标识始终相对 `base` 基础路径解析。
2.  绝对路径和根路径始终相对当前页面解析。
3.  `require` 和 `require.async` 中的相对路径相对当前模块路径来解析。
4.  `seajs.use` 中的相对路径始终相对当前页面来解析。

## 文件后缀的自动添加规则

Sea.js 在解析模块标识时， 除非在路径中有问号（`?`）或最后一个字符是井号（`#`），否则都会自动添加 JS 扩展名（`.js`）。如果不想自动添加扩展名，可以在路径末尾加上井号（`#`）。

```js
// ".js" 后缀可以省略：
require.resolve('http://example.com/js/a');
require.resolve('http://example.com/js/a.js');
  // => http://example.com/js/a.js

// ".css" 后缀不可省略：
require.resolve('http://example.com/css/a.css');
  // => http://example.com/css/a.css

// 当路径中有问号（"?"）时，不会自动添加后缀：
require.resolve('http://example.com/js/a.json?callback=define');
  // => http://example.com/js/a.json?callback=define

// 当路径以井号（"#"）结尾时，不会自动添加后缀，且在解析时，会自动去掉井号：
require.resolve('http://example.com/js/a.json#');
  // => http://example.com/js/a.json
```

## 设计原则

模块标识的规则就上面这些，设计的核心出发点是：

1.  **关注度分离**。比如书写模块 `a.js` 时，如果需要引用 `b.js`，则只需要知道 `b.js` 相对 `a.js` 的相对路径即可，无需关注其他。

2.  **尽量与浏览器的解析规则一致**。比如根路径（`/xx/zz`）、绝对路径、以及传给 `use` 方法的非顶级标识，都是相对所在页面的 URL 进行解析。

一旦理解了以上两点，一切都会很自然、很简单。不必刻意去记这些规则，多写写，自然就会。