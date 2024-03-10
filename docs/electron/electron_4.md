# API 文档

# 简介

所有的[Node.js's built-in modules](http://nodejs.org/api/)在 Electron 中都可用，并且所有的 node 的第三方组件也可以放心使用（包括[自身的模块](https://github.com/heyunjiang/electron/blob/master/docs/tutorial/using-native-node-modules.md)）。

Electron 也提供了一些额外的内置组件来开发传统桌面应用。一些组件只可以在主进程中使用，一些只可以在渲染进程中使用，但是也有部分可以在这 2 种进程中都可使用。

基本规则：GUI 模块或者系统底层的模块只可以在主进程中使用。要使用这些模块，你应当很熟悉[主进程 vs 渲染进程](https://github.com/heyunjiang/electron/blob/master/docs/tutorial/quick-start.md#the-main-process)脚本的概念。

主进程脚本看起来像个普通的 nodejs 脚本

```
const electron = require('electron');
const app = electron.app;
const BrowserWindow = electron.BrowserWindow;

var window = null;

app.on('ready', function() {
  window = new BrowserWindow({width: 800, height: 600});
  window.loadURL('https://github.com');
}); 
```

渲染进程和传统的 web 界面一样，除了它具有使用 node 模块的能力：

```
<!DOCTYPE html>
<html>
<body>
<script> const remote = require('electron').remote;
  console.log(remote.app.getVersion()); </script>
</body>
</html> 
```

如果想运行应用，参考 `Run your app` 。

## 解构任务

如果你使用的是 CoffeeScript 或 Babel，你可以使用[destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)来让使用内置模块更简单:

```
const {app, BrowserWindow} = require('electron'); 
```

然而如果你使用的是普通的 JavaScript，你就需要等到 Chrome 支持 ES6 了。

## 使用内置模块时禁用旧样式

在版本 v0.35.0 之前，所有的内置模块都需要按造 `require('module-name')` 形式来使用，虽然它有很多[弊端](https://github.com/electron/electron/issues/387)，我们仍然在老的应用中友好的支持它。

为了完整的禁用旧样式，你可以设置环境变量 `ELECTRON_HIDE_INTERNAL_MODULES` :

```
process.env.ELECTRON_HIDE_INTERNAL_MODULES = 'true' 
```

或者调用 `hideInternalModules` API:

```
require('electron').hideInternalModules() 
```

# 进程对象

# 进程

Electron 中的 `process` 对象 与 upstream node 中的有以下的不同点:

*   `process.type` String - 进程类型, 可以是 `browser` (i.e. main process) 或 `renderer`.
*   `process.versions['electron']` String - Electron 的版本.
*   `process.versions['chrome']` String - Chromium 的版本.
*   `process.resourcesPath` String - JavaScript 源代码路径.
*   `process.mas` Boolean - 在 Mac App Store 创建, 它的值为 `true`, 在其它的地方值为 `undefined`.

## 事件

### 事件: 'loaded'

在 Electron 已经加载了其内部预置脚本和它准备加载主进程或渲染进程的时候触发.

当 node 被完全关闭的时候，它可以被预加载脚本使用来添加(原文: removed)与 node 无关的全局符号来回退到全局范围:

```
// preload.js
var _setImmediate = setImmediate;
var _clearImmediate = clearImmediate;
process.once('loaded', function() {
  global.setImmediate = _setImmediate;
  global.clearImmediate = _clearImmediate;
}); 
```

## 属性

### `process.noAsar`

设置它为 `true` 可以使 `asar` 文件在 node 的内置模块中实效.

## 方法

`process` 对象有如下方法:

### `process.hang()`

使当前进程的主线成挂起.

### `process.setFdLimit(maxDescriptors)` *OS X* *Linux*

*   `maxDescriptors` Integer

设置文件描述符软限制于 `maxDescriptors` 或硬限制与 os, 无论它是否低于当前进程.

# 支持的 Chrome 命令行开关

这页列出了 Chrome 浏览器和 Electron 支持的命令行开关. 你也可以在 app 模块的 ready 事件发出之前使用 app.commandLine.appendSwitch 来添加它们到你应用的 main 脚本里面:

```
const app = require('electron').app;
app.commandLine.appendSwitch('remote-debugging-port', '8315');
app.commandLine.appendSwitch('host-rules', 'MAP * 127.0.0.1');

app.on('ready', function() {
  // Your code here
}); 
```

## --client-certificate=`path`

设置客户端的证书文件 `path` .

## --ignore-connections-limit=`domains`

忽略用 `,` 分隔的 `domains` 列表的连接限制.

## --disable-http-cache

禁止请求 HTTP 时使用磁盘缓存.

## --remote-debugging-port=`port`

在指定的 `端口` 通过 HTTP 开启远程调试.

## --js-flags=`flags`

指定引擎过渡到 JS 引擎.

在启动 Electron 时，如果你想在主进程中激活 `flags` ，它将被转换.

```
$ electron --js-flags="--harmony_proxies --harmony_collections" your-app 
```

## --proxy-server=`address:port`

使用一个特定的代理服务器，它将比系统设置的优先级更高.这个开关只有在使用 HTTP 协议时有效，它包含 HTTPS 和 WebSocket 请求. 值得注意的是，不是所有的代理服务器都支持 HTTPS 和 WebSocket 请求.

## --proxy-bypass-list=`hosts`

让 Electron 使用(原文:bypass) 提供的以 semi-colon 分隔的 hosts 列表的代理服务器.这个开关只有在使用 `--proxy-server` 时有效.

例如:

```
app.commandLine.appendSwitch('proxy-bypass-list', '<local>;*.google.com;*foo.com;1.2.3.4:5678') 
```

将会为所有的 hosts 使用代理服务器，除了本地地址 (`localhost`, `127.0.0.1` etc.), `google.com` 子域, 以 `foo.com` 结尾的 hosts，和所有类似 `1.2.3.4:5678`的.

## --proxy-pac-url=`url`

在指定的 `url` 上使用 PAC 脚本.

## --no-proxy-server

不使用代理服务并且总是使用直接连接.忽略所有的合理代理标志.

## --host-rules=`rules`

一个逗号分隔的 `rule` 列表来控制主机名如何映射.

例如:

*   `MAP * 127.0.0.1` 强制所有主机名映射到 127.0.0.1
*   `MAP *.google.com proxy` 强制所有 google.com 子域 使用 "proxy".
*   `MAP test.com [::1]:77` 强制 "test.com" 使用 IPv6 回环地址. 也强制使用端口 77.
*   `MAP * baz, EXCLUDE www.google.com` 重新全部映射到 "baz", 除了 "www.google.com".

这些映射适用于终端网络请求 (TCP 连接 和 主机解析 以直接连接的方式, 和 `CONNECT` 以代理连接, 还有 终端 host 使用 `SOCKS` 代理连接).

## --host-resolver-rules=`rules`

类似 `--host-rules` ，但是 `rules` 只适合主机解析.

## --ignore-certificate-errors

忽略与证书相关的错误.

## --ppapi-flash-path=`path`

设置 Pepper Flash 插件的路径 `path` .

## --ppapi-flash-version=`version`

设置 Pepper Flash 插件版本号.

## --log-net-log=`path`

使网络日志事件能够被读写到 `path`.

## --ssl-version-fallback-min=`version`

设置最简化的 SSL/TLS 版本号 ("tls1", "tls1.1" or "tls1.2")，TLS 可接受回退.

## --cipher-suite-blacklist=`cipher_suites`

指定逗号分隔的 SSL 密码套件 列表实效.

## --disable-renderer-backgrounding

防止 Chromium 降低隐藏的渲染进程优先级.

这个标志对所有渲染进程全局有效，如果你只想在一个窗口中禁止使用，你可以采用 hack 方法[playing silent audio](https://github.com/atom/atom/pull/9485/files).

## --enable-logging

打印 Chromium 信息输出到控制台.

如果在用户应用加载完成之前解析`app.commandLine.appendSwitch` ，这个开关将实效，但是你可以设置 `ELECTRON_ENABLE_LOGGING` 环境变量来达到相同的效果.

## --v=`log_level`

设置默认最大活跃 V-logging 标准; 默认为 0.通常 V-logging 标准值为肯定值.

这个开关只有在 `--enable-logging` 开启时有效.

## --vmodule=`pattern`

赋予每个模块最大的 V-logging levels 来覆盖 `--v` 给的值.E.g. `my_module=2,foo*=3` 会改变所有源文件 `my_module.*` and `foo*.*` 的代码中的 logging level .

任何包含向前的(forward slash)或者向后的(backward slash)模式将被测试用于阻止整个路径名，并且不仅是 E.g 模块.`*/foo/bar/*=2` 将会改变所有在 `foo/bar` 下的源文件代码中的 logging level .

这个开关只有在 `--enable-logging` 开启时有效.

# 环境变量

一些 Electron 的行为受到环境变量的控制，因为他们的初始化比命令行和应用代码更早.

POSIX shells 的例子:

```
$ export ELECTRON_ENABLE_LOGGING=true
$ electron 
```

Windows 控制台:

```
> set ELECTRON_ENABLE_LOGGING=true
> electron 
```

## `ELECTRON_RUN_AS_NODE`

类似 node.js 普通进程启动方式.

## `ELECTRON_ENABLE_LOGGING`

打印 Chrome 的内部日志到控制台.

## `ELECTRON_LOG_ASAR_READS`

当 Electron 读取 ASA 文档，把 read offset 和文档路径做日志记录到系统 `tmpdir`.结果文件将提供给 ASAR 模块来优化文档组织.

## `ELECTRON_ENABLE_STACK_DUMPING`

当 Electron 崩溃的时候，打印堆栈记录到控制台.

如果 `crashReporter` 已经启动那么这个环境变量实效.

## `ELECTRON_DEFAULT_ERROR_MODE` *Windows*

当 Electron 崩溃的时候，显示 windows 的崩溃对话框.

如果 `crashReporter` 已经启动那么这个环境变量实效.

## `ELECTRON_NO_ATTACH_CONSOLE` *Windows*

不可使用当前控制台.

## `ELECTRON_FORCE_WINDOW_MENU_BAR` *Linux*

不可再 Linux 上使用全局菜单栏.

## `ELECTRON_HIDE_INTERNAL_MODULES`

关闭旧的内置模块如 `require('ipc')` 的通用模块.

# 自定义的 DOM 元素

# `File` 对象

# `File`对象

为了让用户能够通过 HTML5 的 file API 直接操作本地文件，DOM 的 File 接口提供了对本地文件的抽象。Electron 在 File 接口中增加了一个 path 属性，它是文件在系统中的真实路径。

* * *

获取拖动到 APP 中文件的真实路径的例子：

```
<div id="holder">
  Drag your file here
</div>

<script>
  var holder = document.getElementById('holder');
  holder.ondragover = function () {
    return false;
  };
  holder.ondragleave = holder.ondragend = function () {
    return false;
  };
  holder.ondrop = function (e) {
    e.preventDefault();
    var file = e.dataTransfer.files[0];
    console.log('File you dragged here is', file.path);
    return false;
  };
</script> 
```

# `<webview>` 标签

使用 `webview` 标签来把 'guest' 内容（例如 web pages ）嵌入到你的 Electron app 中. guest 内容包含在 `webview` 容器中.一个嵌入你应用的 page 控制着 guest 内容如何布局摆放和表达含义.

与 `iframe` 不同, `webview` 和你的应用运行的是不同的进程. 它不拥有渲染进程的权限，并且应用和嵌入内容之间的交互全部都是异步的.因为这能保证应用的安全性不受嵌入内容的影响.

## 例子

把一个 web page 嵌入到你的 app，首先添加 `webview` 标签到你的 app 待嵌入 page(展示 guest content). 在一个最简单的 `webview` 中，它包含了 web page 的文件路径和一个控制 `webview` 容器展示效果的 css 样式:

```
<webview id="foo" src="https://www.github.com/" style="display:inline-block; width:640px; height:480px"></webview> 
```

如果想随时控制 guest 内容，可以添加 JavaScript 脚本来监听 `webview` 事件使用 `webview` 方法来做出响应. 这里是 2 个事件监听的例子：一个监听 web page 准备加载，另一个监听 web page 停止加载，并且在加载的时候显示一条 "loading..." 信息:

```
<script> onload = function() {
    var webview = document.getElementById("foo");
    var indicator = document.querySelector(".indicator");

    var loadstart = function() {
      indicator.innerText = "loading...";
    }
    var loadstop = function() {
      indicator.innerText = "";
    }
    webview.addEventListener("did-start-loading", loadstart);
    webview.addEventListener("did-stop-loading", loadstop);
  } </script> 
```

## 标签属性

`webview` 标签有下面一些属性 :

### `src`

```
<webview src="https://www.github.com/"></webview> 
```

将一个可用的 url 做为这个属性的初始值添加到顶部导航.

如果把当前页的 src 添加进去将加载当前 page.

`src`同样可以填 data urls，例如 `data:text/plain,Hello, world!`.

### `autosize`

```
<webview src="https://www.github.com/" autosize="on" minwidth="576" minheight="432"></webview> 
```

如果这个属性的值为 "on" ， `webview` 容器将会根据属性`minwidth`, `minheight`, `maxwidth`, 和 `maxheight` 的值在它们之间自适应. 只有在 `autosize` 开启的时候这个约束才会有效. 当 `autosize` 开启的时候， `webview` 容器的 size 只能在上面那四个属性值之间.

### `nodeintegration`

```
<webview src="http://www.google.com/" nodeintegration></webview> 
```

如果设置了这个属性， `webview` 中的 guest page 将整合 node，并且拥有可以使用系统底层的资源，例如 `require` 和 `process` .

### `plugins`

```
<webview src="https://www.github.com/" plugins></webview> 
```

如果这个属性的值为 "on" ， `webview` 中的 guest page 就可以使用浏览器插件。

### `preload`

```
<webview src="https://www.github.com/" preload="./test.js"></webview> 
```

在 guest page 中的其他脚本执行之前预加载一个指定的脚本。规定预加载脚本的 url 须如 `file:` 或者 `asar:`，因为它在是 guest page 中通过通过 `require` 命令加载的。

如果 guest page 没有整合 node ，这个脚本将试图使用真个 Node APIs ，但是在这个脚本执行完毕时，之前由 node 插入的全局对象会被删除。

### `httpreferrer`

```
<webview src="https://www.github.com/" httpreferrer="http://cheng.guru"></webview> 
```

为 guest page 设置 referrer URL。

### `useragent`

```
<webview src="https://www.github.com/" useragent="Mozilla/5.0 (Windows NT 6.1; WOW64; Trident/7.0; AS; rv:11.0) like Gecko"></webview> 
```

在 guest page 加载之前为其设置用户代理。如果页面已经加载了，可以使用 `setUserAgent` 方法来改变用户代理。

### `disablewebsecurity`

```
<webview src="https://www.github.com/" disablewebsecurity></webview> 
```

如果这个属性的值为 "on" ， guest page 会禁用 web 安全控制.

### partition

```
<webview src="https://github.com" partition="persist:github"></webview>
<webview src="http://electron.atom.io" partition="electron"></webview> 
```

为 page 设置 session。如果初始值为 `partition` ,这个 page 将会为 app 中的所有 page 应用同一个持续有效的 session。如果没有 `persist:` 前缀, 这个 page 将会使用一个历史 session 。通过分配使用相同的 `partition`, 所有的 page 都可以分享相同的 session。如果 `partition` 没有设置，那 app 将使用默认的 session.

这个值只能在在第一个渲染进程之前设置修改，之后修改的话会无效并且抛出一个 DOM 异常.

### `allowpopups`

```
<webview src="https://www.github.com/" allowpopups></webview> 
```

如果这个属性的值为 "on" ，将允许 guest page 打开一个新窗口。

### `blinkfeatures`

```
<webview src="https://www.github.com/" blinkfeatures="PreciseMemoryInfo, CSSVariables"></webview> 
```

这个属性的值为一个用逗号分隔的列表，它的值指定特性被启用。你可以从[setFeatureEnabledFromString](https://code.google.com/p/chromium/codesearch#chromium/src/out/Debug/gen/blink/platform/RuntimeEnabledFeatures.cpp&sq=package:chromium&type=cs&l=527)函数找到完整的支持特性。

## 方法

`webview` 的方法集合:

**注意:** webview 元素必须在使用这些方法之前加载完毕。

**例如**

```
webview.addEventListener("dom-ready", function() {
  webview.openDevTools();
}); 
```

### `<webview>.loadURL(url[, options])`

*   `url` URL
*   `options` Object (可选)
    *   `httpReferrer` String - 一个 http 类型的 url.
    *   `userAgent` String -用于发起请求的用户代理.
    *   `extraHeaders` String - 额外的 headers,用 "\n"分隔.

加载 webview 中的 `url`，`url` 必须包含协议前缀，例如 `http://` 或 `file://`.

### `<webview>.getURL()`

从 guest page 中返回 url.

### `<webview>.getTitle()`

从 guest page 中返回 title.

### `<webview>.isLoading()`

返回一个 guest page 是否仍在加载资源的布尔值.

### `<webview>.isWaitingForResponse()`

返回一个 guest page 是否正在等待 page 的主要资源做出回应的布尔值.

### `<webview>.stop()`

停止渲染.

### `<webview>.reload()`

重新加载 guest page.

### `<webview>.reloadIgnoringCache()`

忽视缓存，重新加载 guest page.

### `<webview>.canGoBack()`

返回一个 guest page 是否能够回退的布尔值.

### `<webview>.canGoForward()`

返回一个 guest page 是否能够前进的布尔值.

### `<webview>.canGoToOffset(offset)`

*   `offset` Integer

返回一个 guest page 是否能够前进到 `offset` 的布尔值.

### `<webview>.clearHistory()`

清除导航历史.

### `<webview>.goBack()`

guest page 回退.

### `<webview>.goForward()`

guest page 前进.

### `<webview>.goToIndex(index)`

*   `index` Integer

guest page 导航到指定的绝对位置.

### `<webview>.goToOffset(offset)`

*   `offset` Integer

guest page 导航到指定的相对位置.

### `<webview>.isCrashed()`

返回一个 渲染进程是否崩溃 的布尔值.

### `<webview>.setUserAgent(userAgent)`

*   `userAgent` String

重新设置用户代理.

### `<webview>.getUserAgent()`

返回用户代理名字，返回类型：`String`.

### `<webview>.insertCSS(css)`

*   `css` String

插入 css.

### `<webview>.executeJavaScript(code, userGesture, callback)`

*   `code` String
*   `userGesture` Boolean - 默认 `false`.
*   `callback` Function (可选) - 回调函数.
    *   `result`

评估 `code` ，如果 `userGesture` 值为 true ，它将在这个 page 里面创建用户手势. HTML APIs ，如 `requestFullScreen`,它需要用户响应，那么将自动通过这个参数优化.

### `<webview>.openDevTools()`

为 guest page 打开开发工具调试窗口.

### `<webview>.closeDevTools()`

为 guest page 关闭开发工具调试窗口.

### `<webview>.isDevToolsOpened()`

返回一个 guest page 是否打开了开发工具调试窗口的布尔值.

### `<webview>.isDevToolsFocused()`

返回一个 guest page 是否聚焦了开发工具调试窗口的布尔值.

### `<webview>.inspectElement(x, y)`

*   `x` Integer
*   `y` Integer

开始检查 guest page 在 (`x`, `y`) 位置的元素.

### `<webview>.inspectServiceWorker()`

在 guest page 中为服务人员打开开发工具.

### `<webview>.setAudioMuted(muted)`

*   `muted` Boolean 设置 guest page 流畅(muted).

### `<webview>.isAudioMuted()`

返回一个 guest page 是否流畅的布尔值.

### `<webview>.undo()`

在 page 中编辑执行 `undo` 命令.

### `<webview>.redo()`

在 page 中编辑执行 `redo` 命令.

### `<webview>.cut()`

在 page 中编辑执行 `cut` 命令.

### `<webview>.copy()`

在 page 中编辑执行 `copy` 命令.

### `<webview>.paste()`

在 page 中编辑执行 `paste` 命令.

### `<webview>.pasteAndMatchStyle()`

在 page 中编辑执行 `pasteAndMatchStyle` 命令.

### `<webview>.delete()`

在 page 中编辑执行 `delete` 命令.

### `<webview>.selectAll()`

在 page 中编辑执行 `selectAll` 命令.

### `<webview>.unselect()`

在 page 中编辑执行 `unselect` 命令.

### `<webview>.replace(text)`

*   `text` String

在 page 中编辑执行 `replace` 命令.

### `<webview>.replaceMisspelling(text)`

*   `text` String

在 page 中编辑执行 `replaceMisspelling` 命令.

### `<webview>.insertText(text)`

*   `text` String

插入文本.

### `<webview>.findInPage(text[, options])`

*   `text` String - 搜索内容,不能为空.
*   `options` Object (可选)
    *   `forward` Boolean - 向前或向后, 默认为 `true`.
    *   `findNext` Boolean - 是否查找的第一个结果, 默认为 `false`.
    *   `matchCase` Boolean - 是否区分大小写, 默认为 `false`.
    *   `wordStart` Boolean - 是否只查找首字母. 默认为 `false`.
    *   `medialCapitalAsWordStart` Boolean - 当配合 `wordStart`的时候,接受一个文字中的匹配项，要求匹配项是以大写字母开头后面跟小写字母或者没有字母。可以接受一些其他单词内部匹配, 默认为 `false`.

发起一个请求来寻找页面中的所有匹配 `text` 的地方并且返回一个 `Integer`来表示这个请求用的请求 Id. 这个请求结果可以通过订阅`found-in-page` 事件来取得.

### `<webview>.stopFindInPage(action)`

*   `action` String - 指定一个行为来接替停止 `<webview>.findInPage` 请求.
    *   `clearSelection` - 转变为一个普通的 selection.
    *   `keepSelection` - 清除 selection.
    *   `activateSelection` - 聚焦并点击 selection node.

使用 `action` 停止 `findInPage` 请求.

### `<webview>.print([options])`

打印输出 `webview` 的 web page. 类似 `webContents.print([options])`.

### `<webview>.printToPDF(options, callback)`

以 pdf 格式打印输出 `webview` 的 web page. 类似 `webContents.printToPDF(options, callback)`.

### `<webview>.send(channel[, arg1][, arg2][, ...])`

*   `channel` String
*   `arg` (可选)

通过 `channel` 向渲染进程发出异步消息，你也可以发送任意的参数。 渲染进程通过`ipcRenderer` 模块监听 `channel` 事件来控制消息.

例子 webContents.send.

### `<webview>.sendInputEvent(event)`

*   `event` Object

向 page 发送输入事件.

查看 webContents.sendInputEvent 关于 `event` 对象的相信介绍.

### `<webview>.getWebContents()`

返回和这个 `webview` 相关的 WebContents.

## DOM 事件

`webview` 可用下面的 DOM 事件:

### Event: 'load-commit'

返回:

*   `url` String
*   `isMainFrame` Boolean

加载完成触发. 这个包含当前文档的导航和副框架的文档加载，但是不包含异步资源加载.

### Event: 'did-finish-load'

在导航加载完成时触发，也就是 tab 的 spinner 停止 spinning，并且加载事件处理.

### Event: 'did-fail-load'

Returns:

*   `errorCode` Integer
*   `errorDescription` String
*   `validatedURL` String

类似 `did-finish-load` ，在加载失败或取消是触发，例如提出 `window.stop()`.

### Event: 'did-frame-finish-load'

返回:

*   `isMainFrame` Boolean

当一个 frame 完成 加载时触发.

### Event: 'did-start-loading'

开始加载时触发.

### Event: 'did-stop-loading'

停止家在时触发.

### Event: 'did-get-response-details'

返回:

*   `status` Boolean
*   `newURL` String
*   `originalURL` String
*   `httpResponseCode` Integer
*   `requestMethod` String
*   `referrer` String
*   `headers` Object

当获得返回详情的时候触发.

`status` 指示 socket 连接来下载资源.

### Event: 'did-get-redirect-request'

返回:

*   `oldURL` String
*   `newURL` String
*   `isMainFrame` Boolean

当重定向请求资源被接收的时候触发.

### Event: 'dom-ready'

当指定的 frame 文档加载完毕时触发.

### Event: 'page-title-updated'

返回:

*   `title` String
*   `explicitSet` Boolean

当导航中的页面 title 被设置时触发. 在 title 通过文档路径异步加载时`explicitSet`为 false.

### Event: 'page-favicon-updated'

返回:

*   `favicons` Array - Array of URLs.

当 page 收到了图标 url 时触发.

### Event: 'enter-html-full-screen'

当通过 HTML API 使界面进入全屏时触发.

### Event: 'leave-html-full-screen'

当通过 HTML API 使界面退出全屏时触发.

### Event: 'console-message'

返回:

*   `level` Integer
*   `message` String
*   `line` Integer
*   `sourceId` String

当客户端输出控制台信息的时候触发.

下面示例代码将所有信息输出到内置控制台，没有考虑到输出等级和其他属性。

```
webview.addEventListener('console-message', function(e) {
  console.log('Guest page logged a message:', e.message);
}); 
```

### Event: 'found-in-page'

返回:

*   `result` Object
    *   `requestId` Integer
    *   `finalUpdate` Boolean - 指明下面是否还有更多的回应.
    *   `activeMatchOrdinal` Integer (可选) - 活动匹配位置
    *   `matches` Integer (optional) - 匹配数量.
    *   `selectionArea` Object (optional) - 整合第一个匹配域.

在请求`webview.findInPage`结果有效时触发.

```
webview.addEventListener('found-in-page', function(e) {
  if (e.result.finalUpdate)
    webview.stopFindInPage("keepSelection");
});

const rquestId = webview.findInPage("test"); 
```

### Event: 'new-window'

返回:

*   `url` String
*   `frameName` String
*   `disposition` String - 可以为 `default`, `foreground-tab`, `background-tab`, `new-window` 和 `other`.
*   `options` Object - 参数应该被用作创建新的 `BrowserWindow`.

在 guest page 试图打开一个新的浏览器窗口时触发.

下面示例代码在系统默认浏览器中打开了一个新的 url.

```
webview.addEventListener('new-window', function(e) {
  require('electron').shell.openExternal(e.url);
}); 
```

### Event: 'will-navigate'

返回:

*   `url` String

当用户或 page 尝试开始导航时触发. 它能在 `window.location` 变化或者用户点击连接的时候触发.

这个事件在以 APIS 编程方式开始导航时不会触发，例如 `<webview>.loadURL` 和 `<webview>.back`.

在页面内部导航跳转也将不回触发这个事件，例如点击锚链接或更新 `window.location.hash`.使用 `did-navigate-in-page` 来实现页内跳转事件.

使用 `event.preventDefault()` 并不会起什么用.

### Event: 'did-navigate'

返回:

*   `url` String

当导航结束时触发.

在页面内部导航跳转也将不回触发这个事件，例如点击锚链接或更新 `window.location.hash`.使用 `did-navigate-in-page` 来实现页内跳转事件.

### Event: 'did-navigate-in-page'

返回:

*   `url` String

当页内导航发生时触发. 当业内导航发生时，page url 改变了，但是不会跳出 page . 例如在锚链接被电击或 DOM `hashchange` 事件发生时触发.

### Event: 'close'

在 guest page 试图关闭自己的时候触发.

下面的示例代码指示了在客户端试图关闭自己的时候将改变导航连接为`about:blank`.

```
webview.addEventListener('close', function() {
  webview.src = 'about:blank';
}); 
```

### Event: 'ipc-message'

返回:

*   `channel` String
*   `args` Array

在 guest page 向嵌入页发送一个异步消息的时候触发.

你可以很简单的使用 `sendToHost` 方法和 `ipc-message` 事件在 guest page 和 嵌入页(embedder page)之间通信:

```
// In embedder page.
webview.addEventListener('ipc-message', function(event) {
  console.log(event.channel);
  // Prints "pong"
});
webview.send('ping'); 
```

```
// In guest page.
var ipcRenderer = require('electron').ipcRenderer;
ipcRenderer.on('ping', function() {
  ipcRenderer.sendToHost('pong');
}); 
```

### Event: 'crashed'

在渲染进程崩溃的时候触发.

### Event: 'gpu-crashed'

在 GPU 进程崩溃的时候触发.

### Event: 'plugin-crashed'

返回:

*   `name` String
*   `version` String

在插件进程崩溃的时候触发.

### Event: 'destroyed'

在界面内容销毁的时候触发.

### Event: 'media-started-playing'

在媒体准备播放的时候触发.

### Event: 'media-paused'

在媒体暂停播放或播放放毕的时候触发.

### Event: 'did-change-theme-color'

在页面的主体色改变的时候触发. 在使用 meta 标签的时候这就很常见了:

```
<meta name='theme-color' content='#ff0000'> 
```

### Event: 'devtools-opened'

在开发者工具打开的时候触发.

### Event: 'devtools-closed'

在开发者工具关闭的时候触发.

### Event: 'devtools-focused'

在开发者工具获取焦点的时候触发.

# `window.open` 函数

当在界面中使用 `window.open` 来创建一个新的窗口时候，将会创建一个 `BrowserWindow` 的实例，并且将返回一个标识，这个界面通过标识来对这个新的窗口进行有限的控制.

这个标识对传统的 web 界面来说，通过它能对子窗口进行有限的功能性兼容控制. 想要完全的控制这个窗口，可以直接创建一个 `BrowserWindow` .

新创建的 `BrowserWindow` 默认为继承父窗口的属性参数，想重写属性的话可以在 `features` 中设置他们.

### `window.open(url[, frameName][, features])`

*   `url` String
*   `frameName` String (可选)
*   `features` String (可选)

创建一个新的 window 并且返回一个 `BrowserWindowProxy` 类的实例.

`features` 遵循标准浏览器的格式，但是每个 feature 应该作为 `BrowserWindow` 参数的一个字段.

### `window.opener.postMessage(message, targetOrigin)`

*   `message` String
*   `targetOrigin` String

通过指定位置或用 `*` 来代替没有明确位置来向父窗口发送信息.

## Class: BrowserWindowProxy

`BrowserWindowProxy` 由`window.open` 创建返回，并且提供了对子窗口的有限功能性控制.

### `BrowserWindowProxy.blur()`

子窗口的失去焦点.

### `BrowserWindowProxy.close()`

强行关闭子窗口，忽略卸载事件.

### `BrowserWindowProxy.closed`

在子窗口关闭之后恢复正常.

### `BrowserWindowProxy.eval(code)`

*   `code` String

评估子窗口的代码.

### `BrowserWindowProxy.focus()`

子窗口获得焦点(让其显示在最前).

### `BrowserWindowProxy.postMessage(message, targetOrigin)`

*   `message` String
*   `targetOrigin` String

通过指定位置或用 `*` 来代替没有明确位置来向子窗口发送信息.

除了这些方法，子窗口还可以无特性和使用单一方法来实现 `window.opener` 对象.

# 在主进程内可用的模块

# app

`app` 模块是为了控制整个应用的生命周期设计的。

下面的这个例子将会展示如何在最后一个窗口被关闭时退出应用：

```
var app = require('app');
app.on('window-all-closed', function() {
  app.quit();
}); 
```

## 事件列表

`app` 对象会触发以下的事件：

### 事件：'will-finish-launching'

当应用程序完成基础的启动的时候被触发。在 Windows 和 Linux 中， `will-finish-launching` 事件与 `ready` 事件是相同的； 在 OS X 中， 这个时间相当于 `NSApplication` 中的 `applicationWillFinishLaunching` 提示。 你应该经常在这里为 `open-file` 和 `open-url` 设置监听器，并启动崩溃报告和自动更新。

在大多数的情况下，你应该只在 `ready` 事件处理器中完成所有的业务。

### 事件：'ready'

当 Electron 完成初始化时被触发。

### 事件：'window-all-closed'

当所有的窗口都被关闭时触发。

这个时间仅在应用还没有退出时才能触发。 如果用户按下了 `Cmd + Q`， 或者开发者调用了 `app.quit()` ，Electron 将会先尝试关闭所有的窗口再触发 `will-quit` 事件， 在这种情况下 `window-all-closed` 不会被触发。

### 事件：'before-quit'

返回：

*   `event` Event

在应用程序开始关闭它的窗口的时候被触发。 调用 `event.preventDefault()` 将会阻止终止应用程序的默认行为。

### 事件：'will-quit'

返回：

*   `event` Event

当所有的窗口已经被关闭，应用即将退出时被触发。 调用 `event.preventDefault()` 将会阻止终止应用程序的默认行为。

你可以在 `window-all-closed` 事件的描述中看到 `will-quit` 事件 和 `window-all-closed` 事件的区别。

### 事件：'quit'

返回：

*   `event` Event
*   `exitCode` Integer

当应用程序正在退出时触发。

### 事件：'open-file' *OS X*

返回：

*   `event` Event
*   `path` String

当用户想要在应用中打开一个文件时触发。`open-file` 事件常常在应用已经打开并且系统想要再次使用应用打开文件时被触发。 `open-file` 也会在一个文件被拖入 dock 且应用还没有运行的时候被触发。 请确认在应用启动的时候（甚至在 `ready` 事件被触发前）就对 `open-file` 事件进行监听，以处理这种情况。

如果你想处理这个事件，你应该调用 `event.preventDefault()` 。 在 Windows 系统中, 你需要通过解析 process.argv 来获取文件路径。

### 事件：'open-url' *OS X*

返回：

*   `event` Event
*   `url` String

当用户想要在应用中打开一个 url 的时候被触发。URL 格式必须要提前标识才能被你的应用打开。

如果你想处理这个事件，你应该调用 `event.preventDefault()` 。

### 事件：'activate' *OS X*

返回：

*   `event` Event
*   `hasVisibleWindows` Boolean

当应用被激活时触发，常用于点击应用的 dock 图标的时候。

### 事件：'browser-window-blur'

返回：

*   `event` Event
*   `window` BrowserWindow

当一个 BrowserWindow 失去焦点的时候触发。

### 事件：'browser-window-focus'

返回：

*   `event` Event
*   `window` BrowserWindow

当一个 BrowserWindow 获得焦点的时候触发。

### 事件：'browser-window-created'

返回：

*   `event` Event
*   `window` BrowserWindow

当一个 BrowserWindow 被创建的时候触发。

### 事件：'certificate-error'

返回：

*   `event` Event
*   `webContents` WebContents
*   `url` String - URL 地址
*   `error` String - 错误码
*   `certificate` Object
    *   `data` Buffer - PEM 编码数据
    *   `issuerName` String - 发行者的公有名称
*   `callback` Function

当对 `url` 验证 `certificate` 证书失败的时候触发，如果需要信任这个证书，你需要阻止默认行为 `event.preventDefault()` 并且 调用 `callback(true)`。

```
session.on('certificate-error', function(event, webContents, url, error, certificate, callback) {
  if (url == "https://github.com") {
    // 验证逻辑。
    event.preventDefault();
    callback(true);
  } else {
    callback(false);
  }
}); 
```

### 事件：'select-client-certificate'

返回：

*   `event` Event
*   `webContents` WebContents
*   `url` String - URL 地址
*   `certificateList` [Object]
    *   `data` Buffer - PEM 编码数据
    *   `issuerName` String - 发行者的公有名称
*   `callback` Function

当一个客户端认证被请求的时候被触发。

`url` 指的是请求客户端认证的网页地址，调用 `callback` 时需要传入一个证书列表中的证书。

需要通过调用 `event.preventDefault()` 来防止应用自动使用第一个证书进行验证。如下所示：

```
app.on('select-certificate', function(event, host, url, list, callback) {
  event.preventDefault();
  callback(list[0]);
}) 
```

### 事件: 'login'

返回：

*   `event` Event
*   `webContents` WebContents
*   `request` Object
    *   `method` String
    *   `url` URL
    *   `referrer` URL
*   `authInfo` Object
    *   `isProxy` Boolean
    *   `scheme` String
    *   `host` String
    *   `port` Integer
    *   `realm` String
*   `callback` Function

当 `webContents` 要做进行一次 HTTP 登陆验证时被触发。

默认情况下，Electron 会取消所有的验证行为，如果需要重写这个行为，你需要用 `event.preventDefault()` 来阻止默认行为，并且 用 `callback(username, password)` 来进行验证。

```
app.on('login', function(event, webContents, request, authInfo, callback) {
  event.preventDefault();
  callback('username', 'secret');
}) 
```

### 事件：'gpu-process-crashed'

当 GPU 进程崩溃时触发。

## 方法列表

`app` 对象拥有以下的方法：

**请注意** 有的方法只能用于特定的操作系统。

### `app.quit()`

试图关掉所有的窗口。`before-quit` 事件将会最先被触发。如果所有的窗口都被成功关闭了， `will-quit` 事件将会被触发，默认下应用将会被关闭。

这个方法保证了所有的 `beforeunload` 和 `unload` 事件处理器被正确执行。假如一个窗口的 `beforeunload` 事件处理器返回 `false`，那么整个应用可能会取消退出。

### `app.hide()` *OS X*

隐藏所有的应用窗口，不是最小化.

### `app.show()` *OS X*

隐藏后重新显示所有的窗口，不会自动选中他们。

### `app.exit(exitCode)`

*   `exitCode` 整数

带着`exitCode`退出应用.

所有的窗口会被立刻关闭，不会询问用户。`before-quit` 和 `will-quit` 这 2 个事件不会被触发

### `app.getAppPath()`

返回当前应用所在的文件路径。

### `app.getPath(name)`

*   `name` String

返回一个与 `name` 参数相关的特殊文件夹或文件路径。当失败时抛出一个 `Error` 。

你可以通过名称请求以下的路径：

*   `home` 用户的 home 文件夹（主目录）
*   `appData` 当前用户的应用数据文件夹，默认对应：
    *   `%APPDATA%` Windows 中
    *   `$XDG_CONFIG_HOME` or `~/.config` Linux 中
    *   `~/Library/Application Support` OS X 中
*   `userData` 储存你应用程序设置文件的文件夹，默认是 `appData` 文件夹附加应用的名称
*   `temp` 临时文件夹
*   `exe` 当前的可执行文件
*   `module` `libchromiumcontent` 库
*   `desktop` 当前用户的桌面文件夹
*   `documents` 用户文档目录的路径
*   `downloads` 用户下载目录的路径.
*   `music` 用户音乐目录的路径.
*   `pictures` 用户图片目录的路径.
*   `videos` 用户视频目录的路径.

### `app.setPath(name, path)`

*   `name` String
*   `path` String

重写某个 `name` 的路径为 `path`，`path` 可以是一个文件夹或者一个文件，这个和 `name` 的类型有关。 如果这个路径指向的文件夹不存在，这个文件夹将会被这个方法创建。 如果错误则会抛出 `Error`。

`name` 参数只能使用 `app.getPath` 中定义过 `name`。

默认情况下，网页的 cookie 和缓存都会储存在 `userData` 文件夹。 如果你想要改变这个位置，你需要在 `app` 模块中的 `ready` 事件被触发之前重写 `userData` 的路径。

### `app.getVersion()`

返回加载应用程序的版本。如果应用程序的 `package.json` 文件中没有写版本号， 将会返回当前包或者可执行文件的版本。

### `app.getName()`

返回当前应用程序的 `package.json` 文件中的名称。

由于 npm 的命名规则，通常 `name` 字段是一个短的小写字符串。但是应用名的完整名称通常是首字母大写的，你应该单独使用一个 `productName` 字段，用于表示你的应用程序的完整名称。Electron 会优先使用这个字段作为应用名。

### `app.setName(name)`

*   `name` String

重写当前应用的名字

### `app.getLocale()`

返回当前应用程序的语言。

### `app.addRecentDocument(path)` *OS X* *Windows*

*   `path` String

在最近访问的文档列表中添加 `path`。

这个列表由操作系统进行管理。在 Windows 中您可以通过任务条进行访问，在 OS X 中你可以通过 dock 菜单进行访问。

### `app.clearRecentDocuments()` *OS X* *Windows*

清除最近访问的文档列表。

### `app.setUserTasks(tasks)` *Windows*

*   `tasks` [Task] - 一个由 Task 对象构成的数组

将 `tasks` 添加到 Windows 中 JumpList 功能的 [Tasks](http://msdn.microsoft.com/en-us/library/windows/desktop/dd378460(v=vs.85).aspx#tasks) 分类中。

`tasks` 中的 `Task` 对象格式如下：

`Task` Object

*   `program` String - 执行程序的路径，通常你应该说明当前程序的路径为 `process.execPath` 字段。
*   `arguments` String - 当 `program` 执行时的命令行参数。
*   `title` String - JumpList 中显示的标题。
*   `description` String - 对这个任务的描述。
*   `iconPath` String - JumpList 中显示的图标的绝对路径，可以是一个任意包含一个图标的资源文件。通常来说，你可以通过指明 `process.execPath` 来显示程序中的图标。
*   `iconIndex` Integer - 图标文件中的采用的图标位置。如果一个图标文件包括了多个图标，就需要设置这个值以确定使用的是哪一个图标。 如果这个图标文件中只包含一个图标，那么这个值为 0。

### `app.allowNTLMCredentialsForAllDomains(allow)`

*   `allow` Boolean

动态设置是否总是为 HTTP NTLM 或 Negotiate 认证发送证书。通常来说，Electron 只会对本地网络（比如和你处在一个域中的计算机）发 送 NTLM / Kerberos 证书。但是假如网络设置得不太好，可能这个自动探测会失效，所以你可以通过这个接口自定义 Electron 对所有 URL 的行为。

### `app.makeSingleInstance(callback)`

*   `callback` Function

这个方法可以让你的应用在同一时刻最多只会有一个实例，否则你的应用可以被运行多次并产生多个实例。你可以利用这个接口保证只有一个实例正 常运行，其余的实例全部会被终止并退出。

如果多个实例同时运行，那么第一个被运行的实例中 `callback` 会以 `callback(argv, workingDirectory)` 的形式被调用。其余的实例 会被终止。 `argv` 是一个包含了这个实例的命令行参数列表的数组，`workingDirectory` 是这个实例目前的运行目录。通常来说，我们会用通过将应用在 主屏幕上激活，并且取消最小化，来提醒用户这个应用已经被打开了。

在 `app` 的 `ready` 事件后，`callback` 才有可能被调用。

如果当前实例为第一个实例，那么在这个方法将会返回 `false` 来保证它继续运行。否则将会返回 `true` 来让它立刻退出。

在 OS X 中，如果用户通过 Finder、`open-file` 或者 `open-url` 打开应用，系统会强制确保只有一个实例在运行。但是如果用户是通过 命令行打开，这个系统机制会被忽略，所以你仍然需要靠这个方法来保证应用为单实例运行的。

下面是一个简单的例子。我们可以通过这个例子了解如何确保应用为单实例运行状态。

```
var myWindow = null;

var shouldQuit = app.makeSingleInstance(function(commandLine, workingDirectory) {
  // 当另一个实例运行的时候，这里将会被调用，我们需要激活应用的窗口
  if (myWindow) {
    if (myWindow.isMinimized()) myWindow.restore();
    myWindow.focus();
  }
  return true;
});

// 这个实例是多余的实例，需要退出
if (shouldQuit) {
  app.quit();
  return;
}

// 创建窗口、继续加载应用、应用逻辑等……
app.on('ready', function() {
}); 
```

### `app.setAppUserModelId(id)` *Windows*

*   `id` String

改变当前应用的 [Application User Model ID](https://msdn.microsoft.com/en-us/library/windows/desktop/dd378459(v=vs.85).aspx) 为 `id`.

### `app.isAeroGlassEnabled()` *Windows*

如果 [DWM composition](https://msdn.microsoft.com/en-us/library/windows/desktop/aa969540.aspx)(Aero Glass) 启用 了，那么这个方法会返回 `true`，否则是 `false`。你可以用这个方法来决定是否要开启透明窗口特效，因为如果用户没开启 DWM，那么透明窗 口特效是无效的。

举个例子：

```
let browserOptions = {width: 1000, height: 800};

// 只有平台支持的时候才使用透明窗口
if (process.platform !== 'win32' || app.isAeroGlassEnabled()) {
  browserOptions.transparent = true;
  browserOptions.frame = false;
}

// 创建窗口
win = new BrowserWindow(browserOptions);

// 转到某个网页
if (browserOptions.transparent) {
  win.loadURL('file://' + __dirname + '/index.html');
} else {
  // 没有透明特效，我们应该用某个只包含基本样式的替代解决方案。
  win.loadURL('file://' + __dirname + '/fallback.html');
} 
```

### `app.commandLine.appendSwitch(switch[, value])`

通过可选的参数 `value` 给 Chromium 中添加一个命令行开关。

**注意** 这个方法不会影响 `process.argv`，我们通常用这个方法控制一些底层 Chromium 行为。

### `app.commandLine.appendArgument(value)`

给 Chromium 中直接添加一个命令行参数，这个参数 `value` 的引号和格式必须正确。

**注意** 这个方法不会影响 `process.argv`。

### `app.dock.bounce([type])` *OS X*

*   `type` String - 可选参数，可以是 `critical` 或 `informational`。默认为 `informational`。

当传入的是 `critical` 时，dock 中的应用将会开始弹跳，直到这个应用被激活或者这个请求被取消。

当传入的是 `informational` 时，dock 中的图标只会弹跳一秒钟。但是，这个请求仍然会激活，直到应用被激活或者请求被取消。

这个方法返回的返回值表示这个请求的 ID。

### `app.dock.cancelBounce(id)` *OS X*

*   `id` Integer

取消这个 `id` 对应的请求。

### `app.dock.setBadge(text)` *OS X*

*   `text` String

设置应用在 dock 中显示的字符串。

### `app.dock.getBadge()` *OS X*

返回应用在 dock 中显示的字符串。

### `app.dock.hide()` *OS X*

隐藏应用在 dock 中的图标。

### `app.dock.show()` *OS X*

显示应用在 dock 中的图标。

### `app.dock.setMenu(menu)` *OS X*

*   `menu` Menu

设置应用的 [dock 菜单](https://developer.apple.com/library/mac/documentation/Carbon/Conceptual/customizing_docktile/concepts/dockconcepts.html#//apple_ref/doc/uid/TP30000986-CH2-TPXREF103).

### `app.dock.setIcon(image)` *OS X*

*   `image` NativeImage

设置应用在 dock 中显示的图标。

# autoUpdater

这个模块提供了一个到 `Squirrel` 自动更新框架的接口。

## 平台相关的提示

虽然 `autoUpdater` 模块提供了一套各平台通用的接口，但是在每个平台间依然会有一些微小的差异。

### OS X

在 OS X 上，`autoUpdater` 模块依靠的是内置的 [Squirrel.Mac](https://github.com/Squirrel/Squirrel.Mac)，这意味着你不需要依靠其他的设置就能使用。关于 更新服务器的配置，你可以通过阅读 [Server Support](https://github.com/Squirrel/Squirrel.Mac#server-support) 这篇文章来了解。

### Windows

在 Windows 上，你必须使用安装程序将你的应用装到用户的计算机上，所以比较推荐的方法是用 [grunt-electron-installer](https://github.com/atom/grunt-electron-installer) 这个模块来自动生成一个 Windows 安装向导。

Squirrel 自动生成的安装向导会生成一个带 [Application User Model ID](https://msdn.microsoft.com/en-us/library/windows/desktop/dd378459(v=vs.85).aspx) 的快捷方式。 Application User Model ID 的格式是 `com.squirrel.PACKAGE_ID.YOUR_EXE_WITHOUT_DOT_EXE`, 比如 像 `com.squirrel.slack.Slack` 和 `com.squirrel.code.Code` 这样的。你应该在自己的应用中使用 `app.setAppUserModelId` 方法设置相同的 API，不然 Windows 将不能正确地把你的应用固定在任务栏上。

服务器端的配置和 OS X 也是不一样的，你可以阅读 [Squirrel.Windows](https://github.com/Squirrel/Squirrel.Windows) 这个文档来获得详细信息。

### Linux

Linux 下没有任何的自动更新支持，所以我们推荐用各个 Linux 发行版的包管理器来分发你的应用。

## 事件列表

`autoUpdater` 对象会触发以下的事件：

### 事件：'error'

返回：

*   `error` Error

当更新发生错误的时候触发。

### 事件：'checking-for-update'

当开始检查更新的时候触发。

### 事件：'update-available'

当发现一个可用更新的时候触发，更新包下载会自动开始。

### 事件：'update-not-available'

当没有可用更新的时候触发。

### 事件：'update-downloaded'

返回：

*   `event` Event
*   `releaseNotes` String - 新版本更新公告
*   `releaseName` String - 新的版本号
*   `releaseDate` Date - 新版本发布的日期
*   `updateURL` String - 更新地址

在更新下载完成的时候触发。

在 Windows 上只有 `releaseName` 是有效的。

## 方法列表

`autoUpdater` 对象有以下的方法：

### `autoUpdater.setFeedURL(url)`

*   `url` String

设置检查更新的 `url`，并且初始化自动更新。这个 `url` 一旦设置就无法更改。

### `autoUpdater.checkForUpdates()`

向服务端查询现在是否有可用的更新。在调用这个方法之前，必须要先调用 `setFeedURL`。

### `autoUpdater.quitAndInstall()`

在下载完成后，重启当前的应用并且安装更新。这个方法应该仅在 `update-downloaded` 事件触发后被调用。

# BrowserWindow

`BrowserWindow` 类让你有创建一个浏览器窗口的权力。例如:

```
// In the main process.
const BrowserWindow = require('electron').BrowserWindow;

// Or in the renderer process.
const BrowserWindow = require('electron').remote.BrowserWindow;

var win = new BrowserWindow({ width: 800, height: 600, show: false });
win.on('closed', function() {
  win = null;
});

win.loadURL('https://github.com');
win.show(); 
```

你也可以不通过 chrome 创建窗口，使用 Frameless Window API.

## Class: BrowserWindow

`BrowserWindow` 是一个 [EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter).

通过 `options` 可以创建一个具有本质属性的 `BrowserWindow` .

### `new BrowserWindow([options])`

*   `options` Object
    *   `width` Integer - 窗口宽度,单位像素. 默认是 `800`.
    *   `height` Integer - 窗口高度,单位像素. 默认是 `600`.
    *   `x` Integer - 窗口相对于屏幕的左偏移位置.默认居中.
    *   `y` Integer - 窗口相对于屏幕的顶部偏移位置.默认居中.
    *   `useContentSize` Boolean - `width` 和 `height` 使用 web 网页 size, 这意味着实际窗口的 size 应该包括窗口框架的 size，稍微会大一点，默认为 `false`.
    *   `center` Boolean - 窗口屏幕居中.
    *   `minWidth` Integer - 窗口最小宽度，默认为 `0`.
    *   `minHeight` Integer - 窗口最小高度，默认为 `0`.
    *   `maxWidth` Integer - 窗口最大宽度，默认无限制.
    *   `maxHeight` Integer - 窗口最大高度，默认无限制.
    *   `resizable` Boolean - 是否可以改变窗口 size，默认为 `true`.
    *   `movable` Boolean - 窗口是否可以拖动. 在 Linux 上无效. 默认为 `true`.
    *   `minimizable` Boolean - 窗口是否可以最小化. 在 Linux 上无效. 默认为 `true`.
    *   `maximizable` Boolean - 窗口是否可以最大化. 在 Linux 上无效. 默认为 `true`.
    *   `closable` Boolean - 窗口是否可以关闭. 在 Linux 上无效. 默认为 `true`.
    *   `alwaysOnTop` Boolean - 窗口是否总是显示在其他窗口之前. 在 Linux 上无效. 默认为 `false`.
    *   `fullscreen` Boolean - 窗口是否可以全屏幕. 当明确设置值为 When `false` ，全屏化按钮将会隐藏，在 OS X 将禁用. 默认 `false`.
    *   `fullscreenable` Boolean - 在 OS X 上，全屏化按钮是否可用，默认为 `true`.
    *   `skipTaskbar` Boolean - 是否在人物栏中显示窗口. 默认是`false`.
    *   `kiosk` Boolean - kiosk 方式. 默认为 `false`.
    *   `title` String - 窗口默认 title. 默认 `"Electron"`.
    *   `icon` NativeImage - 窗口图标, 如果不设置，窗口将使用可用的默认图标.
    *   `show` Boolean - 窗口创建的时候是否显示. 默认为 `true`.
    *   `frame` Boolean - 指定 `false` 来创建一个 Frameless Window. 默认为 `true`.
    *   `acceptFirstMouse` Boolean - 是否允许单击 web view 来激活窗口 . 默认为 `false`.
    *   `disableAutoHideCursor` Boolean - 当 typing 时是否隐藏鼠标.默认 `false`.
    *   `autoHideMenuBar` Boolean - 除非点击 `Alt`，否则隐藏菜单栏.默认为 `false`.
    *   `enableLargerThanScreen` Boolean - 是否允许允许改变窗口大小大于屏幕. 默认是 `false`.
    *   `backgroundColor` String -窗口的 background color 值为十六进制,如 `#66CD00` 或 `#FFF` 或 `#80FFFFFF` (支持透明度). 默认为在 Linux 和 Windows 上为 `#000` (黑色) , Mac 上为 `#FFF`(或透明).
    *   `hasShadow` Boolean - 窗口是否有阴影. 只在 OS X 上有效. 默认为 `true`.
    *   `darkTheme` Boolean - 为窗口使用 dark 主题, 只在一些拥有 GTK+3 桌面环境上有效. 默认为 `false`.
    *   `transparent` Boolean - 窗口 透明. 默认为 `false`.
    *   `type` String - 窗口 type, 默认普通窗口. 下面查看更多.
    *   `titleBarStyle` String - 窗口标题栏样式. 下面查看更多.
    *   `webPreferences` Object - 设置界面特性. 下面查看更多.

`type` 的值和效果不同平台展示效果不同，具体:

*   Linux, 可用值为 `desktop`, `dock`, `toolbar`, `splash`, `notification`.
*   OS X, 可用值为 `desktop`, `textured`.
    *   `textured` type 添加金属梯度效果 (`NSTexturedBackgroundWindowMask`).
    *   `desktop` 设置窗口在桌面背景窗口水平 (`kCGDesktopWindowLevel - 1`). 注意桌面窗口不可聚焦, 不可不支持键盘和鼠标事件, 但是可以使用 `globalShortcut` 来解决输入问题.

`titleBarStyle` 只在 OS X 10.10 Yosemite 或更新版本上支持. 可用值:

*   `default` 以及无值, 显示在 Mac 标题栏上为不透明的标准灰色.
*   `hidden` 隐藏标题栏，内容充满整个窗口, 然后它依然在左上角，仍然受标准窗口控制.
*   `hidden-inset`主体隐藏，显示小的控制按钮在窗口边缘.

`webPreferences` 参数是个对象，它的属性:

*   `nodeIntegration` Boolean - 是否完整支持 node. 默认为 `true`.
*   `preload` String - 界面的其它脚本运行之前预先加载一个指定脚本. 这个脚本将一直可以使用 node APIs 无论 node integration 是否开启. 脚本路径为绝对路径. 当 node integration 关闭, 预加载的脚本将从全局范围重新引入 node 的全局引用标志. 查看例子 here.
*   `session` Session - 设置界面 session. 而不是直接忽略 session 对象 , 也可用 `partition` 来代替, 它接受一个 partition 字符串. 当同时使用 `session` 和 `partition`, `session` 优先级更高. 默认使用默认 session.
*   `partition` String - 通过 session 的 partition 字符串来设置界面 session. 如果 `partition` 以 `persist:` 开头, 这个界面将会为所有界面使用相同的 `partition`. 如果没有 `persist:` 前缀, 界面使用历史 session. 通过分享同一个 `partition`, 所有界面使用相同的 session. 默认使用默认 session.
*   `zoomFactor` Number - 界面默认缩放值, `3.0` 表示 `300%`. 默认 `1.0`.
*   `javascript` Boolean - 开启 javascript 支持. 默认为`true`.
*   `webSecurity` Boolean - 当设置为 `false`, 它将禁用相同地方的规则 (通常测试服), 并且如果有 2 个非用户设置的参数，就设置 `allowDisplayingInsecureContent` 和 `allowRunningInsecureContent` 的值为 `true`. 默认为 `true`.
*   `allowDisplayingInsecureContent` Boolean -允许一个使用 https 的界面来展示由 http URLs 传过来的资源. 默认`false`.
*   `allowRunningInsecureContent` Boolean - Boolean -允许一个使用 https 的界面来渲染由 http URLs 提交的 html,css,javascript. 默认为 `false`.
*   `images` Boolean - 开启图片使用支持. 默认 `true`.
*   `textAreasAreResizable` Boolean - textArea 可以编辑. 默认为 `true`.
*   `webgl` Boolean - 开启 WebGL 支持. 默认为 `true`.
*   `webaudio` Boolean - 开启 WebAudio 支持. 默认为 `true`.
*   `plugins` Boolean - 是否开启插件支持. 默认为 `false`.
*   `experimentalFeatures` Boolean - 开启 Chromium 的 可测试 特性. 默认为 `false`.
*   `experimentalCanvasFeatures` Boolean - 开启 Chromium 的 canvas 可测试特性. 默认为 `false`.
*   `directWrite` Boolean - 开启窗口的 DirectWrite font 渲染系统. 默认为 `true`.
*   `blinkFeatures` String - 以 `,` 分隔的特性列表, 如 `CSSVariables,KeyboardEventKey`. 被支持的所有特性可在 [setFeatureEnabledFromString](https://code.google.com/p/chromium/codesearch#chromium/src/out/Debug/gen/blink/platform/RuntimeEnabledFeatures.cpp&sq=package:chromium&type=cs&l=527) 中找到.
*   `defaultFontFamily` Object - 设置 font-family 默认字体.
    *   `standard` String - 默认为 `Times New Roman`.
    *   `serif` String - 默认为 `Times New Roman`.
    *   `sansSerif` String - 默认为 `Arial`.
    *   `monospace` String - 默认为 `Courier New`.
*   `defaultFontSize` Integer - 默认为 `16`.
*   `defaultMonospaceFontSize` Integer - 默认为 `13`.
*   `minimumFontSize` Integer - 默认为 `0`.
*   `defaultEncoding` String - 默认为 `ISO-8859-1`.

## 事件

`BrowserWindow` 对象可触发下列事件:

**注意:** 一些事件只能在特定 os 环境中触发，已经尽可能地标出.

### Event: 'page-title-updated'

返回:

*   `event` Event

当文档改变标题时触发,使用 `event.preventDefault()` 可以阻止原窗口的标题改变.

### Event: 'close'

返回:

*   `event` Event

在窗口要关闭的时候触发. 它在 DOM 的 `beforeunload` and `unload` 事件之前触发.使用 `event.preventDefault()` 可以取消这个操作

通常你想通过 `beforeunload` 处理器来决定是否关闭窗口，但是它也会在窗口重载的时候被触发. 在 Electron 中，返回一个空的字符串或 `false` 可以取消关闭.例如:

```
window.onbeforeunload = function(e) {
  console.log('I do not want to be closed');

  // Unlike usual browsers, in which a string should be returned and the user is
  // prompted to confirm the page unload, Electron gives developers more options.
  // Returning empty string or false would prevent the unloading now.
  // You can also use the dialog API to let the user confirm closing the application.
  e.returnValue = false;
}; 
```

### Event: 'closed'

当窗口已经关闭的时候触发.当你接收到这个事件的时候，你应当删除对已经关闭的窗口的引用对象和避免再次使用它.

### Event: 'unresponsive'

在界面卡死的时候触发事件.

### Event: 'responsive'

在界面恢复卡死的时候触发.

### Event: 'blur'

在窗口失去焦点的时候触发.

### Event: 'focus'

在窗口获得焦点的时候触发.

### Event: 'maximize'

在窗口最大化的时候触发.

### Event: 'unmaximize'

在窗口退出最大化的时候触发.

### Event: 'minimize'

在窗口最小化的时候触发.

### Event: 'restore'

在窗口从最小化恢复的时候触发.

### Event: 'resize'

在窗口 size 改变的时候触发.

### Event: 'move'

在窗口移动的时候触发.

注意：在 OS X 中别名为 `moved`.

### Event: 'moved' *OS X*

在窗口移动的时候触发.

### Event: 'enter-full-screen'

在的窗口进入全屏状态时候触发.

### Event: 'leave-full-screen'

在的窗口退出全屏状态时候触发.

### Event: 'enter-html-full-screen'

在的窗口通过 html api 进入全屏状态时候触发.

### Event: 'leave-html-full-screen'

在的窗口通过 html api 退出全屏状态时候触发.

### Event: 'app-command' *Windows*

在请求一个[App Command](https://msdn.microsoft.com/en-us/library/windows/desktop/ms646275(v=vs.85).aspx)的时候触发. 典型的是键盘媒体或浏览器命令, Windows 上的 "Back" 按钮用作鼠标也会触发.

```
someWindow.on('app-command', function(e, cmd) {
  // Navigate the window back when the user hits their mouse back button
  if (cmd === 'browser-backward' && someWindow.webContents.canGoBack()) {
    someWindow.webContents.goBack();
  }
}); 
```

### Event: 'scroll-touch-begin' *OS X*

在滚动条事件开始的时候触发.

### Event: 'scroll-touch-end' *OS X*

在滚动条事件结束的时候触发.

## 方法

`BrowserWindow` 对象有如下方法:

### `BrowserWindow.getAllWindows()`

返回一个所有已经打开了窗口的对象数组.

### `BrowserWindow.getFocusedWindow()`

返回应用当前获得焦点窗口,如果没有就返回 `null`.

### `BrowserWindow.fromWebContents(webContents)`

*   `webContents` WebContents

根据 `webContents` 查找窗口.

### `BrowserWindow.fromId(id)`

*   `id` Integer

根据 id 查找窗口.

### `BrowserWindow.addDevToolsExtension(path)`

*   `path` String

添加位于 `path` 的开发者工具栏扩展,并且返回扩展项的名字.

这个扩展会被添加到历史，所以只需要使用这个 API 一次，这个 api 不可用作编程使用.

### `BrowserWindow.removeDevToolsExtension(name)`

*   `name` String

删除开发者工具栏名为 `name` 的扩展.

## 实例属性

使用 `new BrowserWindow` 创建的实例对象，有如下属性:

```
// In this example `win` is our instance
var win = new BrowserWindow({ width: 800, height: 600 }); 
```

### `win.webContents`

这个窗口的 `WebContents` 对象，所有与界面相关的事件和方法都通过它完成的.

查看 `webContents` documentation 的方法和事件.

### `win.id`

窗口的唯一 id.

## 实例方法

使用 `new BrowserWindow` 创建的实例对象，有如下方法:

**注意:** 一些方法只能在特定 os 环境中调用，已经尽可能地标出.

### `win.destroy()`

强制关闭窗口, `unload` and `beforeunload` 不会触发，并且 `close` 也不会触发, 但是它保证了 `closed` 触发.

### `win.close()`

尝试关闭窗口，这与用户点击关闭按钮的效果一样. 虽然网页可能会取消关闭，查看 close event.

### `win.focus()`

窗口获得焦点.

### `win.isFocused()`

返回 boolean, 窗口是否获得焦点.

### `win.show()`

展示并且使窗口获得焦点.

### `win.showInactive()`

展示窗口但是不获得焦点.

### `win.hide()`

隐藏窗口.

### `win.isVisible()`

返回 boolean, 窗口是否可见.

### `win.maximize()`

窗口最大化.

### `win.unmaximize()`

取消窗口最大化.

### `win.isMaximized()`

返回 boolean, 窗口是否最大化.

### `win.minimize()`

窗口最小化. 在一些 os 中，它将在 dock 中显示.

### `win.restore()`

将最小化的窗口恢复为之前的状态.

### `win.isMinimized()`

返回 boolean, 窗口是否最小化.

### `win.setFullScreen(flag)`

*   `flag` Boolean

设置是否全屏.

### `win.isFullScreen()`

返回 boolean, 窗口是否全屏化.

### `win.setAspectRatio(aspectRatio[, extraSize])` *OS X*

*   `aspectRatio` 维持部分视图内容窗口的高宽比值.
*   `extraSize` Object (可选) - 维持高宽比值时不包含的额外 size.
    *   `width` Integer
    *   `height` Integer

由一个窗口来维持高宽比值. `extraSize` 允许开发者使用它，它的单位为像素，不包含在 `aspectRatio` 中.这个 API 可用来区分窗口的 size 和内容的 size .

想象一个普通可控的 HD video 播放器窗口. 假如左边缘有 15 控制像素，右边缘有 25 控制像素，在播放器下面有 50 控制像素.为了在播放器内保持一个 16:9 的高宽比例，我们可以调用这个 api 传入参数 16/9 and [ 40, 50 ].第二个参数不管网页中的额外的宽度和高度在什么位置，只要它们存在就行.只需要把网页中的所有额外的高度和宽度加起来就行.

### `win.setBounds(options[, animate])`

*   `options` Object
    *   `x` Integer
    *   `y` Integer
    *   `width` Integer
    *   `height` Integer
*   `animate` Boolean (可选) *OS X*

重新设置窗口的宽高值，并且移动到指定的 `x`, `y` 位置.

### `win.getBounds()`

返回一个对象，它包含了窗口的宽，高，x 坐标，y 坐标.

### `win.setSize(width, height[, animate])`

*   `width` Integer
*   `height` Integer
*   `animate` Boolean (可选) *OS X*

重新设置窗口的宽高值.

### `win.getSize()`

返回一个数组，它包含了窗口的宽，高.

### `win.setContentSize(width, height[, animate])`

*   `width` Integer
*   `height` Integer
*   `animate` Boolean (可选) *OS X*

重新设置窗口客户端的宽高值（例如网页界面）.

### `win.getContentSize()`

返回一个数组，它包含了窗口客户端的宽，高.

### `win.setMinimumSize(width, height)`

*   `width` Integer
*   `height` Integer

设置窗口最小化的宽高值.

### `win.getMinimumSize()`

返回一个数组，它包含了窗口最小化的宽，高.

### `win.setMaximumSize(width, height)`

*   `width` Integer
*   `height` Integer

设置窗口最大化的宽高值.

### `win.getMaximumSize()`

返回一个数组，它包含了窗口最大化的宽，高.

### `win.setResizable(resizable)`

*   `resizable` Boolean

设置窗口是否可以被用户改变 size.

### `win.isResizable()`

返回 boolean,窗口是否可以被用户改变 size.

### `win.setMovable(movable)` *OS X* *Windows*

*   `movable` Boolean

设置窗口是否可以被用户拖动. Linux 无效.

### `win.isMovable()` *OS X* *Windows*

返回 boolean,窗口是否可以被用户拖动. Linux 总是返回 `true`.

### `win.setMinimizable(minimizable)` *OS X* *Windows*

*   `minimizable` Boolean

设置窗口是否可以最小化. Linux 无效.

### `win.isMinimizable()` *OS X* *Windows*

返回 boolean,窗口是否可以最小化. Linux 总是返回 `true`.

### `win.setMaximizable(maximizable)` *OS X* *Windows*

*   `maximizable` Boolean

设置窗口是否可以最大化. Linux 无效.

### `win.isMaximizable()` *OS X* *Windows*

返回 boolean,窗口是否可以最大化. Linux 总是返回 `true`.

### `win.setFullScreenable(fullscreenable)`

*   `fullscreenable` Boolean

设置点击最大化按钮是否可以全屏或最大化窗口.

### `win.isFullScreenable()`

返回 boolean,点击最大化按钮是否可以全屏或最大化窗口.

### `win.setClosable(closable)` *OS X* *Windows*

*   `closable` Boolean

设置窗口是否可以人为关闭. Linux 无效.

### `win.isClosable()` *OS X* *Windows*

返回 boolean,窗口是否可以人为关闭. Linux 总是返回 `true`.

### `win.setAlwaysOnTop(flag)`

*   `flag` Boolean

是否设置这个窗口始终在其他窗口之上.设置之后，这个窗口仍然是一个普通的窗口，不是一个不可以获得焦点的工具箱窗口.

### `win.isAlwaysOnTop()`

返回 boolean,当前窗口是否始终在其它窗口之前.

### `win.center()`

窗口居中.

### `win.setPosition(x, y[, animate])`

*   `x` Integer
*   `y` Integer
*   `animate` Boolean (可选) *OS X*

移动窗口到对应的 `x` and `y` 坐标.

### `win.getPosition()`

返回一个包含当前窗口位置的数组.

### `win.setTitle(title)`

*   `title` String

改变原窗口的 title.

### `win.getTitle()`

返回原窗口的 title.

**注意:** 界面 title 可能和窗口 title 不相同.

### `win.flashFrame(flag)`

*   `flag` Boolean

开始或停止显示窗口来获得用户的关注.

### `win.setSkipTaskbar(skip)`

*   `skip` Boolean

让窗口不在任务栏中显示.

### `win.setKiosk(flag)`

*   `flag` Boolean

进入或离开 kiosk 模式.

### `win.isKiosk()`

返回 boolean,是否进入或离开 kiosk 模式.

### `win.getNativeWindowHandle()`

以 `Buffer` 形式返回这个具体平台的窗口的句柄.

windows 上句柄类型为 `HWND` ，OS X `NSView*` ， Linux `Window`.

### `win.hookWindowMessage(message, callback)` *Windows*

*   `message` Integer
*   `callback` Function

拦截 windows 消息，在 WndProc 接收到消息时触发 `callback`函数.

### `win.isWindowMessageHooked(message)` *Windows*

*   `message` Integer

返回 `true` or `false` 来代表是否拦截到消息.

### `win.unhookWindowMessage(message)` *Windows*

*   `message` Integer

不拦截窗口消息.

### `win.unhookAllWindowMessages()` *Windows*

窗口消息全部不拦截.

### `win.setRepresentedFilename(filename)` *OS X*

*   `filename` String

设置窗口当前文件路径，并且将这个文件的图标放在窗口标题栏上.

### `win.getRepresentedFilename()` *OS X*

获取窗口当前文件路径.

### `win.setDocumentEdited(edited)` *OS X*

*   `edited` Boolean

明确指出窗口文档是否可以编辑，如果可以编辑则将标题栏的图标变成灰色.

### `win.isDocumentEdited()` *OS X*

返回 boolean,当前窗口文档是否可编辑.

### `win.focusOnWebView()`

### `win.blurWebView()`

### `win.capturePage([rect, ]callback)`

*   `rect` Object (可选) - 捕获 Page 位置
    *   `x` Integer
    *   `y` Integer
    *   `width` Integer
    *   `height` Integer
*   `callback` Function

捕获 `rect` 中的 page 的快照.完成后将调用回调函数 `callback` 并返回 `image` . `image` 是存储了快照信息的 NativeImage 实例.如果不设置 `rect` 则将捕获所有可见 page.

### `win.print([options])`

类似 `webContents.print([options])`

### `win.printToPDF(options, callback)`

类似 `webContents.printToPDF(options, callback)`

### `win.loadURL(url[, options])`

类似 `webContents.loadURL(url[, options])`.

### `win.reload()`

类似 `webContents.reload`.

### `win.setMenu(menu)` *Linux* *Windows*

*   `menu` Menu

设置菜单栏的 `menu` ，设置它为 `null` 则表示不设置菜单栏.

### `win.setProgressBar(progress)`

*   `progress` Double

在进度条中设置进度值，有效范围 [0, 1.0].

当进度小于 0 时则不显示进度; 当进度大于 0 时显示结果不确定.

在 libux 上，只支持 Unity 桌面环境，需要指明 `*.desktop` 文件并且在 `package.json` 中添加文件名字.默认它为 `app.getName().desktop`.

### `win.setOverlayIcon(overlay, description)` *Windows 7+*

*   `overlay` NativeImage - 在底部任务栏右边显示图标.
*   `description` String - 描述.

向当前任务栏添加一个 16 x 16 像素的图标，通常用来覆盖一些应用的状态，或者直接来提示用户.

### `win.setHasShadow(hasShadow)` *OS X*

*   `hasShadow` (Boolean)

设置窗口是否应该有阴影.在 Windows 和 Linux 系统无效.

### `win.hasShadow()` *OS X*

返回 boolean,设置窗口是否有阴影.在 Windows 和 Linux 系统始终返回 `true`.

### `win.setThumbarButtons(buttons)` *Windows 7+*

*   `buttons` Array

在窗口的任务栏 button 布局出为缩略图添加一个有特殊 button 的缩略图工具栏. 返回一个 `Boolean` 对象来指示是否成功添加这个缩略图工具栏.

因为空间有限，缩略图工具栏上的 button 数量不应该超过 7 个.一旦设置了，由于平台限制，就不能移动它了.但是你可使用一个空数组来调用 api 来清除 buttons .

所有 `buttons` 是一个 `Button` 对象数组:

*   `Button` Object
    *   `icon` NativeImage - 在工具栏上显示的图标.
    *   `click` Function
    *   `tooltip` String (可选) - tooltip 文字.
    *   `flags` Array (可选) - 控制 button 的状态和行为. 默认它是 `['enabled']`.

`flags` 是一个数组，它包含下面这些 `String`s:

*   `enabled` - button 为激活状态并且开放给用户.
*   `disabled` -button 不可用. 目前它有一个可见的状态来表示它不会响应你的行为.
*   `dismissonclick` - 点击 button，这个缩略窗口直接关闭.
*   `nobackground` - 不绘制边框，仅仅使用图像.
*   `hidden` - button 对用户不可见.
*   `noninteractive` - button 可用但是不可响应; 也不显示按下的状态. 它的值意味着这是一个在通知单使用 button 的实例.

### `win.showDefinitionForSelection()` *OS X*

在界面查找选中文字时显示弹出字典.

### `win.setAutoHideMenuBar(hide)`

*   `hide` Boolean

设置窗口的菜单栏是否可以自动隐藏. 一旦设置了，只有当用户按下 `Alt` 键时则显示.

如果菜单栏已经可见，调用 `setAutoHideMenuBar(true)` 则不会立刻隐藏.

### `win.isMenuBarAutoHide()`

返回 boolean,窗口的菜单栏是否可以自动隐藏.

### `win.setMenuBarVisibility(visible)`

*   `visible` Boolean

设置菜单栏是否可见.如果菜单栏自动隐藏，用户仍然可以按下 `Alt` 键来显示.

### `win.isMenuBarVisible()`

返回 boolean,菜单栏是否可见.

### `win.setVisibleOnAllWorkspaces(visible)`

*   `visible` Boolean

设置窗口是否在所有地方都可见.

**注意:** 这个 api 在 windows 无效.

### `win.isVisibleOnAllWorkspaces()`

返回 boolean,窗口是否在所有地方都可见.

**注意:** 在 windows 上始终返回 false.

### `win.setIgnoreMouseEvents(ignore)` *OS X*

*   `ignore` Boolean

忽略窗口的所有鼠标事件.

# contentTracing

`content-tracing` 模块是用来收集由底层的 Chromium content 模块 产生的搜索数据. 这个模块不具备 web 接口，所有需要我们在 chrome 浏览器中添加 `chrome://tracing/` 来加载生成文件从而查看结果.

```
const contentTracing = require('electron').contentTracing;

const options = {
  categoryFilter: '*',
  traceOptions: 'record-until-full,enable-sampling'
}

contentTracing.startRecording(options, function() {
  console.log('Tracing started');

  setTimeout(function() {
    contentTracing.stopRecording('', function(path) {
      console.log('Tracing data recorded to ' + path);
    });
  }, 5000);
}); 
```

## 方法

`content-tracing` 模块的方法如下:

### `contentTracing.getCategories(callback)`

*   `callback` Function

获得一组分类组. 分类组可以更改为新的代码路径。

一旦所有的子进程都接受到了`getCategories`方法请求, 分类组将调用 `callback`.

### `contentTracing.startRecording(options, callback)`

*   `options` Object
    *   `categoryFilter` String
    *   `traceOptions` String
*   `callback` Function

开始向所有进程进行记录.(recording)

一旦收到可以开始记录的请求，记录将会立马启动并且在子进程是异步记录听的. 当所有的子进程都收到 `startRecording` 请求的时候，`callback` 将会被调用.

`categoryFilter`是一个过滤器，它用来控制那些分类组应该被用来查找.过滤器应当有一个可选的 `-` 前缀来排除匹配的分类组.不允许同一个列表既是包含又是排斥.

例子:

*   `test_MyTest*`,
*   `test_MyTest*,test_OtherStuff`,
*   `"-excluded_category1,-excluded_category2`

`traceOptions` 控制着哪种查找应该被启动，这是一个用逗号分隔的列表.可用参数如下:

*   `record-until-full`
*   `record-continuously`
*   `trace-to-console`
*   `enable-sampling`
*   `enable-systrace`

前 3 个参数是来查找记录模块，并且以后都互斥.如果在`traceOptions` 中超过一个跟踪 记录模式，那最后一个的优先级最高.如果没有指明跟踪 记录模式，那么它默认为 `record-until-full`.

在 `traceOptions` 中的参数被解析应用之前，查找参数初始化默认为 (`record_mode` 设置为 `record-until-full`, `enable_sampling` 和 `enable_systrace` 设置为 `false`).

### `contentTracing.stopRecording(resultFilePath, callback)`

*   `resultFilePath` String
*   `callback` Function

停止对所有子进程的记录.

子进程通常缓存查找数据，并且仅仅将数据截取和发送给主进程.这有利于在通过 IPC 发送查找数据之前减小查找时的运行开销，这样做很有价值.因此，发送查找数据，我们应当异步通知所有子进程来截取任何待查找的数据.

一旦所有子进程接收到了 `stopRecording` 请求，将调用 `callback` ，并且返回一个包含查找数据的文件.

如果 `resultFilePath` 不为空，那么将把查找数据写入其中，否则写入一个临时文件.实际文件路径如果不为空，则将调用 `callback` .

### `contentTracing.startMonitoring(options, callback)`

*   `options` Object
    *   `categoryFilter` String
    *   `traceOptions` String
*   `callback` Function

开始向所有进程进行监听.(monitoring)

一旦收到可以开始监听的请求，记录将会立马启动并且在子进程是异步记监听的. 当所有的子进程都收到 `startMonitoring` 请求的时候，`callback` 将会被调用.

### `contentTracing.stopMonitoring(callback)`

*   `callback` Function

停止对所有子进程的监听.

一旦所有子进程接收到了 `stopMonitoring` 请求，将调用 `callback` .

### `contentTracing.captureMonitoringSnapshot(resultFilePath, callback)`

*   `resultFilePath` String
*   `callback` Function

获取当前监听的查找数据.

子进程通常缓存查找数据，并且仅仅将数据截取和发送给主进程.因为如果直接通过 IPC 来发送查找数据的代价昂贵，我们宁愿避免不必要的查找运行开销.因此，为了停止查找，我们应当异步通知所有子进程来截取任何待查找的数据.

一旦所有子进程接收到了 `captureMonitoringSnapshot` 请求，将调用 `callback` ，并且返回一个包含查找数据的文件.

### `contentTracing.getTraceBufferUsage(callback)`

*   `callback` Function

通过查找 buffer 进程来获取百分比最大使用量.当确定了 TraceBufferUsage 的值确定的时候，就调用 `callback` .

### `contentTracing.setWatchEvent(categoryName, eventName, callback)`

*   `categoryName` String
*   `eventName` String
*   `callback` Function

任意时刻在任何进程上指定事件发生时将调用 `callback` .

### `contentTracing.cancelWatchEvent()`

取消 watch 事件. 如果启动查找，这或许会造成 watch 事件的回调函数 出错.

# dialog

`dialog` 模块提供了 api 来展示原生的系统对话框，例如打开文件框，alert 框，所以 web 应用可以给用户带来跟系统应用相同的体验.

对话框例子，展示了选择文件和目录:

```
var win = ...;  // BrowserWindow in which to show the dialog
const dialog = require('electron').dialog;
console.log(dialog.showOpenDialog({ properties: [ 'openFile', 'openDirectory', 'multiSelections' ]})); 
```

**OS X 上的注意事项**: 如果你想像 sheets 一样展示对话框，只需要在`browserWindow` 参数中提供一个 `BrowserWindow` 的引用对象.

## 方法

`dialog` 模块有以下方法:

### `dialog.showOpenDialog([browserWindow, ]options[, callback])`

*   `browserWindow` BrowserWindow (可选)
*   `options` Object
    *   `title` String
    *   `defaultPath` String
    *   `filters` Array
    *   `properties` Array - 包含了对话框的特性值, 可以包含 `openFile`, `openDirectory`, `multiSelections` and `createDirectory`
*   `callback` Function (可选)

成功使用这个方法的话，就返回一个可供用户选择的文件路径数组，失败返回 `undefined`.

`filters` 当需要限定用户的行为的时候，指定一个文件数组给用户展示或选择. 例如:

```
{
  filters: [
    { name: 'Images', extensions: ['jpg', 'png', 'gif'] },
    { name: 'Movies', extensions: ['mkv', 'avi', 'mp4'] },
    { name: 'Custom File Type', extensions: ['as'] },
    { name: 'All Files', extensions: ['*'] }
  ]
} 
```

`extensions` 数组应当只包含扩展名，不应该包含通配符或'.'号 (例如 `'png'` 正确，但是 `'.png'` 和 `'*.png'` 不正确). 展示全部文件的话, 使用 `'*'` 通配符 (不支持其他通配符).

如果 `callback` 被调用, 将异步调用 API ，并且结果将用过 `callback(filenames)` 展示.

**注意:** 在 Windows 和 Linux ，一个打开的 dialog 不能既是文件选择框又是目录选择框, 所以如果在这些平台上设置 `properties` 的值为 `['openFile', 'openDirectory']` , 将展示一个目录选择框.

### `dialog.showSaveDialog([browserWindow, ]options[, callback])`

*   `browserWindow` BrowserWindow (可选)
*   `options` Object
    *   `title` String
    *   `defaultPath` String
    *   `filters` Array
*   `callback` Function (可选)

成功使用这个方法的话，就返回一个可供用户选择的文件路径数组，失败返回 `undefined`.

`filters` 指定展示一个文件类型数组, 例子 `dialog.showOpenDialog` .

如果 `callback` 被调用, 将异步调用 API ，并且结果将用过 `callback(filenames)` 展示.

### `dialog.showMessageBox([browserWindow, ]options[, callback])`

*   `browserWindow` BrowserWindow (可选)
*   `options` Object
    *   `type` String - 可以是 `"none"`, `"info"`, `"error"`, `"question"` 或 `"warning"`. 在 Windows, "question" 与 "info" 展示图标相同, 除非你使用 "icon" 参数.
    *   `buttons` Array - buttons 内容，数组.
    *   `defaultId` Integer - 在 message box 对话框打开的时候，设置默认 button 选中，值为在 buttons 数组中的 button 索引.
    *   `title` String - message box 的标题，一些平台不显示.
    *   `message` String - message box 内容.
    *   `detail` String - 额外信息.
    *   `icon` NativeImage
    *   `cancelId` Integer - 当用户关闭对话框的时候，不是通过点击对话框的 button，就返回值.默认值为对应 "cancel" 或 "no" 标签 button 的索引值, 或者如果没有这种 button，就返回 0\. 在 OS X 和 Windows 上， "Cancel" button 的索引值将一直是 `cancelId`, 不管之前是不是特别指出的.
    *   `noLink` Boolean - 在 Windows ，Electron 将尝试识别哪个 button 是普通 button (如 "Cancel" 或 "Yes"), 然后再对话框中以链接命令(command links)方式展现其它的 button . 这能让对话框展示得很炫酷.如果你不喜欢这种效果，你可以设置 `noLink` 为 `true`.
*   `callback` Function

展示 message box, 它会阻塞进程，直到 message box 关闭为止.返回点击按钮的索引值.

如果 `callback` 被调用, 将异步调用 API ，并且结果将用过 `callback(response)` 展示.

### `dialog.showErrorBox(title, content)`

展示一个传统的包含错误信息的对话框.

在 `app` 模块触发 `ready` 事件之前，这个 api 可以被安全调用，通常它被用来在启动的早期阶段报告错误. 在 Linux 上，如果在 `app` 模块触发 `ready` 事件之前调用，message 将会被触发显示 stderr，并且没有实际 GUI 框显示.

# globalShortcut

# global-shortcut

`global-shortcut` 模块可以便捷的为您设置(注册/注销)各种自定义操作的快捷键.

**Note**: 使用此模块注册的快捷键是系统全局的(QQ 截图那种), 不要在应用模块(app module)响应 `ready` 消息前使用此模块(注册快捷键).

```
var app = require('app');
var globalShortcut = require('global-shortcut');

app.on('ready', function() {
  // Register a 'ctrl+x' shortcut listener.
  var ret = globalShortcut.register('ctrl+x', function() {
    console.log('ctrl+x is pressed');
  })

  if (!ret) {
    console.log('registration failed');
  }

  // Check whether a shortcut is registered.
  console.log(globalShortcut.isRegistered('ctrl+x'));
});

app.on('will-quit', function() {
  // Unregister a shortcut.
  globalShortcut.unregister('ctrl+x');

  // Unregister all shortcuts.
  globalShortcut.unregisterAll();
}); 
```

## Methods

`global-shortcut` 模块包含以下函数:

### `globalShortcut.register(accelerator, callback)`

*   `accelerator` Accelerator
*   `callback` Function

注册 `accelerator` 快捷键. 当用户按下注册的快捷键时将会调用 `callback` 函数.

### `globalShortcut.isRegistered(accelerator)`

*   `accelerator` Accelerator

查询 `accelerator` 快捷键是否已经被注册过了,将会返回 `true`(已被注册) 或 `false`(未注册).

### `globalShortcut.unregister(accelerator)`

*   `accelerator` Accelerator

注销全局快捷键 `accelerator`.

### `globalShortcut.unregisterAll()`

注销本应用注册的所有全局快捷键.

# ipcMain

`ipcMain` 模块是类 [EventEmitter](https://nodejs.org/api/events.html) 的实例.当在主进程中使用它的时候，它控制着由渲染进程(web page)发送过来的异步或同步消息.从渲染进程发送过来的消息将触发事件.

## 发送消息

同样也可以从主进程向渲染进程发送消息，查看更多 webContents.send .

*   发送消息，事件名为 `channel`.
*   回应同步消息, 你可以设置 `event.returnValue`.
*   回应异步消息, 你可以使用 `event.sender.send(...)`.

一个例子，在主进程和渲染进程之间发送和处理消息:

```
// In main process.
const ipcMain = require('electron').ipcMain;
ipcMain.on('asynchronous-message', function(event, arg) {
  console.log(arg);  // prints "ping"
  event.sender.send('asynchronous-reply', 'pong');
});

ipcMain.on('synchronous-message', function(event, arg) {
  console.log(arg);  // prints "ping"
  event.returnValue = 'pong';
}); 
```

```
// In renderer process (web page).
const ipcRenderer = require('electron').ipcRenderer;
console.log(ipcRenderer.sendSync('synchronous-message', 'ping')); // prints "pong"

ipcRenderer.on('asynchronous-reply', function(event, arg) {
  console.log(arg); // prints "pong"
});
ipcRenderer.send('asynchronous-message', 'ping'); 
```

## 监听消息

`ipcMain` 模块有如下监听事件方法:

### `ipcMain.on(channel, listener)`

*   `channel` String
*   `listener` Function

监听 `channel`, 当新消息到达，将通过 `listener(event, args...)` 调用 `listener`.

### `ipcMain.once(channel, listener)`

*   `channel` String
*   `listener` Function

为事件添加一个一次性用的`listener` 函数.这个 `listener` 只有在下次的消息到达 `channel` 时被请求调用，之后就被删除了.

### `ipcMain.removeListener(channel, listener)`

*   `channel` String
*   `listener` Function

为特定的 `channel` 从监听队列中删除特定的 `listener` 监听者.

### `ipcMain.removeAllListeners([channel])`

*   `channel` String (可选)

删除所有监听者，或特指的 `channel` 的所有监听者.

## 事件对象

传递给 `callback` 的 `event` 对象有如下方法:

### `event.returnValue`

将此设置为在一个同步消息中返回的值.

### `event.sender`

返回发送消息的 `webContents` ，你可以调用 `event.sender.send` 来回复异步消息，更多信息 webContents.send.

# Menu

# 菜单

`menu` 类可以用来创建原生菜单，它可用作应用菜单和 [context 菜单](https://developer.mozilla.org/en-US/docs/Mozilla/Tech/XUL/PopupGuide/ContextMenus).

这个模块是一个主进程的模块，并且可以通过 `remote` 模块给渲染进程调用.

每个菜单有一个或几个菜单项 menu items，并且每个菜单项可以有子菜单.

下面这个例子是在网页(渲染进程)中通过 remote 模块动态创建的菜单，并且右键显示:

```
<!-- index.html -->
<script> const remote = require('electron').remote;
const Menu = remote.Menu;
const MenuItem = remote.MenuItem;

var menu = new Menu();
menu.append(new MenuItem({ label: 'MenuItem1', click: function() { console.log('item 1 clicked'); } }));
menu.append(new MenuItem({ type: 'separator' }));
menu.append(new MenuItem({ label: 'MenuItem2', type: 'checkbox', checked: true }));

window.addEventListener('contextmenu', function (e) {
  e.preventDefault();
  menu.popup(remote.getCurrentWindow());
}, false); </script> 
```

例子，在渲染进程中使用模板 api 创建应用菜单:

```
var template = [
  {
    label: 'Edit',
    submenu: [
      {
        label: 'Undo',
        accelerator: 'CmdOrCtrl+Z',
        role: 'undo'
      },
      {
        label: 'Redo',
        accelerator: 'Shift+CmdOrCtrl+Z',
        role: 'redo'
      },
      {
        type: 'separator'
      },
      {
        label: 'Cut',
        accelerator: 'CmdOrCtrl+X',
        role: 'cut'
      },
      {
        label: 'Copy',
        accelerator: 'CmdOrCtrl+C',
        role: 'copy'
      },
      {
        label: 'Paste',
        accelerator: 'CmdOrCtrl+V',
        role: 'paste'
      },
      {
        label: 'Select All',
        accelerator: 'CmdOrCtrl+A',
        role: 'selectall'
      },
    ]
  },
  {
    label: 'View',
    submenu: [
      {
        label: 'Reload',
        accelerator: 'CmdOrCtrl+R',
        click: function(item, focusedWindow) {
          if (focusedWindow)
            focusedWindow.reload();
        }
      },
      {
        label: 'Toggle Full Screen',
        accelerator: (function() {
          if (process.platform == 'darwin')
            return 'Ctrl+Command+F';
          else
            return 'F11';
        })(),
        click: function(item, focusedWindow) {
          if (focusedWindow)
            focusedWindow.setFullScreen(!focusedWindow.isFullScreen());
        }
      },
      {
        label: 'Toggle Developer Tools',
        accelerator: (function() {
          if (process.platform == 'darwin')
            return 'Alt+Command+I';
          else
            return 'Ctrl+Shift+I';
        })(),
        click: function(item, focusedWindow) {
          if (focusedWindow)
            focusedWindow.toggleDevTools();
        }
      },
    ]
  },
  {
    label: 'Window',
    role: 'window',
    submenu: [
      {
        label: 'Minimize',
        accelerator: 'CmdOrCtrl+M',
        role: 'minimize'
      },
      {
        label: 'Close',
        accelerator: 'CmdOrCtrl+W',
        role: 'close'
      },
    ]
  },
  {
    label: 'Help',
    role: 'help',
    submenu: [
      {
        label: 'Learn More',
        click: function() { require('electron').shell.openExternal('http://electron.atom.io') }
      },
    ]
  },
];

if (process.platform == 'darwin') {
  var name = require('electron').remote.app.getName();
  template.unshift({
    label: name,
    submenu: [
      {
        label: 'About ' + name,
        role: 'about'
      },
      {
        type: 'separator'
      },
      {
        label: 'Services',
        role: 'services',
        submenu: []
      },
      {
        type: 'separator'
      },
      {
        label: 'Hide ' + name,
        accelerator: 'Command+H',
        role: 'hide'
      },
      {
        label: 'Hide Others',
        accelerator: 'Command+Alt+H',
        role: 'hideothers'
      },
      {
        label: 'Show All',
        role: 'unhide'
      },
      {
        type: 'separator'
      },
      {
        label: 'Quit',
        accelerator: 'Command+Q',
        click: function() { app.quit(); }
      },
    ]
  });
  // Window menu.
  template[3].submenu.push(
    {
      type: 'separator'
    },
    {
      label: 'Bring All to Front',
      role: 'front'
    }
  );
}

var menu = Menu.buildFromTemplate(template);
Menu.setApplicationMenu(menu); 
```

## 类: Menu

### `new Menu()`

创建一个新的菜单.

## 方法

`菜单` 类有如下方法:

### `Menu.setApplicationMenu(menu)`

*   `menu` Menu

在 OS X 上设置应用菜单 `menu` . 在 windows 和 linux，是为每个窗口都在其顶部设置菜单 `menu`.

### `Menu.sendActionToFirstResponder(action)` *OS X*

*   `action` String

发送 `action` 给应用的第一个响应器.这个用来模仿 Cocoa 菜单的默认行为，通常你只需要使用 `MenuItem` 的属性 `role`.

查看更多 OS X 的原生 action [OS X Cocoa Event Handling Guide](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/EventOverview/EventArchitecture/EventArchitecture.html#//apple_ref/doc/uid/10000060i-CH3-SW7) .

### `Menu.buildFromTemplate(template)`

*   `template` Array

一般来说，`template` 只是用来创建 MenuItem 的数组 `参数` .

你也可以向 `template` 元素添加其它东西，并且他们会变成已经有的菜单项的属性.

## 实例方法

`menu` 对象有如下实例方法

### `menu.popup([browserWindow, x, y, positioningItem])`

*   `browserWindow` BrowserWindow (可选) - 默认为 `null`.
*   `x` Number (可选) - 默认为 -1.
*   `y` Number (**必须** 如果 x 设置了) - 默认为 -1.
*   `positioningItem` Number (可选) *OS X* - 在指定坐标鼠标位置下面的菜单项的索引. 默认为 -1.

在 `browserWindow` 中弹出 context menu .你可以选择性地提供指定的 `x, y` 来设置菜单应该放在哪里,否则它将默认地放在当前鼠标的位置.

### `menu.append(menuItem)`

*   `menuItem` MenuItem

添加菜单项.

### `menu.insert(pos, menuItem)`

*   `pos` Integer
*   `menuItem` MenuItem

在制定位置添加菜单项.

### `menu.items()`

获取一个菜单项数组.

## OS X Application 上的菜单的注意事项

相对于 windows 和 linux, OS X 上的应用菜单是完全不同的 style，这里是一些注意事项，来让你的菜单项更原生化.

### 标准菜单

在 OS X 上，有很多系统定义的标准菜单，例如 `Services` and `Windows` 菜单.为了让你的应用更标准化，你可以为你的菜单的 `role` 设置值，然后 electron 将会识别他们并且让你的菜单更标准:

*   `window`
*   `help`
*   `services`

### 标准菜单项行为

OS X 为一些菜单项提供了标准的行为方法，例如 `About xxx`, `Hide xxx`, and `Hide Others`. 为了让你的菜单项的行为更标准化，你应该为菜单项设置 `role` 属性.

### 主菜单名

在 OS X ，无论你设置的什么标签，应用菜单的第一个菜单项的标签始终未你的应用名字.想要改变它的话，你必须通过修改应用绑定的 `Info.plist` 文件来修改应用名字.更多信息参考[About Information Property List Files](https://developer.apple.com/library/ios/documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) .

## 为制定浏览器窗口设置菜单 (*Linux* *Windows*)

浏览器窗口的[`setMenu` 方法][setMenu] 能够设置菜单为特定浏览器窗口的类型.

## 菜单项位置

当通过 `Menu.buildFromTemplate` 创建菜单的时候，你可以使用 `position` and `id` 来放置菜单项.

`MenuItem` 的属性 `position` 格式为 `[placement]=[id]`，`placement` 取值为 `before`, `after`, 或 `endof` 和 `id`， `id` 是菜单已经存在的菜单项的唯一 ID:

*   `before` - 在对应引用 id 菜单项之前插入. 如果引用的菜单项不存在，则将其插在菜单末尾.
*   `after` - 在对应引用 id 菜单项之后插入. 如果引用的菜单项不存在，则将其插在菜单末尾.
*   `endof` - 在逻辑上包含对应引用 id 菜单项的集合末尾插入. 如果引用的菜单项不存在, 则将使用给定的 id 创建一个新的集合，并且这个菜单项将插入.

当一个菜档项插入成功了，所有的没有插入的菜单项将一个接一个地在后面插入.所以如果你想在同一个位置插入一组菜单项，只需要为这组菜单项的第一个指定位置.

### 例子

模板:

```
[
  {label: '4', id: '4'},
  {label: '5', id: '5'},
  {label: '1', id: '1', position: 'before=4'},
  {label: '2', id: '2'},
  {label: '3', id: '3'}
] 
```

菜单:

```
- 1
- 2
- 3
- 4
- 5 
```

模板:

```
[
  {label: 'a', position: 'endof=letters'},
  {label: '1', position: 'endof=numbers'},
  {label: 'b', position: 'endof=letters'},
  {label: '2', position: 'endof=numbers'},
  {label: 'c', position: 'endof=letters'},
  {label: '3', position: 'endof=numbers'}
] 
```

菜单:

```
- ---
- a
- b
- c
- ---
- 1
- 2
- 3 
```

[setMenu]: [`github.com/electron/electron/blob/master/docs/api/browser-window.md#winsetmenumenu-linux-windows`](https://github.com/electron/electron/blob/master/docs/api/browser-window.md#winsetmenumenu-linux-windows)

# MenuItem

# 菜单项

菜单项模块允许你向应用或[menu](https://github.com/heyunjiang/electron/blob/master/docs-translations/zh-CN/api/menu.md)添加选项。

查看[menu](https://github.com/heyunjiang/electron/blob/master/docs-translations/zh-CN/api/menu.md)例子。

## 类：MenuItem

使用下面的方法创建一个新的 `MenuItem`

### new MenuItem(options)

*   `options` Object
    *   `click` Function - 当菜单项被点击的时候，使用 `click(menuItem,browserWindow)` 调用
    *   `role` String - 定义菜单项的行为，在指定 `click` 属性时将会被忽略
    *   `type` String - 取值 `normal`，`separator`，`checkbox`or`radio`
    *   `label` String
    *   `sublabel` String
    *   `accelerator` [Accelerator](https://github.com/heyunjiang/electron/blob/master/docs/api/accelerator.md)
    *   `icon` [NativeImage](https://github.com/heyunjiang/electron/blob/master/docs/api/native-image.md)
    *   `enabled` Boolean
    *   `visible` Boolean
    *   `checked` Boolean
    *   `submenu` Menu - 应当作为 `submenu` 菜单项的特定类型，当它作为 `type: 'submenu'` 菜单项的特定类型时可以忽略。如果它的值不是 `Menu`，将自动转为 `Menu.buildFromTemplate`。
    *   `id` String - 标志一个菜单的唯一性。如果被定义使用，它将被用作这个菜单项的参考位置属性。
    *   `position` String - 定义给定的菜单的具体指定位置信息。

在创建菜单项时，如果有匹配的方法，建议指定 `role` 属性，不需要人为操作它的行为，这样菜单使用可以给用户最好的体验。

`role`属性值可以为：

*   `undo`
*   `redo`
*   `cut`
*   `copy`
*   `paste`
*   `selectall`
*   `minimize` - 最小化当前窗口
*   `close` - 关闭当前窗口

在 OS X 上，`role` 还可以有以下值：

*   `about` - 匹配 `orderFrontStandardAboutPanel` 行为
*   `hide` - 匹配 `hide` 行为
*   `hideothers` - 匹配 `hideOtherApplications` 行为
*   `unhide` - 匹配 `unhideAllApplications` 行为
*   `front` - 匹配 `arrangeInFront` 行为
*   `window` - "Window" 菜单项
*   `help` - "Help" 菜单项
*   `services` - "Services" 菜单项

# powerMonitor

`power-monitor`模块是用来监听能源区改变的.只能在主进程中使用.在 `app` 模块的 `ready` 事件触发之后就不能使用这个模块了.

例如:

```
app.on('ready', function() {
  require('electron').powerMonitor.on('suspend', function() {
    console.log('The system is going to sleep');
  });
}); 
```

## 事件

`power-monitor` 模块可以触发下列事件:

### Event: 'suspend'

在系统挂起的时候触发.

### Event: 'resume'

在系统恢复继续工作的时候触发. Emitted when system is resuming.

### Event: 'on-ac'

在系统使用交流电的时候触发. Emitted when the system changes to AC power.

### Event: 'on-battery'

在系统使用电池电源的时候触发. Emitted when system changes to battery power.

# powerSaveBlocker

`powerSaveBlocker` 模块是用来阻止应用系统进入睡眠模式的，因此这允许应用保持系统和屏幕继续工作.

例如:

```
const powerSaveBlocker = require('electron').powerSaveBlocker;

var id = powerSaveBlocker.start('prevent-display-sleep');
console.log(powerSaveBlocker.isStarted(id));

powerSaveBlocker.stop(id); 
```

## 方法

`powerSaveBlocker` 模块有如下方法:

### `powerSaveBlocker.start(type)`

*   `type` String - 强行保存阻塞类型.
    *   `prevent-app-suspension` - 阻止应用挂起. 保持系统活跃，但是允许屏幕不亮. 用例: 下载文件或者播放音频.
    *   `prevent-display-sleep`- 阻止应用进入休眠. 保持系统和屏幕活跃，屏幕一直亮. 用例: 播放音频.

开始阻止系统进入睡眠模式.返回一个整数，这个整数标识了保持活跃的 blocker.

**注意:** `prevent-display-sleep` 有更高的优先级 `prevent-app-suspension`. 只有最高优先级生效. 换句话说, `prevent-display-sleep` 优先级永远高于 `prevent-app-suspension`.

例如, A 请求调用了 `prevent-app-suspension`, B 请求调用了 `prevent-display-sleep`. `prevent-display-sleep` 将一直工作，直到 B 停止调用. 在那之后, `prevent-app-suspension` 才起效.

### `powerSaveBlocker.stop(id)`

*   `id` Integer - 通过 `powerSaveBlocker.start` 返回的保持活跃的 blocker id.

让指定 blocker 停止活跃.

### `powerSaveBlocker.isStarted(id)`

*   `id` Integer - 通过 `powerSaveBlocker.start` 返回的保持活跃的 blocker id.

返回 boolean， 是否对应的 `powerSaveBlocker` 已经启动.

# protocol

# 协议

`protocol` 模块可以注册一个自定义协议，或者使用一个已经存在的协议.

例子，使用一个与 `file://` 功能相似的协议 :

```
const electron = require('electron');
const app = electron.app;
const path = require('path');

app.on('ready', function() {
    var protocol = electron.protocol;
    protocol.registerFileProtocol('atom', function(request, callback) {
      var url = request.url.substr(7);
      callback({path: path.normalize(__dirname + '/' + url)});
    }, function (error) {
      if (error)
        console.error('Failed to register protocol')
    });
}); 
```

**注意:** 这个模块只有在 `app` 模块的 `ready` 事件触发之后才可使用.

## 方法

`protocol` 模块有如下方法:

### `protocol.registerStandardSchemes(schemes)`

*   `schemes` Array - 将一个自定义的方案注册为标准的方案.

一个标准的 `scheme` 遵循 RFC 3986 的 [generic URI syntax](https://tools.ietf.org/html/rfc3986#section-3) 标准. 这包含了 `file:` 和 `filesystem:`.

### `protocol.registerServiceWorkerSchemes(schemes)`

*   `schemes` Array - 将一个自定义的方案注册为处理 service workers.

### `protocol.registerFileProtocol(scheme, handler[, completion])`

*   `scheme` String
*   `handler` Function
*   `completion` Function (可选)

注册一个协议，用来发送响应文件.当通过这个协议来发起一个请求的时候，将使用 `handler(request, callback)` 来调用 `handler` .当 `scheme` 被成功注册或者完成(错误)时失败，将使用 `completion(null)` 调用 `completion`.

*   `request` Object
    *   `url` String
    *   `referrer` String
    *   `method` String
    *   `uploadData` Array (可选)
*   `callback` Function

`uploadData` 是一个 `data` 对象数组:

*   `data` Object
    *   `bytes` Buffer - 被发送的内容.
    *   `file` String - 上传的文件路径.

为了处理请求，调用 `callback` 时需要使用文件路径或者一个带 `path` 参数的对象, 例如 `callback(filePath)` 或 `callback({path: filePath})`.

当不使用任何参数调用 `callback` 时，你可以指定一个数字或一个带有 `error` 参数的对象，来标识 `request` 失败.你可以使用的 error number 可以参考 [net error list](https://code.google.com/p/chromium/codesearch#chromium/src/net/base/net_error_list.h).

默认 `scheme` 会被注册为一个 `http:` 协议，它与遵循 "generic URI syntax" 规则的协议解析不同，例如 `file:` ，所以你或许应该调用 `protocol.registerStandardSchemes` 来创建一个标准的 scheme.

### `protocol.registerBufferProtocol(scheme, handler[, completion])`

*   `scheme` String
*   `handler` Function
*   `completion` Function (可选)

注册一个 `scheme` 协议，用来发送响应 `Buffer` .

这个方法的用法类似 `registerFileProtocol`，除非使用一个 `Buffer` 对象，或一个有 `data`, `mimeType`, 和 `charset` 属性的对象来调用 `callback` .

例子:

```
protocol.registerBufferProtocol('atom', function(request, callback) {
  callback({mimeType: 'text/html', data: new Buffer('<h5>Response</h5>')});
}, function (error) {
  if (error)
    console.error('Failed to register protocol')
}); 
```

### `protocol.registerStringProtocol(scheme, handler[, completion])`

*   `scheme` String
*   `handler` Function
*   `completion` Function (可选)

注册一个 `scheme` 协议，用来发送响应 `String` .

这个方法的用法类似 `registerFileProtocol`，除非使用一个 `String` 对象，或一个有 `data`, `mimeType`, 和 `charset` 属性的对象来调用 `callback` .

### `protocol.registerHttpProtocol(scheme, handler[, completion])`

*   `scheme` String
*   `handler` Function
*   `completion` Function (可选)

注册一个 `scheme` 协议，用来发送 HTTP 请求作为响应.

这个方法的用法类似 `registerFileProtocol`，除非使用一个 `redirectRequest` 对象，或一个有 `url`, `method`, `referrer`, `uploadData` 和 `session` 属性的对象来调用 `callback` .

*   `redirectRequest` Object
    *   `url` String
    *   `method` String
    *   `session` Object (可选)
    *   `uploadData` Object (可选)

默认这个 HTTP 请求会使用当前 session .如果你想使用不同的 session 值，你应该设置 `session` 为 `null`.

POST 请求应当包含 `uploadData` 对象.

*   `uploadData` object
    *   `contentType` String - 内容的 MIME type.
    *   `data` String - 被发送的内容.

### `protocol.unregisterProtocol(scheme[, completion])`

*   `scheme` String
*   `completion` Function (可选)

注销自定义协议 `scheme`.

### `protocol.isProtocolHandled(scheme, callback)`

*   `scheme` String
*   `callback` Function

将使用一个布尔值来调用 `callback` ，这个布尔值标识了是否已经存在 `scheme` 的句柄了.

### `protocol.interceptFileProtocol(scheme, handler[, completion])`

*   `scheme` String
*   `handler` Function
*   `completion` Function (可选)

拦截 `scheme` 协议并且使用 `handler` 作为协议的新的句柄来发送响应文件.

### `protocol.interceptStringProtocol(scheme, handler[, completion])`

*   `scheme` String
*   `handler` Function
*   `completion` Function (可选)

拦截 `scheme` 协议并且使用 `handler` 作为协议的新的句柄来发送响应 `String`.

### `protocol.interceptBufferProtocol(scheme, handler[, completion])`

*   `scheme` String
*   `handler` Function
*   `completion` Function (可选)

拦截 `scheme` 协议并且使用 `handler` 作为协议的新的句柄来发送响应 `Buffer`.

### `protocol.interceptHttpProtocol(scheme, handler[, completion])`

*   `scheme` String
*   `handler` Function
*   `completion` Function (optional)

拦截 `scheme` 协议并且使用 `handler` 作为协议的新的句柄来发送新的响应 HTTP 请求. Intercepts `scheme` protocol and uses `handler` as the protocol's new handler which sends a new HTTP request as a response.

### `protocol.uninterceptProtocol(scheme[, completion])`

*   `scheme` String
*   `completion` Function 取消对 `scheme` 的拦截，使用它的原始句柄进行处理.

# session

`session` 模块可以用来创建一个新的 `Session` 对象.

你也可以通过使用 `webContents` 的属性 `session` 来使用一个已有页面的 `session` ，`webContents` 是`BrowserWindow` 的属性.

```
const BrowserWindow = require('electron').BrowserWindow;

var win = new BrowserWindow({ width: 800, height: 600 });
win.loadURL("http://github.com");

var ses = win.webContents.session; 
```

## 方法

`session` 模块有如下方法:

### session.fromPartition(partition)

*   `partition` String

从字符串 `partition` 返回一个新的 `Session` 实例.

如果 `partition` 以 `persist:` 开头，那么这个 page 将使用一个持久的 session，这个 session 将对应用的所有 page 可用.如果没前缀，这个 page 将使用一个历史 session.如果 `partition` 为空，那么将返回应用的默认 session .

## 属性

`session` 模块有如下属性:

### session.defaultSession

返回应用的默认 session 对象.

## Class: Session

可以在 `session` 模块中创建一个 `Session` 对象 :

```
const session = require('electron').session;

var ses = session.fromPartition('persist:name'); 
```

### 实例事件

实例 `Session` 有以下事件:

#### Event: 'will-download'

*   `event` Event
*   `item` DownloadItem
*   `webContents` WebContents

当 Electron 将要从 `webContents` 下载 `item` 时触发.

调用 `event.preventDefault()` 可以取消下载，并且在进程的下个 tick 中，这个 `item` 也不可用.

```
session.defaultSession.on('will-download', function(event, item, webContents) {
  event.preventDefault();
  require('request')(item.getURL(), function(data) {
    require('fs').writeFileSync('/somewhere', data);
  });
}); 
```

### 实例方法

实例 `Session` 有以下方法:

#### `ses.cookies`

`cookies` 赋予你全力来查询和修改 cookies. 例如:

```
// 查询所有 cookies.
session.defaultSession.cookies.get({}, function(error, cookies) {
  console.log(cookies);
});

// 查询与指定 url 相关的所有 cookies.
session.defaultSession.cookies.get({ url : "http://www.github.com" }, function(error, cookies) {
  console.log(cookies);
});

// 设置 cookie;
// may overwrite equivalent cookies if they exist.
var cookie = { url : "http://www.github.com", name : "dummy_name", value : "dummy" };
session.defaultSession.cookies.set(cookie, function(error) {
  if (error)
    console.error(error);
}); 
```

#### `ses.cookies.get(filter, callback)`

*   `filter` Object
    *   `url` String (可选) - 与获取 cookies 相关的 `url`.不设置的话就是从所有 url 获取 cookies .
    *   `name` String (可选) - 通过 name 过滤 cookies.
    *   `domain` String (可选) - 获取对应域名或子域名的 cookies .
    *   `path` String (可选) - 获取对应路径的 cookies .
    *   `secure` Boolean (可选) - 通过安全性过滤 cookies.
    *   `session` Boolean (可选) - 过滤掉 session 或 持久的 cookies.
*   `callback` Function

发送一个请求，希望获得所有匹配 `details` 的 cookies, 在完成的时候，将通过 `callback(error, cookies)` 调用 `callback`.

`cookies`是一个 `cookie` 对象.

*   `cookie` Object
    *   `name` String - cookie 名.
    *   `value` String - cookie 值.
    *   `domain` String - cookie 域名.
    *   `hostOnly` String - 是否 cookie 是一个 host-only cookie.
    *   `path` String - cookie 路径.
    *   `secure` Boolean - 是否是安全 cookie.
    *   `httpOnly` Boolean - 是否只是 HTTP cookie.
    *   `session` Boolean - cookie 是否是一个 session cookie 或一个带截至日期的持久 cookie .
    *   `expirationDate` Double (可选) - cookie 的截至日期，数值为 UNIX 纪元以来的秒数. 对 session cookies 不提供.

#### `ses.cookies.set(details, callback)`

*   `details` Object
    *   `url` String - 与获取 cookies 相关的 `url`.
    *   `name` String - cookie 名. 忽略默认为空.
    *   `value` String - cookie 值. 忽略默认为空.
    *   `domain` String - cookie 的域名. 忽略默认为空.
    *   `path` String - cookie 的路径. 忽略默认为空.
    *   `secure` Boolean - 是否已经进行了安全性标识. 默认为 false.
    *   `session` Boolean - 是否已经 HttpOnly 标识. 默认为 false.
    *   `expirationDate` Double - cookie 的截至日期，数值为 UNIX 纪元以来的秒数. 如果忽略, cookie 变为 session cookie.
*   `callback` Function

使用 `details` 设置 cookie, 完成时使用 `callback(error)` 掉哟个 `callback` .

#### `ses.cookies.remove(url, name, callback)`

*   `url` String - 与 cookies 相关的 `url`.
*   `name` String - 需要删除的 cookie 名.
*   `callback` Function

删除匹配 `url` 和 `name` 的 cookie, 完成时使用 `callback()`调用`callback`.

#### `ses.getCacheSize(callback)`

*   `callback` Function
    *   `size` Integer - 单位 bytes 的缓存 size.

返回 session 的当前缓存 size .

#### `ses.clearCache(callback)`

*   `callback` Function - 操作完成时调用

清空 session 的 HTTP 缓存.

#### `ses.clearStorageData([options, ]callback)`

*   `options` Object (可选)
    *   `origin` String - 应当遵循 `window.location.origin` 的格式 `scheme://host:port`.
    *   `storages` Array - 需要清理的 storages 类型, 可以包含 : `appcache`, `cookies`, `filesystem`, `indexdb`, `local storage`, `shadercache`, `websql`, `serviceworkers`
    *   `quotas` Array - 需要清理的类型指标, 可以包含: `temporary`, `persistent`, `syncable`.
*   `callback` Function - 操作完成时调用.

清除 web storages 的数据.

#### `ses.flushStorageData()`

将没有写入的 DOMStorage 写入磁盘.

#### `ses.setProxy(config, callback)`

*   `config` Object
    *   `pacScript` String - 与 PAC 文件相关的 URL.
    *   `proxyRules` String - 代理使用规则.
*   `callback` Function - 操作完成时调用.

设置 proxy settings.

当 `pacScript` 和 `proxyRules` 一同提供时，将忽略 `proxyRules`，并且使用 `pacScript` 配置 .

`proxyRules` 需要遵循下面的规则:

```
proxyRules = schemeProxies[";"<schemeProxies>]
schemeProxies = [<urlScheme>"="]<proxyURIList>
urlScheme = "http" | "https" | "ftp" | "socks"
proxyURIList = <proxyURL>[","<proxyURIList>]
proxyURL = [<proxyScheme>"://"]<proxyHost>[":"<proxyPort>] 
```

例子:

*   `http=foopy:80;ftp=foopy2` - 为 `http://` URL 使用 HTTP 代理 `foopy:80` , 和为 `ftp://` URL HTTP 代理 `foopy2:80` .
*   `foopy:80` - 为所有 URL 使用 HTTP 代理 `foopy:80` .
*   `foopy:80,bar,direct://` - 为所有 URL 使用 HTTP 代理 `foopy:80` , 如果 `foopy:80` 不可用，则切换使用 `bar`, 再往后就不使用代理了.
*   `socks4://foopy` - 为所有 URL 使用 SOCKS v4 代理 `foopy:1080`.
*   `http=foopy,socks5://bar.com` - 为所有 URL 使用 HTTP 代理 `foopy`, 如果 `foopy`不可用，则切换到 SOCKS5 代理 `bar.com`.
*   `http=foopy,direct://` - 为所有 http url 使用 HTTP 代理，如果 `foopy`不可用，则不使用代理.
*   `http=foopy;socks=foopy2` - 为所有 http url 使用 `foopy` 代理，为所有其他 url 使用 `socks4://foopy2` 代理.

### `ses.resolveProxy(url, callback)`

*   `url` URL
*   `callback` Function

解析 `url` 的代理信息.当请求完成的时候使用 `callback(proxy)` 调用 `callback`.

#### `ses.setDownloadPath(path)`

*   `path` String - 下载地址

设置下载保存地址，默认保存地址为各自 app 应用的 `Downloads`目录.

#### `ses.enableNetworkEmulation(options)`

*   `options` Object
    *   `offline` Boolean - 是否模拟网络故障.
    *   `latency` Double - 每毫秒的 RTT
    *   `downloadThroughput` Double - 每 Bps 的下载速率.
    *   `uploadThroughput` Double - 每 Bps 的上载速率.

通过给定配置的 `session` 来模拟网络.

```
// 模拟 GPRS 连接，使用的 50kbps 流量，500 毫秒的 rtt.
window.webContents.session.enableNetworkEmulation({
    latency: 500,
    downloadThroughput: 6400,
    uploadThroughput: 6400
});

// 模拟网络故障.
window.webContents.session.enableNetworkEmulation({offline: true}); 
```

#### `ses.disableNetworkEmulation()`

停止所有已经使用 `session` 的活跃模拟网络. 重置为原始网络类型.

#### `ses.setCertificateVerifyProc(proc)`

*   `proc` Function

为 `session` 设置证书验证过程，当请求一个服务器的证书验证时，使用 `proc(hostname, certificate, callback)` 调用 `proc`.调用 `callback(true)` 来接收证书，调用 `callback(false)` 来拒绝验证证书.

调用了 `setCertificateVerifyProc(null)` ，则将会回复到默认证书验证过程.

```
myWindow.webContents.session.setCertificateVerifyProc(function(hostname, cert, callback) {
  if (hostname == 'github.com')
    callback(true);
  else
    callback(false);
}); 
```

#### `ses.setPermissionRequestHandler(handler)`

*   `handler` Function
    *   `webContents` Object - WebContents 请求许可.
    *   `permission` String - 枚举了 'media', 'geolocation', 'notifications', 'midiSysex', 'pointerLock', 'fullscreen'.
    *   `callback` Function - 允许或禁止许可.

为对应 `session` 许可请求设置响应句柄.调用 `callback(true)` 接收许可，调用 `callback(false)` 禁止许可.

```
session.fromPartition(partition).setPermissionRequestHandler(function(webContents, permission, callback) {
  if (webContents.getURL() === host) {
    if (permission == "notifications") {
      callback(false); // denied.
      return;
    }
  }

  callback(true);
}); 
```

#### `ses.clearHostResolverCache([callback])`

*   `callback` Function (可选) - 操作结束调用.

清除主机解析缓存.

#### `ses.webRequest`

在其生命周期的不同阶段，`webRequest` API 设置允许拦截并修改请求内容.

每个 API 接收一可选的 `filter` 和 `listener`，当 API 事件发生的时候使用 `listener(details)` 调用 `listener`，`details` 是一个用来描述请求的对象.为 `listener` 使用 `null` 则会退定事件.

`filter` 是一个拥有 `urls` 属性的对象，这是一个 url 模式数组，这用来过滤掉不匹配指定 url 模式的请求.如果忽略 `filter` ，那么所有请求都将可以成功匹配.

所有事件的 `listener` 都有一个回调事件，当 `listener` 完成它的工作的时候，它将使用一个 `response` 对象来调用.

```
// 将所有请求的代理都修改为下列 url.
var filter = {
  urls: ["https://*.github.com/*", "*://electron.github.io"]
};

session.defaultSession.webRequest.onBeforeSendHeaders(filter, function(details, callback) {
  details.requestHeaders['User-Agent'] = "MyAgent";
  callback({cancel: false, requestHeaders: details.requestHeaders});
}); 
```

#### `ses.webRequest.onBeforeRequest([filter, ]listener)`

*   `filter` Object
*   `listener` Function

当一个请求即将开始的时候，使用 `listener(details, callback)` 调用 `listener`.

*   `details` Object
    *   `id` Integer
    *   `url` String
    *   `method` String
    *   `resourceType` String
    *   `timestamp` Double
    *   `uploadData` Array (可选)
*   `callback` Function

`uploadData` 是一个 `data` 数组对象:

*   `data` Object
    *   `bytes` Buffer - 被发送的内容.
    *   `file` String - 上载文件路径.

`callback` 必须使用一个 `response` 对象来调用:

*   `response` Object
    *   `cancel` Boolean (可选)
    *   `redirectURL` String (可选) - 原始请求阻止发送或完成，而不是重定向.

#### `ses.webRequest.onBeforeSendHeaders([filter, ]listener)`

*   `filter` Object
*   `listener` Function

一旦请求报文头可用了,在发送 HTTP 请求的之前，使用 `listener(details, callback)` 调用 `listener`.这也许会在服务器发起一个 tcp 连接，但是在发送任何 http 数据之前发生.

*   `details` Object
    *   `id` Integer
    *   `url` String
    *   `method` String
    *   `resourceType` String
    *   `timestamp` Double
    *   `requestHeaders` Object
*   `callback` Function

必须使用一个 `response` 对象来调用 `callback` :

*   `response` Object
    *   `cancel` Boolean (可选)
    *   `requestHeaders` Object (可选) - 如果提供了,将使用这些 headers 来创建请求.

#### `ses.webRequest.onSendHeaders([filter, ]listener)`

*   `filter` Object
*   `listener` Function

在一个请求正在发送到服务器的时候，使用 `listener(details)` 来调用 `listener` ，之前 `onBeforeSendHeaders` 修改部分响应可用，同时取消监听.

*   `details` Object
    *   `id` Integer
    *   `url` String
    *   `method` String
    *   `resourceType` String
    *   `timestamp` Double
    *   `requestHeaders` Object

#### `ses.webRequest.onHeadersReceived([filter,] listener)`

*   `filter` Object
*   `listener` Function

当 HTTP 请求报文头已经到达的时候，使用 `listener(details, callback)` 调用 `listener` .

*   `details` Object
    *   `id` String
    *   `url` String
    *   `method` String
    *   `resourceType` String
    *   `timestamp` Double
    *   `statusLine` String
    *   `statusCode` Integer
    *   `responseHeaders` Object
*   `callback` Function

必须使用一个 `response` 对象来调用 `callback` :

*   `response` Object
    *   `cancel` Boolean
    *   `responseHeaders` Object (可选) - 如果提供, 服务器将假定使用这些头来响应.

#### `ses.webRequest.onResponseStarted([filter, ]listener)`

*   `filter` Object
*   `listener` Function

当响应 body 的首字节到达的时候，使用 `listener(details)` 调用 `listener`.对 http 请求来说，这意味着状态线和响应头可用了.

*   `details` Object
    *   `id` Integer
    *   `url` String
    *   `method` String
    *   `resourceType` String
    *   `timestamp` Double
    *   `responseHeaders` Object
    *   `fromCache` Boolean - 标识响应是否来自磁盘 cache.
    *   `statusCode` Integer
    *   `statusLine` String

#### `ses.webRequest.onBeforeRedirect([filter, ]listener)`

*   `filter` Object
*   `listener` Function

当服务器的重定向初始化正要启动时，使用 `listener(details)` 调用 `listener`.

*   `details` Object
    *   `id` String
    *   `url` String
    *   `method` String
    *   `resourceType` String
    *   `timestamp` Double
    *   `redirectURL` String
    *   `statusCode` Integer
    *   `ip` String (可选) - 请求的真实服务器 ip 地址
    *   `fromCache` Boolean
    *   `responseHeaders` Object

#### `ses.webRequest.onCompleted([filter, ]listener)`

*   `filter` Object
*   `listener` Function

当请求完成的时候，使用 `listener(details)` 调用 `listener`.

*   `details` Object
    *   `id` Integer
    *   `url` String
    *   `method` String
    *   `resourceType` String
    *   `timestamp` Double
    *   `responseHeaders` Object
    *   `fromCache` Boolean
    *   `statusCode` Integer
    *   `statusLine` String

#### `ses.webRequest.onErrorOccurred([filter, ]listener)`

*   `filter` Object
*   `listener` Function

当一个错误发生的时候，使用 `listener(details)` 调用 `listener`.

*   `details` Object
    *   `id` Integer
    *   `url` String
    *   `method` String
    *   `resourceType` String
    *   `timestamp` Double
    *   `fromCache` Boolean
    *   `error` String - 错误描述.

# webContents

`webContents` 是一个 [事件发出者](http://nodejs.org/api/events.html#events_class_events_eventemitter).

它负责渲染并控制网页，也是 `BrowserWindow` 对象的属性.一个使用 `webContents` 的例子:

```
const BrowserWindow = require('electron').BrowserWindow;

var win = new BrowserWindow({width: 800, height: 1500});
win.loadURL("http://github.com");

var webContents = win.webContents; 
```

## 事件

`webContents` 对象可发出下列事件:

### Event: 'did-finish-load'

当导航完成时发出事件，`onload` 事件也完成.

### Event: 'did-fail-load'

返回:

*   `event` Event
*   `errorCode` Integer
*   `errorDescription` String
*   `validatedURL` String

这个事件类似 `did-finish-load` ，但是是在加载失败或取消加载时发出, 例如， `window.stop()` 请求结束.错误代码的完整列表和它们的含义都可以在 [here](https://code.google.com/p/chromium/codesearch#chromium/src/net/base/net_error_list.h) 找到.

### Event: 'did-frame-finish-load'

返回:

*   `event` Event
*   `isMainFrame` Boolean

当一个 frame 导航完成的时候发出事件.

### Event: 'did-start-loading'

当 tab 的 spinner 开始 spinning 的时候.

### Event: 'did-stop-loading'

当 tab 的 spinner 结束 spinning 的时候.

### Event: 'did-get-response-details'

返回:

*   `event` Event
*   `status` Boolean
*   `newURL` String
*   `originalURL` String
*   `httpResponseCode` Integer
*   `requestMethod` String
*   `referrer` String
*   `headers` Object

当有关请求资源的详细信息可用的时候发出事件. `status` 标识了 socket 链接来下载资源.

### Event: 'did-get-redirect-request'

返回:

*   `event` Event
*   `oldURL` String
*   `newURL` String
*   `isMainFrame` Boolean
*   `httpResponseCode` Integer
*   `requestMethod` String
*   `referrer` String
*   `headers` Object

当在请求资源时收到重定向的时候发出事件.

### Event: 'dom-ready'

返回:

*   `event` Event

当指定 frame 中的 文档加载完成的时候发出事件.

### Event: 'page-favicon-updated'

返回:

*   `event` Event
*   `favicons` Array - Array of URLs

当 page 收到图标 url 的时候发出事件.

### Event: 'new-window'

返回:

*   `event` Event
*   `url` String
*   `frameName` String
*   `disposition` String - 可为 `default`, `foreground-tab`, `background-tab`, `new-window` 和 `other`.
*   `options` Object - 创建新的 `BrowserWindow`时使用的参数.

当 page 请求打开指定 url 窗口的时候发出事件.这可以是通过 `window.open` 或一个外部连接如 `<a target='_blank'>` 发出的请求.

默认指定 `url` 的 `BrowserWindow` 会被创建.

调用 `event.preventDefault()` 可以用来阻止打开窗口.

### Event: 'will-navigate'

返回:

*   `event` Event
*   `url` String

当用户或 page 想要开始导航的时候发出事件.它可在当 `window.location` 对象改变或用户点击 page 中的链接的时候发生.

当使用 api(如 `webContents.loadURL` 和 `webContents.back`) 以编程方式来启动导航的时候，这个事件将不会发出.

它也不会在页内跳转发生， 例如点击锚链接或更新 `window.location.hash`.使用 `did-navigate-in-page` 事件可以达到目的.

调用 `event.preventDefault()` 可以阻止导航.

### Event: 'did-navigate'

返回:

*   `event` Event
*   `url` String

当一个导航结束时候发出事件.

页内跳转时不会发出这个事件，例如点击锚链接或更新 `window.location.hash`.使用 `did-navigate-in-page` 事件可以达到目的.

### Event: 'did-navigate-in-page'

返回:

*   `event` Event
*   `url` String

当页内导航发生的时候发出事件.

当页内导航发生的时候，page 的 url 改变，但是不会跳出界面.例如当点击锚链接时或者 DOM 的 `hashchange` 事件发生.

### Event: 'crashed'

当渲染进程崩溃的时候发出事件.

### Event: 'plugin-crashed'

返回:

*   `event` Event
*   `name` String
*   `version` String

当插件进程崩溃时候发出事件.

### Event: 'destroyed'

当 `webContents` 被删除的时候发出事件.

### Event: 'devtools-opened'

当开发者工具栏打开的时候发出事件.

### Event: 'devtools-closed'

当开发者工具栏关闭时候发出事件.

### Event: 'devtools-focused'

当开发者工具栏获得焦点或打开的时候发出事件.

### Event: 'certificate-error'

返回:

*   `event` Event
*   `url` URL
*   `error` String - The error code
*   `certificate` Object
    *   `data` Buffer - PEM encoded data
    *   `issuerName` String
*   `callback` Function

当验证证书或 `url` 失败的时候发出事件.

使用方法类似 `app` 的 `certificate-error` 事件.

### Event: 'select-client-certificate'

返回:

*   `event` Event
*   `url` URL
*   `certificateList` [Objects]
    *   `data` Buffer - PEM encoded data
    *   `issuerName` String - Issuer's Common Name
*   `callback` Function

当请求客户端证书的时候发出事件.

使用方法类似 `app` 的 `select-client-certificate` 事件.

### Event: 'login'

返回:

*   `event` Event
*   `request` Object
    *   `method` String
    *   `url` URL
    *   `referrer` URL
*   `authInfo` Object
    *   `isProxy` Boolean
    *   `scheme` String
    *   `host` String
    *   `port` Integer
    *   `realm` String
*   `callback` Function

当 `webContents` 想做基本验证的时候发出事件.

使用方法类似 the `login` event of `app`.

### Event: 'found-in-page'

返回:

*   `event` Event
*   `result` Object
    *   `requestId` Integer
    *   `finalUpdate` Boolean - 标识是否还有更多的值可以查看.
    *   `activeMatchOrdinal` Integer (可选) - 活动匹配位置
    *   `matches` Integer (可选) - 匹配数量.
    *   `selectionArea` Object (可选) - 协调首个匹配位置.

当使用 `webContents.findInPage` 进行页内查找并且找到可用值得时候发出事件.

### Event: 'media-started-playing'

当媒体开始播放的时候发出事件.

### Event: 'media-paused'

当媒体停止播放的时候发出事件.

### Event: 'did-change-theme-color'

当 page 的主题色时候发出事件.这通常由于引入了一个 meta 标签 :

```
<meta name='theme-color' content='#ff0000'> 
```

### Event: 'cursor-changed'

返回:

*   `event` Event
*   `type` String
*   `image` NativeImage (可选)
*   `scale` Float (可选)

当鼠标的类型发生改变的时候发出事件. `type` 的参数可以是 `default`, `crosshair`, `pointer`, `text`, `wait`, `help`, `e-resize`, `n-resize`, `ne-resize`, `nw-resize`, `s-resize`, `se-resize`, `sw-resize`, `w-resize`, `ns-resize`, `ew-resize`, `nesw-resize`, `nwse-resize`, `col-resize`, `row-resize`, `m-panning`, `e-panning`, `n-panning`, `ne-panning`, `nw-panning`, `s-panning`, `se-panning`, `sw-panning`, `w-panning`, `move`, `vertical-text`, `cell`, `context-menu`, `alias`, `progress`, `nodrop`, `copy`, `none`, `not-allowed`, `zoom-in`, `zoom-out`, `grab`, `grabbing`, `custom`.

如果 `type` 参数值为 `custom`, `image` 参数会在一个`NativeImage` 中控制自定义鼠标图片, 并且 `scale` 会控制图片的缩放比例.

## 实例方法

`webContents` 对象有如下的实例方法:

### `webContents.loadURL(url[, options])`

*   `url` URL
*   `options` Object (可选)
    *   `httpReferrer` String - A HTTP Referrer url.
    *   `userAgent` String - 产生请求的用户代理
    *   `extraHeaders` String - 以 "\n" 分隔的额外头

在窗口中加载 `url` , `url` 必须包含协议前缀, 比如 `http://` 或 `file://`. 如果加载想要忽略 http 缓存，可以使用 `pragma` 头来达到目的.

```
const options = {"extraHeaders" : "pragma: no-cache\n"}
webContents.loadURL(url, options) 
```

### `webContents.downloadURL(url)`

*   `url` URL

初始化一个指定 `url` 的资源下载，不导航跳转. `session` 的 `will-download` 事件会触发.

### `webContents.getURL()`

返回当前 page 的 url.

```
var win = new BrowserWindow({width: 800, height: 600});
win.loadURL("http://github.com");

var currentURL = win.webContents.getURL(); 
```

### `webContents.getTitle()`

返回当前 page 的 标题.

### `webContents.isLoading()`

返回一个布尔值，标识当前页是否正在加载.

### `webContents.isWaitingForResponse()`

返回一个布尔值，标识当前页是否正在等待主要资源的第一次响应.

### `webContents.stop()`

停止还为开始的导航.

### `webContents.reload()`

重载当前页.

### `webContents.reloadIgnoringCache()`

重载当前页，忽略缓存.

### `webContents.canGoBack()`

返回一个布尔值，标识浏览器是否能回到前一个 page.

### `webContents.canGoForward()`

返回一个布尔值，标识浏览器是否能前往下一个 page.

### `webContents.canGoToOffset(offset)`

*   `offset` Integer

返回一个布尔值，标识浏览器是否能前往指定 `offset` 的 page.

### `webContents.clearHistory()`

清除导航历史.

### `webContents.goBack()`

让浏览器回退到前一个 page.

### `webContents.goForward()`

让浏览器回前往下一个 page.

### `webContents.goToIndex(index)`

*   `index` Integer

让浏览器回前往指定 `index` 的 page.

### `webContents.goToOffset(offset)`

*   `offset` Integer

导航到相对于当前页的偏移位置页.

### `webContents.isCrashed()`

渲染进程是否崩溃.

### `webContents.setUserAgent(userAgent)`

*   `userAgent` String

重写本页用户代理.

### `webContents.getUserAgent()`

返回一个 `String` ，标识本页用户代理信息.

### `webContents.insertCSS(css)`

*   `css` String

为当前页插入 css.

### `webContents.executeJavaScript(code[, userGesture, callback])`

*   `code` String
*   `userGesture` Boolean (可选)
*   `callback` Function (可选) - 脚本执行完成后调用的回调函数.
    *   `result`

评估 page `代码`.

浏览器窗口中的一些 HTML API ，例如 `requestFullScreen`，只能被用户手势请求.设置 `userGesture` 为 `true` 可以取消这个限制.

### `webContents.setAudioMuted(muted)`

*   `muted` Boolean

减缓当前也的 audio 的播放速度.

### `webContents.isAudioMuted()`

返回一个布尔值，标识当前页是否减缓了 audio 的播放速度.

### `webContents.undo()`

执行网页的编辑命令 `undo` .

### `webContents.redo()`

执行网页的编辑命令 `redo` .

### `webContents.cut()`

执行网页的编辑命令 `cut` .

### `webContents.copy()`

执行网页的编辑命令 `copy` .

### `webContents.paste()`

执行网页的编辑命令 `paste` .

### `webContents.pasteAndMatchStyle()`

执行网页的编辑命令 `pasteAndMatchStyle` .

### `webContents.delete()`

执行网页的编辑命令 `delete` .

### `webContents.selectAll()`

执行网页的编辑命令 `selectAll` .

### `webContents.unselect()`

执行网页的编辑命令 `unselect` .

### `webContents.replace(text)`

*   `text` String

执行网页的编辑命令 `replace` .

### `webContents.replaceMisspelling(text)`

*   `text` String

执行网页的编辑命令 `replaceMisspelling` .

### `webContents.insertText(text)`

*   `text` String

插入 `text` 到获得了焦点的元素.

### `webContents.findInPage(text[, options])`

*   `text` String - 查找内容, 不能为空.
*   `options` Object (可选)
    *   `forward` Boolean - 是否向前或向后查找, 默认为 `true`.
    *   `findNext` Boolean - 当前操作是否是第一次查找或下一次查找, 默认为 `false`.
    *   `matchCase` Boolean - 查找是否区分大小写, 默认为 `false`.
    *   `wordStart` Boolean -是否仅以首字母查找. 默认为 `false`.
    *   `medialCapitalAsWordStart` Boolean - 是否结合 `wordStart`,如果匹配是大写字母开头，后面接小写字母或无字母，那么就接受这个词中匹配.接受几个其它的合成词匹配, 默认为 `false`.

发起请求，在网页中查找所有与 `text` 相匹配的项，并且返回一个 `Integer` 来表示这个请求用的请求 Id.这个请求结果可以通过订阅 `found-in-page` 事件来取得.

### `webContents.stopFindInPage(action)`

*   `action` String - 指定一个行为来接替停止 `webContents.findInPage` 请求.
    *   `clearSelection` - 转变为一个普通的 selection.
    *   `keepSelection` - 清除 selection.
    *   `activateSelection` - 获取焦点并点击 selection node.

使用给定的 `action` 来为 `webContents` 停止任何 `findInPage` 请求.

```
webContents.on('found-in-page', function(event, result) {
  if (result.finalUpdate)
    webContents.stopFindInPage("clearSelection");
});

const requestId = webContents.findInPage("api"); 
```

### `webContents.hasServiceWorker(callback)`

*   `callback` Function

检查是否有任何 ServiceWorker 注册了，并且返回一个布尔值，来作为 `callback`响应的标识.

### `webContents.unregisterServiceWorker(callback)`

*   `callback` Function

如果存在任何 ServiceWorker ，则全部注销，并且当 JS 承诺执行行或 JS 拒绝执行而失败的时候，返回一个布尔值，它标识了相应的 `callback`.

### `webContents.print([options])`

*   `options` Object (可选)
    *   `silent` Boolean - 不需要请求用户的打印设置. 默认为 `false`.
    *   `printBackground` Boolean - 打印背景和网页图片. 默认为 `false`.

打印窗口的网页. 当设置 `silent` 为 `false` 的时候，Electron 将使用系统默认的打印机和打印方式来打印.

在网页中调用 `window.print()` 和 调用 `webContents.print({silent: false, printBackground: false})`具有相同的作用.

**注意:** 在 Windows, 打印 API 依赖于 `pdf.dll`. 如果你的应用不使用任何的打印, 你可以安全删除 `pdf.dll` 来减少二进制文件的 size.

### `webContents.printToPDF(options, callback)`

*   `options` Object
    *   `marginsType` Integer - 指定使用的 margin type. 默认 margin 使用 0, 无 margin 使用 1, 最小化 margin 使用 2.
    *   `pageSize` String - 指定生成的 PDF 文件的 page size. 可以是 `A3`, `A4`, `A5`, `Legal`, `Letter` 和 `Tabloid`.
    *   `printBackground` Boolean - 是否打印 css 背景.
    *   `printSelectionOnly` Boolean - 是否只打印选中的部分.
    *   `landscape` Boolean - landscape 为 `true`, portrait 为 `false`.
*   `callback` Function

打印窗口的网页为 pdf ，使用 Chromium 预览打印的自定义设置.

完成时使用 `callback(error, data)` 调用 `callback` . `data` 是一个 `Buffer` ，包含了生成的 pdf 数据.

默认，空的 `options` 被视为 :

```
{
  marginsType: 0,
  printBackground: false,
  printSelectionOnly: false,
  landscape: false
} 
```

```
const BrowserWindow = require('electron').BrowserWindow;
const fs = require('fs');

var win = new BrowserWindow({width: 800, height: 600});
win.loadURL("http://github.com");

win.webContents.on("did-finish-load", function() {
  // Use default printing options
  win.webContents.printToPDF({}, function(error, data) {
    if (error) throw error;
    fs.writeFile("/tmp/print.pdf", data, function(error) {
      if (error)
        throw error;
      console.log("Write PDF successfully.");
    })
  })
}); 
```

### `webContents.addWorkSpace(path)`

*   `path` String

添加指定的路径给开发者工具栏的 workspace.必须在 DevTools 创建之后使用它 :

```
mainWindow.webContents.on('devtools-opened', function() {
  mainWindow.webContents.addWorkSpace(__dirname);
}); 
```

### `webContents.removeWorkSpace(path)`

*   `path` String

从开发者工具栏的 workspace 删除指定的路径.

### `webContents.openDevTools([options])`

*   `options` Object (可选)
    *   `detach` Boolean - 在一个新窗口打开开发者工具栏

打开开发者工具栏.

### `webContents.closeDevTools()`

关闭开发者工具栏.

### `webContents.isDevToolsOpened()`

返回布尔值，开发者工具栏是否打开.

### `webContents.isDevToolsFocused()`

返回布尔值，开发者工具栏视图是否获得焦点.

### `webContents.toggleDevTools()`

Toggles 开发者工具.

### `webContents.inspectElement(x, y)`

*   `x` Integer
*   `y` Integer

在 (`x`, `y`) 开始检测元素.

### `webContents.inspectServiceWorker()`

为 service worker 上下文打开开发者工具栏.

### `webContents.send(channel[, arg1][, arg2][, ...])`

*   `channel` String
*   `arg` (可选)

通过 `channel` 发送异步消息给渲染进程，你也可发送任意的参数.参数应该在 JSON 内部序列化，并且此后没有函数或原形链被包括了.

渲染进程可以通过使用 `ipcRenderer` 监听 `channel` 来处理消息.

例子，从主进程向渲染进程发送消息 :

```
// 主进程.
var window = null;
app.on('ready', function() {
  window = new BrowserWindow({width: 800, height: 600});
  window.loadURL('file://' + __dirname + '/index.html');
  window.webContents.on('did-finish-load', function() {
    window.webContents.send('ping', 'whoooooooh!');
  });
}); 
```

```
<!-- index.html -->
<html>
<body>
  <script> require('electron').ipcRenderer.on('ping', function(event, message) {
      console.log(message);  // Prints "whoooooooh!"
    }); </script>
</body>
</html> 
```

### `webContents.enableDeviceEmulation(parameters)`

`parameters` Object, properties:

*   `screenPosition` String - 指定需要模拟的屏幕 (默认 : `desktop`)
    *   `desktop`
    *   `mobile`
*   `screenSize` Object - 设置模拟屏幕 size (screenPosition == mobile)
    *   `width` Integer - 设置模拟屏幕 width
    *   `height` Integer - 设置模拟屏幕 height
*   `viewPosition` Object - 在屏幕放置 view (screenPosition == mobile) (默认: `{x: 0, y: 0}`)
    *   `x` Integer - 设置偏移左上角的 x 轴
    *   `y` Integer - 设置偏移左上角的 y 轴
*   `deviceScaleFactor` Integer - 设置设备比例因子 (如果为 0，默认为原始屏幕比例) (默认: `0`)
*   `viewSize` Object - 设置模拟视图 size (空表示不覆盖)
    *   `width` Integer - 设置模拟视图 width
    *   `height` Integer - 设置模拟视图 height
*   `fitToView` Boolean - 如果有必要的话，是否把模拟视图按比例缩放来适应可用空间 (默认: `false`)
*   `offset` Object - 可用空间内的模拟视图偏移 (不在适应模式) (默认: `{x: 0, y: 0}`)
    *   `x` Float - 设置相对左上角的 x 轴偏移值
    *   `y` Float - 设置相对左上角的 y 轴偏移值
*   `scale` Float - 可用空间内的模拟视图偏移 (不在适应视图模式) (默认: `1`)

使用给定的参数来开启设备模拟.

### `webContents.disableDeviceEmulation()`

使用 `webContents.enableDeviceEmulation` 关闭设备模拟.

### `webContents.sendInputEvent(event)`

*   `event` Object
    *   `type` String (**必需**) - 事件类型，可以是 `mouseDown`, `mouseUp`, `mouseEnter`, `mouseLeave`, `contextMenu`, `mouseWheel`, `mouseMove`, `keyDown`, `keyUp`, `char`.
    *   `modifiers` Array - 事件的 modifiers 数组, 可以是 include `shift`, `control`, `alt`, `meta`, `isKeypad`, `isAutoRepeat`, `leftButtonDown`, `middleButtonDown`, `rightButtonDown`, `capsLock`, `numLock`, `left`, `right`.

向 page 发送一个输入 `event` .

对键盘事件来说，`event` 对象还有如下属性 :

*   `keyCode` String (**必需**) - 特点是将作为键盘事件发送. 可用的 key codes Accelerator.

对鼠标事件来说，`event` 对象还有如下属性 :

*   `x` Integer (**required**)
*   `y` Integer (**required**)
*   `button` String - button 按下, 可以是 `left`, `middle`, `right`
*   `globalX` Integer
*   `globalY` Integer
*   `movementX` Integer
*   `movementY` Integer
*   `clickCount` Integer

对鼠标滚轮事件来说，`event` 对象还有如下属性 :

*   `deltaX` Integer
*   `deltaY` Integer
*   `wheelTicksX` Integer
*   `wheelTicksY` Integer
*   `accelerationRatioX` Integer
*   `accelerationRatioY` Integer
*   `hasPreciseScrollingDeltas` Boolean
*   `canScroll` Boolean

### `webContents.beginFrameSubscription(callback)`

*   `callback` Function

开始订阅 提交 事件和捕获数据帧，当有 提交 事件时，使用 `callback(frameBuffer)` 调用 `callback`.

`frameBuffer` 是一个包含原始像素数据的 `Buffer`,像素数据是按照 32bit BGRA 格式有效存储的，但是实际情况是取决于处理器的字节顺序的(大多数的处理器是存放小端序的，如果是在大端序的处理器上，数据是 32bit ARGB 格式).

### `webContents.endFrameSubscription()`

停止订阅帧提交事件.

### `webContents.savePage(fullPath, saveType, callback)`

*   `fullPath` String - 文件的完整路径.
*   `saveType` String - 指定保存类型.
    *   `HTMLOnly` - 只保存 html.
    *   `HTMLComplete` - 保存整个 page 内容.
    *   `MHTML` - 保存完整的 html 为 MHTML.
*   `callback` Function - `function(error) {}`.
    *   `error` Error

如果保存界面过程初始化成功，返回 true.

```
win.loadURL('https://github.com');

win.webContents.on('did-finish-load', function() {
  win.webContents.savePage('/tmp/test.html', 'HTMLComplete', function(error) {
    if (!error)
      console.log("Save page successfully");
  });
}); 
```

## 实例属性

`WebContents` 对象也有下列属性:

### `webContents.session`

返回这个 `webContents` 使用的 session 对象.

### `webContents.hostWebContents`

返回这个 `webContents` 的父 `webContents` .

### `webContents.devToolsWebContents`

获取这个 `WebContents` 的开发者工具栏的 `WebContents` .

**注意:** 用户不可保存这个对象，因为当开发者工具栏关闭的时候它的值为 `null` .

### `webContents.debugger`

调试 API 为 [remote debugging protocol](https://developer.chrome.com/devtools/docs/debugger-protocol) 提供交替传送.

```
try {
  win.webContents.debugger.attach("1.1");
} catch(err) {
  console.log("Debugger attach failed : ", err);
};

win.webContents.debugger.on('detach', function(event, reason) {
  console.log("Debugger detached due to : ", reason);
});

win.webContents.debugger.on('message', function(event, method, params) {
  if (method == "Network.requestWillBeSent") {
    if (params.request.url == "https://www.github.com")
      win.webContents.debugger.detach();
  }
})

win.webContents.debugger.sendCommand("Network.enable"); 
```

#### `webContents.debugger.attach([protocolVersion])`

*   `protocolVersion` String (可选) - 请求调试协议版本.

添加 `webContents` 调试.

#### `webContents.debugger.isAttached()`

返回一个布尔值，标识是否已经给 `webContents` 添加了调试.

#### `webContents.debugger.detach()`

删除 `webContents` 调试.

#### `webContents.debugger.sendCommand(method[, commandParams, callback])`

*   `method` String - 方法名, 应该是由远程调试协议定义的方法.
*   `commandParams` Object (可选) - 请求参数为 JSON 对象.
*   `callback` Function (可选) - Response
    *   `error` Object - 错误消息，标识命令失败.
    *   `result` Object - 回复在远程调试协议中由 'returns'属性定义的命令描述.

发送给定命令给调试目标.

#### Event: 'detach'

*   `event` Event
*   `reason` String - 拆分调试器原因.

在调试 session 结束时发出事件.这在 `webContents` 关闭时或 `webContents` 请求开发者工具栏时发生.

#### Event: 'message'

*   `event` Event
*   `method` String - 方法名.
*   `params` Object - 在远程调试协议中由 'parameters' 属性定义的事件参数.

每当调试目标发出事件时发出.

# Tray

用一个 `Tray` 来表示一个图标,这个图标处于正在运行的系统的通知区 ，通常被添加到一个 context menu 上.

```
const electron = require('electron');
const app = electron.app;
const Menu = electron.Menu;
const Tray = electron.Tray;

var appIcon = null;
app.on('ready', function(){
  appIcon = new Tray('/path/to/my/icon');
  var contextMenu = Menu.buildFromTemplate([
    { label: 'Item1', type: 'radio' },
    { label: 'Item2', type: 'radio' },
    { label: 'Item3', type: 'radio', checked: true },
    { label: 'Item4', type: 'radio' }
  ]);
  appIcon.setToolTip('This is my application.');
  appIcon.setContextMenu(contextMenu);
}); 
```

**平台限制:**

*   在 Linux， 如果支持应用指示器则使用它，否则使用 `GtkStatusIcon` 代替.
*   在 Linux ，配置了只有有了应用指示器的支持, 你必须安装 `libappindicator1` 来让 tray icon 执行.
*   应用指示器只有在它拥有 context menu 时才会显示.
*   当在 linux 上使用了应用指示器，将忽略点击事件.
*   在 Linux，为了让单独的 `MenuItem` 起效，需要再次调用 `setContextMenu` .例如:

```
contextMenu.items[2].checked = false;
appIcon.setContextMenu(contextMenu); 
```

如果想在所有平台保持完全相同的行为，不应该依赖点击事件，而是一直将一个 context menu 添加到 tray icon.

## Class: Tray

`Tray` 是一个 [事件发出者](http://nodejs.org/api/events.html#events_class_events_eventemitter).

### `new Tray(image)`

*   `image` NativeImage

创建一个与 `image` 相关的 icon.

## 事件

`Tray` 模块可发出下列事件:

**注意:** 一些事件只能在特定的 os 中运行，已经标明.

### Event: 'click'

*   `event` Event
    *   `altKey` Boolean
    *   `shiftKey` Boolean
    *   `ctrlKey` Boolean
    *   `metaKey` Boolean
*   `bounds` Object - tray icon 的 bounds.
    *   `x` Integer
    *   `y` Integer
    *   `width` Integer
    *   `height` Integer

当 tray icon 被点击的时候发出事件.

**注意:** `bounds` 只在 OS X 和 Windows 上起效.

### Event: 'right-click' *OS X* *Windows*

*   `event` Event
    *   `altKey` Boolean
    *   `shiftKey` Boolean
    *   `ctrlKey` Boolean
    *   `metaKey` Boolean
*   `bounds` Object - tray icon 的 bounds.
    *   `x` Integer
    *   `y` Integer
    *   `width` Integer
    *   `height` Integer

当 tray icon 被鼠标右键点击的时候发出事件.

### Event: 'double-click' *OS X* *Windows*

*   `event` Event
    *   `altKey` Boolean
    *   `shiftKey` Boolean
    *   `ctrlKey` Boolean
    *   `metaKey` Boolean
*   `bounds` Object - tray icon 的 bounds.
    *   `x` Integer
    *   `y` Integer
    *   `width` Integer
    *   `height` Integer

当 tray icon 被双击的时候发出事件.

### Event: 'balloon-show' *Windows*

当 tray 气泡显示的时候发出事件.

### Event: 'balloon-click' *Windows*

当 tray 气泡被点击的时候发出事件.

### Event: 'balloon-closed' *Windows*

当 tray 气泡关闭的时候发出事件，因为超时或人为关闭.

### Event: 'drop' *OS X*

当 tray icon 上的任何可拖动项被删除的时候发出事件.

### Event: 'drop-files' *OS X*

*   `event`
*   `files` Array - 已删除文件的路径.

当 tray icon 上的可拖动文件被删除的时候发出事件.

### Event: 'drag-enter' *OS X*

当一个拖动操作进入 tray icon 的时候发出事件.

### Event: 'drag-leave' *OS X*

当一个拖动操作离开 tray icon 的时候发出事件. Emitted when a drag operation exits the tray icon.

### Event: 'drag-end' *OS X*

当一个拖动操作在 tray icon 上或其它地方停止拖动的时候发出事件.

## 方法

`Tray` 模块有以下方法:

**Note:** 一些方法只能在特定的 os 中运行，已经标明.

### `Tray.destroy()`

立刻删除 tray icon.

### `Tray.setImage(image)`

*   `image` NativeImage

让 `image` 与 tray icon 关联起来.

### `Tray.setPressedImage(image)` *OS X*

*   `image` NativeImage

当在 OS X 上按压 tray icon 的时候， 让 `image` 与 tray icon 关联起来.

### `Tray.setToolTip(toolTip)`

*   `toolTip` String

为 tray icon 设置 hover text.

### `Tray.setTitle(title)` *OS X*

*   `title` String

在状态栏沿着 tray icon 设置标题.

### `Tray.setHighlightMode(highlight)` *OS X*

*   `highlight` Boolean

当 tray icon 被点击的时候，是否设置它的背景色变为高亮(blue).默认为 true.

### `Tray.displayBalloon(options)` *Windows*

*   `options` Object
    *   `icon` NativeImage
    *   `title` String
    *   `content` String

展示一个 tray balloon.

### `Tray.popUpContextMenu([menu, position])` *OS X* *Windows*

*   `menu` Menu (optional)
*   `position` Object (可选) - 上托位置.
    *   `x` Integer
    *   `y` Integer

从 tray icon 上托出 context menu . 当划过 `menu` 的时候， `menu` 显示，代替 tray 的 context menu .

`position` 只在 windows 上可用，默认为 (0, 0) .

### `Tray.setContextMenu(menu)`

*   `menu` Menu

为这个 icon 设置 context menu .

# 在渲染进程（网页）内可用的模块

# desktopCapturer

`desktopCapturer` 模块可用来获取可用资源，这个资源可通过 `getUserMedia` 捕获得到.

```
// 在渲染进程中.
var desktopCapturer = require('electron').desktopCapturer;

desktopCapturer.getSources({types: ['window', 'screen']}, function(error, sources) {
  if (error) throw error;
  for (var i = 0; i < sources.length; ++i) {
    if (sources[i].name == "Electron") {
      navigator.webkitGetUserMedia({
        audio: false,
        video: {
          mandatory: {
            chromeMediaSource: 'desktop',
            chromeMediaSourceId: sources[i].id,
            minWidth: 1280,
            maxWidth: 1280,
            minHeight: 720,
            maxHeight: 720
          }
        }
      }, gotStream, getUserMediaError);
      return;
    }
  }
});

function gotStream(stream) {
  document.querySelector('video').src = URL.createObjectURL(stream);
}

function getUserMediaError(e) {
  console.log('getUserMediaError');
} 
```

当调用 `navigator.webkitGetUserMedia` 时创建一个约束对象，如果使用 `desktopCapturer` 的资源，必须设置 `chromeMediaSource` 为 `"desktop"` ，并且 `audio` 为 `false`.

如果你想捕获整个桌面的 audio 和 video，你可以设置 `chromeMediaSource` 为 `"screen"` ，和 `audio` 为 `true`. 当使用这个方法的时候，不可以指定一个 `chromeMediaSourceId`.

## 方法

`desktopCapturer` 模块有如下方法:

### `desktopCapturer.getSources(options, callback)`

*   `options` Object
    *   `types` Array - 一个 String 数组，列出了可以捕获的桌面资源类型, 可用类型为 `screen` 和 `window`.
    *   `thumbnailSize` Object (可选) - 建议缩略可被缩放的 size, 默认为 `{width: 150, height: 150}`.
*   `callback` Function

发起一个请求，获取所有桌面资源，当请求完成的时候使用 `callback(error, sources)` 调用 `callback` .

`sources` 是一个 `Source` 对象数组, 每个 `Source` 表示了一个捕获的屏幕或单独窗口，并且有如下属性 :

*   `id` String - 在 `navigator.webkitGetUserMedia` 中使用的捕获窗口或屏幕的 id . 格式为 `window:XX` 祸 `screen:XX`，`XX` 是一个随机数.
*   `name` String - 捕获窗口或屏幕的描述名 . 如果资源为屏幕，名字为 `Entire Screen` 或 `Screen <index>`; 如果资源为窗口, 名字为窗口的标题.
*   `thumbnail` NativeImage - 缩略图.

**注意:** 不能保证 `source.thumbnail` 的 size 和 `options` 中的 `thumnbailSize` 一直一致. 它也取决于屏幕或窗口的缩放比例.

# ipcRenderer

`ipcRenderer` 模块是一个 [EventEmitter](https://nodejs.org/api/events.html) 类的实例. 它提供了有限的方法，你可以从渲染进程向主进程发送同步或异步消息. 也可以收到主进程的相应.

查看 ipcMain 代码例子.

## 消息监听

`ipcRenderer` 模块有下列方法来监听事件:

### `ipcRenderer.on(channel, listener)`

*   `channel` String
*   `listener` Function

监听 `channel`, 当有新消息到达，使用 `listener(event, args...)` 调用 `listener` .

### `ipcRenderer.once(channel, listener)`

*   `channel` String
*   `listener` Function

为这个事件添加一个一次性 `listener` 函数.这个 `listener` 将在下一次有新消息被发送到 `channel` 的时候被请求调用，之后就被删除了.

### `ipcRenderer.removeListener(channel, listener)`

*   `channel` String
*   `listener` Function

从指定的 `channel` 中的监听者数组删除指定的 `listener` .

### `ipcRenderer.removeAllListeners([channel])`

*   `channel` String (optional)

删除所有的监听者，或者删除指定 `channel` 中的全部.

## 发送消息

`ipcRenderer` 模块有如下方法来发送消息:

### `ipcRenderer.send(channel[, arg1][, arg2][, ...])`

*   `channel` String
*   `arg` (可选)

通过 `channel` 向主进程发送异步消息，也可以发送任意参数.参数会被 JSON 序列化，之后就不会包含函数或原型链.

主进程通过使用 `ipcMain` 模块来监听 `channel`，从而处理消息.

### `ipcRenderer.sendSync(channel[, arg1][, arg2][, ...])`

*   `channel` String
*   `arg` (可选)

通过 `channel` 向主进程发送同步消息，也可以发送任意参数.参数会被 JSON 序列化，之后就不会包含函数或原型链.

主进程通过使用 `ipcMain` 模块来监听 `channel`，从而处理消息, 通过 `event.returnValue` 来响应.

**注意:** 发送同步消息将会阻塞整个渲染进程,除非你知道你在做什么，否则就永远不要用它 .

### `ipcRenderer.sendToHost(channel[, arg1][, arg2][, ...])`

*   `channel` String
*   `arg` (可选)

类似 `ipcRenderer.send` ，但是它的事件将发往 host page 的 `<webview>` 元素，而不是主进程.

# remote

`remote` 模块提供了一种在渲染进程（网页）和主进程之间进行进程间通讯（IPC）的简便途径。

Electron 中, 与 GUI 相关的模块（如 `dialog`, `menu` 等)只存在于主进程，而不在渲染进程中 。为了能从渲染进程中使用它们，需要用`ipc`模块来给主进程发送进程间消息。使用 `remote` 模块，可以调用主进程对象的方法，而无需显式地发送进程间消息，这类似于 Java 的 [RMI](http://en.wikipedia.org/wiki/Java_remote_method_invocation)。 下面是从渲染进程创建一个浏览器窗口的例子：

```
const remote = require('electron').remote;
const BrowserWindow = remote.BrowserWindow;

var win = new BrowserWindow({ width: 800, height: 600 });
win.loadURL('https://github.com'); 
```

**注意:** 反向操作（从主进程访问渲染进程），可以使用 webContents.executeJavascript.

## 远程对象

`remote`模块返回的每个对象（包括函数）都代表了主进程中的一个对象（我们称之为远程对象或者远程函数）。 当调用远程对象的方法、执行远程函数或者使用远程构造器（函数）创建新对象时，其实就是在发送同步的进程间消息。

在上面的例子中， `BrowserWindow` 和 `win` 都是远程对象，然而 `new BrowserWindow` 并没有在渲染进程中创建 `BrowserWindow` 对象。 而是在主进程中创建了 `BrowserWindow` 对象，并在渲染进程中返回了对应的远程对象，即 `win` 对象。

请注意只有 [可枚举属性](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties) 才能通过 remote 进行访问.

## 远程对象的生命周期

Electron 确保在渲染进程中的远程对象存在（换句话说，没有被垃圾收集），那主进程中的对应对象也不会被释放。 当远程对象被垃圾收集之后，主进程中的对应对象才会被取消关联。

如果远程对象在渲染进程泄露了（即，存在某个表中但永远不会释放），那么主进程中的对应对象也一样会泄露， 所以你必须小心不要泄露了远程对象。If the remote object is leaked in the renderer process (e.g. stored in a map but never freed), the corresponding object in the main process will also be leaked, so you should be very careful not to leak remote objects.

不过，主要的值类型如字符串和数字，是传递的副本。

## 给主进程传递回调函数

在主进程中的代码可以从渲染进程——`remote`模块——中接受回调函数，但是使用这个功能的时候必须非常非常小心。Code in the main process can accept callbacks from the renderer - for instance the `remote` module - but you should be extremely careful when using this feature.

首先，为了避免死锁，传递给主进程的回调函数会进行异步调用。所以不能期望主进程来获得传递过去的回调函数的返回值。First, in order to avoid deadlocks, the callbacks passed to the main process are called asynchronously. You should not expect the main process to get the return value of the passed callbacks.

比如，你不能主进程中给`Array.map`传递来自渲染进程的函数。

```
// 主进程 mapNumbers.js
exports.withRendererCallback = function(mapper) {
  return [1,2,3].map(mapper);
}

exports.withLocalCallback = function() {
  return exports.mapNumbers(function(x) {
    return x + 1;
  });
} 
```

```
// 渲染进程
var mapNumbers = require("remote").require("./mapNumbers");

var withRendererCb = mapNumbers.withRendererCallback(function(x) {
  return x + 1;
})

var withLocalCb = mapNumbers.withLocalCallback()

console.log(withRendererCb, withLocalCb) // [true, true, true], [2, 3, 4] 
```

如你所见，渲染器回调函数的同步返回值没有按预期产生，与主进程中的一模一样的回调函数的返回值不同。

其次，传递给主进程的函数会持续到主进程对他们进行垃圾回收。

例如，下面的代码第一眼看上去毫无问题。给远程对象的`close`事件绑定了一个回调函数：

```
remote.getCurrentWindow().on('close', function() {
  // blabla...
}); 
```

但记住主进程会一直保持对这个回调函数的引用，除非明确的卸载它。如果不卸载，每次重新载入窗口都会再次绑定，这样每次重启就会泄露一个回调函数。

更严重的是，由于前面安装了回调函数的上下文已经被释放，所以当主进程的 `close` 事件触发的时候，会抛出异常。

为了避免这个问题，要确保对传递给主进程的渲染器的回调函数进行清理。可以清理事件处理器，或者明确告诉主进行取消来自已经退出的渲染器进程中的回调函数。

## 访问主进程中的内置模块

在主进程中的内置模块已经被添加为`remote`模块中的属性，所以可以直接像使用`electron`模块一样直接使用它们。

```
const app = remote.app; 
```

## 方法

`remote` 模块有以下方法：

### `remote.require(module)`

*   `module` String

返回在主进程中执行 `require(module)` 所返回的对象。

### `remote.getCurrentWindow()`

返回该网页所属的 `BrowserWindow` 对象。

### `remote.getCurrentWebContents()`

返回该网页的 `WebContents` 对象

### `remote.getGlobal(name)`

*   `name` String

返回在主进程中名为 `name` 的全局变量(即 `global[name]`) 。

### `remote.process`

返回主进程中的 `process` 对象。等同于 `remote.getGlobal('process')` 但是有缓存。

# webFrame

`web-frame` 模块允许你自定义如何渲染当前网页 .

例子，放大当前页到 200%.

```
var webFrame = require('electron').webFrame;

webFrame.setZoomFactor(2); 
```

## 方法

`web-frame` 模块有如下方法:

### `webFrame.setZoomFactor(factor)`

*   `factor` Number - 缩放参数.

将缩放参数修改为指定的参数值.缩放参数是百分制的，所以 300% = 3.0.

### `webFrame.getZoomFactor()`

返回当前缩放参数值.

### `webFrame.setZoomLevel(level)`

*   `level` Number - 缩放水平

将缩放水平修改为指定的水平值. 原始 size 为 0 ，并且每次增长都表示放大 20% 或缩小 20%，默认限制为原始 size 的 300% 到 50% 之间 .

### `webFrame.getZoomLevel()`

返回当前缩放水平值.

### `webFrame.setZoomLevelLimits(minimumLevel, maximumLevel)`

*   `minimumLevel` Number
*   `maximumLevel` Number

设置缩放水平的最大值和最小值.

### `webFrame.setSpellCheckProvider(language, autoCorrectWord, provider)`

*   `language` String
*   `autoCorrectWord` Boolean
*   `provider` Object

为输入框或文本域设置一个拼写检查 provider .

`provider` 必须是一个对象，它有一个 `spellCheck` 方法，这个方法返回扫过的单词是否拼写正确 .

例子，使用 [node-spellchecker](https://github.com/atom/node-spellchecker) 作为一个 provider:

```
webFrame.setSpellCheckProvider("en-US", true, {
  spellCheck: function(text) {
    return !(require('spellchecker').isMisspelled(text));
  }
}); 
```

### `webFrame.registerURLSchemeAsSecure(scheme)`

*   `scheme` String

注册 `scheme` 为一个安全的 scheme.

安全的 schemes 不会引发混合内容 warnings.例如, `https` 和 `data` 是安全的 schemes ，因为它们不能被活跃网络攻击而失效.

### `webFrame.registerURLSchemeAsBypassingCSP(scheme)`

*   `scheme` String

忽略当前网页内容的安全策略，直接从 `scheme` 加载.

### `webFrame.registerURLSchemeAsPrivileged(scheme)`

*   `scheme` String

通过资源的内容安全策略，注册 `scheme` 为安全的 scheme，允许注册 ServiceWorker 并且支持 fetch API.

### `webFrame.insertText(text)`

*   `text` String

向获得焦点的原色插入内容 .

### `webFrame.executeJavaScript(code[, userGesture])`

*   `code` String
*   `userGesture` Boolean (可选) - 默认为 `false`.

评估页面代码 .

在浏览器窗口中，一些 HTML APIs ，例如 `requestFullScreen`，只可以通过用户手势来使用.设置`userGesture` 为 `true` 可以突破这个限制 .

# 在两种进程中都可用的模块

# clipboard

`clipboard` 模块提供方法来供复制和粘贴操作 . 下面例子展示了如何将一个字符串写道 clipboard 上:

```
const clipboard = require('electron').clipboard;
clipboard.writeText('Example String'); 
```

在 X Window 系统上, 有一个可选的 clipboard. 你可以为每个方法使用 `selection` 来控制它:

```
clipboard.writeText('Example String', 'selection');
console.log(clipboard.readText('selection')); 
```

## 方法

`clipboard` 模块有以下方法:

**注意:** 测试 APIs 已经标明，并且在将来会被删除 .

### `clipboard.readText([type])`

*   `type` String (可选)

以纯文本形式从 clipboard 返回内容 .

### `clipboard.writeText(text[, type])`

*   `text` String
*   `type` String (可选)

以纯文本形式向 clipboard 添加内容 .

### `clipboard.readHtml([type])`

*   `type` String (可选)

返回 clipboard 中的标记内容.

### `clipboard.writeHtml(markup[, type])`

*   `markup` String
*   `type` String (可选)

向 clipboard 添加 `markup` 内容 .

### `clipboard.readImage([type])`

*   `type` String (可选)

从 clipboard 中返回 NativeImage 内容.

### `clipboard.writeImage(image[, type])`

*   `image` NativeImage
*   `type` String (可选)

向 clipboard 中写入 `image` .

### `clipboard.readRtf([type])`

*   `type` String (可选)

从 clipboard 中返回 RTF 内容.

### `clipboard.writeRtf(text[, type])`

*   `text` String
*   `type` String (可选)

向 clipboard 中写入 RTF 格式的 `text` .

### `clipboard.clear([type])`

*   `type` String (可选)

清空 clipboard 内容.

### `clipboard.availableFormats([type])`

*   `type` String (可选)

返回 clipboard 支持的格式数组 .

### `clipboard.has(data[, type])` *Experimental*

*   `data` String
*   `type` String (可选)

返回 clipboard 是否支持指定 `data` 的格式.

```
console.log(clipboard.has('<p>selection</p>')); 
```

### `clipboard.read(data[, type])` *Experimental*

*   `data` String
*   `type` String (可选)

读取 clipboard 的 `data`.

### `clipboard.write(data[, type])`

*   `data` Object
    *   `text` String
    *   `html` String
    *   `image` NativeImage
*   `type` String (可选)

```
clipboard.write({text: 'test', html: "<b>test</b>"}); 
```

向 clipboard 写入 `data` .

# crashReporter

`crash-reporter` 模块开启发送应用崩溃报告.

下面是一个自动提交崩溃报告给服务器的例子 :

```
const crashReporter = require('electron').crashReporter;

crashReporter.start({
  productName: 'YourName',
  companyName: 'YourCompany',
  submitURL: 'https://your-domain.com/url-to-submit',
  autoSubmit: true
}); 
```

可以使用下面的项目来创建一个服务器，用来接收和处理崩溃报告 :

*   [socorro](https://github.com/mozilla/socorro)
*   [mini-breakpad-server](https://github.com/atom/mini-breakpad-server)

## 方法

`crash-reporter` 模块有如下方法:

### `crashReporter.start(options)`

*   `options` Object
    *   `companyName` String
    *   `submitURL` String - 崩溃报告发送的路径，以 post 方式.
    *   `productName` String (可选) - 默认为 `Electron`.
    *   `autoSubmit` Boolean - 是否自动提交. 默认为 `true`.
    *   `ignoreSystemCrashHandler` Boolean - 默认为 `false`.
    *   `extra` Object - 一个你可以定义的对象，附带在崩溃报告上一起发送 . 只有字符串属性可以被正确发送，不支持嵌套对象.

只可以在使用其它 `crashReporter` APIs 之前使用这个方法.

**注意:** 在 OS X, Electron 使用一个新的 `crashpad` 客户端, 与 Windows 和 Linux 的 `breakpad` 不同. 为了开启崩溃点搜集，你需要在主进程和其它每个你需要搜集崩溃报告的渲染进程中调用 `crashReporter.start` API 来初始化 `crashpad`.

### `crashReporter.getLastCrashReport()`

返回最后一个崩溃报告的日期和 ID.如果没有过崩溃报告发送过来，或者还没有开始崩溃报告搜集，将返回 `null` .

### `crashReporter.getUploadedReports()`

返回所有上载的崩溃报告，每个报告包含了上载日期和 ID.

## crash-reporter Payload

崩溃报告将发送下面 `multipart/form-data` `POST` 型的数据给 `submitURL` :

*   `ver` String - Electron 版本.
*   `platform` String - 例如 'win32'.
*   `process_type` String - 例如 'renderer'.
*   `guid` String - 例如 '5e1286fc-da97-479e-918b-6bfb0c3d1c72'
*   `_version` String - `package.json` 版本.
*   `_productName` String - `crashReporter` `options` 对象中的产品名字.
*   `prod` String - 基础产品名字. 这种情况为 Electron.
*   `_companyName` String - `crashReporter` `options` 对象中的公司名字.
*   `upload_file_minidump` File - 崩溃报告按照 `minidump` 的格式.
*   `crashReporter` 中的 `extra` 对象的所有等级和一个属性. `options` object

# nativeImage

在 Electron 中, 对所有创建 images 的 api 来说, 你可以使用文件路径或 `nativeImage` 实例. 如果使用 `null` ，将创建一个空的 image 对象.

例如, 当创建一个 tray 或设置窗口的图标时候，你可以使用一个字符串的图片路径 :

```
var appIcon = new Tray('/Users/somebody/images/icon.png');
var window = new BrowserWindow({icon: '/Users/somebody/images/window.png'}); 
```

或者从剪切板中读取图片，它返回的是 `nativeImage`:

```
var image = clipboard.readImage();
var appIcon = new Tray(image); 
```

## 支持的格式

当前支持 `PNG` 和 `JPEG` 图片格式. 推荐 `PNG` ，因为它支持透明和无损压缩.

在 Windows, 你也可以使用 `ICO` 图标的格式.

## 高分辨率图片

如果平台支持 high-DPI，你可以在图片基础路径后面添加 `@2x` ，可以标识它为高分辨率的图片.

例如，如果 `icon.png` 是一个普通图片并且拥有标准分辨率，然后 `icon@2x.png`将被当作高分辨率的图片处理，它将拥有双倍 DPI 密度.

如果想同时支持展示不同分辨率的图片，你可以将拥有不同 size 的图片放在同一个文件夹下，不用 DPI 后缀.例如 :

```
images/
├── icon.png
├── icon@2x.png
└── icon@3x.png 
```

```
var appIcon = new Tray('/Users/somebody/images/icon.png'); 
```

也支持下面这些 DPI 后缀:

*   `@1x`
*   `@1.25x`
*   `@1.33x`
*   `@1.4x`
*   `@1.5x`
*   `@1.8x`
*   `@2x`
*   `@2.5x`
*   `@3x`
*   `@4x`
*   `@5x`

## 模板图片

模板图片由黑色和清色(和一个 alpha 通道)组成. 模板图片不是单独使用的，而是通常和其它内容混合起来创建期望的最终效果.

最常见的用力是将模板图片用到菜单栏图片上，所以它可以同时适应亮、黑不同的菜单栏.

**注意:** 模板图片只在 OS X 上可用.

为了将图片标识为一个模板图片，它的文件名应当以 `Template` 结尾. 例如:

*   `xxxTemplate.png`
*   `xxxTemplate@2x.png`

## 方法

`nativeImage` 类有如下方法:

### `nativeImage.createEmpty()`

创建一个空的 `nativeImage` 实例.

### `nativeImage.createFromPath(path)`

*   `path` String

从指定 `path` 创建一个新的 `nativeImage` 实例 .

### `nativeImage.createFromBuffer(buffer[, scaleFactor])`

*   `buffer` [Buffer](https://nodejs.org/api/buffer.html#buffer_class_buffer)
*   `scaleFactor` Double (可选)

从 `buffer` 创建一个新的 `nativeImage` 实例 .默认 `scaleFactor` 是 1.0.

### `nativeImage.createFromDataURL(dataURL)`

*   `dataURL` String

从 `dataURL` 创建一个新的 `nativeImage` 实例 .

## 实例方法

`nativeImage` 有如下方法:

```
const nativeImage = require('electron').nativeImage;

var image = nativeImage.createFromPath('/Users/somebody/images/icon.png'); 
```

### `image.toPng()`

返回一个 [Buffer](https://nodejs.org/api/buffer.html#buffer_class_buffer) ，它包含了图片的 `PNG` 编码数据.

### `image.toJpeg(quality)`

*   `quality` Integer (**必须**) - 在 0 - 100 之间.

返回一个 [Buffer](https://nodejs.org/api/buffer.html#buffer_class_buffer) ，它包含了图片的 `JPEG` 编码数据.

### `image.toDataURL()`

返回图片数据的 URL.

### `image.getNativeHandle()` *OS X*

返回一个保存了 c 指针的 [Buffer](https://nodejs.org/api/buffer.html#buffer_class_buffer) 来潜在处理原始图像.在 OS X, 将会返回一个 `NSImage` 指针实例.

注意那返回的指针是潜在原始图像的弱指针，而不是一个复制，你*必须* 确保与 `nativeImage` 的关联不间断 .

### `image.isEmpty()`

返回一个 boolean ，标识图片是否为空.

### `image.getSize()`

返回图片的 size.

### `image.setTemplateImage(option)`

*   `option` Boolean

将图片标识为模板图片.

### `image.isTemplateImage()`

返回一个 boolean ，标识图片是否是模板图片.

# screen

`screen` 模块检索屏幕的 size，显示，鼠标位置等的信息.在 `app` 模块的`ready` 事件触发之前不可使用这个模块.

`screen` 是一个 [EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter).

**注意:** 在渲染进程 / 开发者工具栏, `window.screen` 是一个预设值的 DOM 属性, 所以这样写 `var screen = require('electron').screen` 将不会工作. 在我们下面的例子, 我们取代使用可变名字的 `electronScreen`. 一个例子，创建一个充满真个屏幕的窗口 :

```
const electron = require('electron');
const app = electron.app;
const BrowserWindow = electron.BrowserWindow;

var mainWindow;

app.on('ready', function() {
  var electronScreen = electron.screen;
  var size = electronScreen.getPrimaryDisplay().workAreaSize;
  mainWindow = new BrowserWindow({ width: size.width, height: size.height });
}); 
```

另一个例子，在次页外创建一个窗口:

```
const electron = require('electron');
const app = electron.app;
const BrowserWindow = electron.BrowserWindow;

var mainWindow;

app.on('ready', function() {
  var electronScreen = electron.screen;
  var displays = electronScreen.getAllDisplays();
  var externalDisplay = null;
  for (var i in displays) {
    if (displays[i].bounds.x != 0 || displays[i].bounds.y != 0) {
      externalDisplay = displays[i];
      break;
    }
  }

  if (externalDisplay) {
    mainWindow = new BrowserWindow({
      x: externalDisplay.bounds.x + 50,
      y: externalDisplay.bounds.y + 50
    });
  }
}); 
```

## `Display` 对象

`Display` 对象表示了物力方式连接系统. 一个伪造的 `Display` 或许存在于一个无头系统中，或者一个 `Display` 相当于一个远程的、虚拟的 display.

*   `display` object
    *   `id` Integer - 与 display 相关的唯一性标志.
    *   `rotation` Integer - 可以是 0, 1, 2, 3, 每个代表了屏幕旋转的度数 0, 90, 180, 270.
    *   `scaleFactor` Number - Output device's pixel scale factor.
    *   `touchSupport` String - 可以是 `available`, `unavailable`, `unknown`.
    *   `bounds` Object
    *   `size` Object
    *   `workArea` Object
    *   `workAreaSize` Object

## 事件

`screen` 模块有如下事件:

### Event: 'display-added'

返回:

*   `event` Event
*   `newDisplay` Object

当添加了 `newDisplay` 时发出事件

### Event: 'display-removed'

返回:

*   `event` Event
*   `oldDisplay` Object

当移出了 `oldDisplay` 时发出事件

### Event: 'display-metrics-changed'

返回:

*   `event` Event
*   `display` Object
*   `changedMetrics` Array

当一个 `display` 中的一个或更多的 metrics 改变时发出事件. `changedMetrics` 是一个用来描述这个改变的数组.可能的变化为 `bounds`, `workArea`, `scaleFactor` 和 `rotation`.

## 方法

`screen` 模块有如下方法:

### `screen.getCursorScreenPoint()`

返回当前鼠标的绝对路径 .

### `screen.getPrimaryDisplay()`

返回最主要的 display.

### `screen.getAllDisplays()`

返回一个当前可用的 display 数组.

### `screen.getDisplayNearestPoint(point)`

*   `point` Object
    *   `x` Integer
    *   `y` Integer

返回离指定点最近的 display.

### `screen.getDisplayMatching(rect)`

*   `rect` Object
    *   `x` Integer
    *   `y` Integer
    *   `width` Integer
    *   `height` Integer

返回与提供的边界范围最密切相关的 display.

# shell

`shell` 模块提供了集成其他桌面客户端的关联功能.

在用户默认浏览器中打开 URL 的示例:

```
var shell = require('shell');

shell.openExternal('https://github.com'); 
```

## Methods

`shell` 模块包含以下函数:

### `shell.showItemInFolder(fullPath)`

*   `fullPath` String

打开文件所在文件夹,一般情况下还会选中它.

### `shell.openItem(fullPath)`

*   `fullPath` String

以默认打开方式打开文件.

### `shell.openExternal(url)`

*   `url` String

以系统默认设置打开外部协议.(例如,mailto: somebody@somewhere.io 会打开用户默认的邮件客户端)

### `shell.moveItemToTrash(fullPath)`

*   `fullPath` String

删除指定路径文件,并返回此操作的状态值(boolean 类型).

### `shell.beep()`

播放 beep 声音.