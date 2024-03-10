# Zepto 模块

| module | default | description |
| --- | --- | --- |
| [zepto](https://github.com/madrobby/zepto/blob/master/src/zepto.js#files) | yes | 核心模块；包含许多方法 |
| [event](https://github.com/madrobby/zepto/blob/master/src/event.js#files) | yes | 通过`on()`& `off()`处理事件 |
| [ajax](https://github.com/madrobby/zepto/blob/master/src/ajax.js#files) | yes | XMLHttpRequest 和 JSONP 实用功能 |
| [form](https://github.com/madrobby/zepto/blob/master/src/form.js#files) | yes | 序列化 & 提交 web 表单 |
| [ie](https://github.com/madrobby/zepto/blob/master/src/ie.js#files) | yes | 增加支持桌面的 Internet Explorer 10+和 Windows Phone 8。 |
| [detect](https://github.com/madrobby/zepto/blob/master/src/detect.js#files) |  | 提供 `$.os`和 `$.browser`消息 |
| [fx](https://github.com/madrobby/zepto/blob/master/src/fx.js#files) |  | The `animate()`方法 |
| [fx_methods](https://github.com/madrobby/zepto/blob/master/src/fx_methods.js#files) |  | 以动画形式的 `show`, `hide`, `toggle`, 和 `fade*()`方法. |
| [assets](https://github.com/madrobby/zepto/blob/master/src/assets.js#files) |  | 实验性支持从 DOM 中移除 image 元素后清理 iOS 的内存。 |
| [data](https://github.com/madrobby/zepto/blob/master/src/data.js#files) |  | 一个全面的 `data()`方法, 能够在内存中存储任意对象。 |
| [deferred](https://github.com/madrobby/zepto/blob/master/src/deferred.js#files) |  | 提供 `$.Deferred`promises API. 依赖"callbacks" 模块. 当包含这个模块时候, `$.ajax()` 支持 promise 接口链式的回调。 |
| [callbacks](https://github.com/madrobby/zepto/blob/master/src/callbacks.js#files) |  | 为"deferred"模块提供 `$.Callbacks`。 |
| [selector](https://github.com/madrobby/zepto/blob/master/src/selector.js#files) |  | 实验性的支持 [jQuery CSS 表达式](http://api.jquery.com/category/selectors/jquery-selector-extensions/) 实用功能，比如 `$('div:first')`和 `el.is(':visible')`。 |
| [touch](https://github.com/madrobby/zepto/blob/master/src/touch.js#files) |  | 在触摸设备上触发 tap– 和 swipe– 相关事件。这适用于所有的`touch`(iOS, Android)和`pointer`事件(Windows Phone)。 |
| [gesture](https://github.com/madrobby/zepto/blob/master/src/gesture.js#files) |  | 在触摸设备上触发 pinch 手势事件。 |
| [stack](https://github.com/madrobby/zepto/blob/master/src/stack.js#files) |  | 提供 `andSelf`& `end()`链式调用方法 |
| [ios3](https://github.com/madrobby/zepto/blob/master/src/ios3.js#files) |  | String.prototype.trim 和 Array.prototype.reduce 方法 (如果他们不存在) ，以兼容 iOS 3.x. |