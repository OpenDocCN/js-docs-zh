# Backbone.Events（事件）

## Backbone.Events（事件）

**Events** 是一个可以融合到任何对象的模块, 给予 对象绑定和触发自定义事件的能力. Events 在绑定之前 不需要声明, 并且还可以传递参数. 比如:

```
var object = {};

_.extend(object, Backbone.Events);

object.on("alert", function(msg) {
  alert("Triggered " + msg);
});

object.trigger("alert", "an event"); 
```

举个例子, 你可以定义一个事件调度程序，然后在你应用的不同地方调用，例如： `var dispatcher = _.clone(Backbone.Events)`

**on**`object.on(event, callback, [context])`别名: bind 在 object 上绑定一个**callback**回调函数。 只要**event**触发，该回调函数就会调用。如果你的一个页面含有大量的不同时间，我们约定使用冒号来为事件添加 命名空间 俗成地使用冒号来命名：`"poll:start"`, 或 `"change:selection"`。 事件字符串也可能是用空格分隔的多个事件列表（愚人码头注：即可以同时绑定多个事件，事件用空格分隔）...

```
book.on("change:title change:author", ...); 
```

当回调函数被调用时，通过可选的第三个参数可以为`this`提供一个**context（上下文）**值：`model.on('change', this.render, this)` （愚人码头注：即回调函数中的 This，指向传递的第三个参数）。

当回调函数被绑定到特殊"all"事件时，任何事件的发生都会触发该回调函数，回调函数的第一个参数会传递该事件的名称。举个例子，将一个对象的所有事件代理到另一对象：

```
proxy.on("all", function(eventName) {
  object.trigger(eventName);
}); 
```

所有 Backbone 事件方法还支持事件映射的语法， 作为可惜的位置参数：

```
book.on({
  "change:title": titleView.update,
  "change:author": authorPane.update,
  "destroy": bookView.remove
}); 
```

**off**`object.off([event], [callback], [context])`别名: unbi nd 从 object 对象移除先前绑定的 **callback** 函数。如果没有指定**context（上下文）**，所有上下文下的这个回调函数将被移除。如果没有指定 callback，所有绑定这个事件回调函数将被移除；如果没有指定 event，所有事件的回调函数会被移除。

```
// Removes just the `onChange` callback.
object.off("change", onChange);

// Removes all "change" callbacks.
object.off("change");

// Removes the `onChange` callback for all events.
object.off(null, onChange);

// Removes all callbacks for `context` for all events.
object.off(null, null, context);

// Removes all callbacks on `object`.
object.off(); 
```

需要注意的是，调用 `model.off()`，例如，这确实会删除 model（模型）上*所有*的事件—包括 Backbone 内部用来统计的事件。

**trigger**`object.trigger(event, [*args])` 触发给定 **event**或用空格隔开的事件的回调函数。后续传入 **trigger** 的参数会传递到触发事件的回调函数里。

**once**`object.once(event, callback, [context])` 用法跟 on 很像，区别在于绑定的回调函数触发一次后就会被移除（愚人码头注：只执行一次）。简单的说就是“下次不在触发了，用这个方法”。

**listenTo**`object.listenTo(other, event, callback)` 让 **object** 监听 **另一个（other）**对象上的一个特定事件。不使用`other.on(event, callback, object)`，而使用这种形式的优点是：**listenTo**允许 **object**来跟踪这个特定事件，并且以后可以一次性全部移除它们。**callback**总是在**object**上下文环境中被调用。

```
view.listenTo(model, 'change', view.render); 
```

**stopListening**`object.stopListening([other], [event], [callback])` 让 **object** 停止监听事件。如果调用不带参数的**stopListening**，可以移除 **object** 下所有已经 registered(注册)的 callback 函数...，或者只删除指定对象上明确告知的监听事件，或者一个删除指定事件，或者只删除指定的回调函数。

```
view.stopListening();

view.stopListening(model); 
```

**listenToOnce**`object.listenToOnce(other, event, callback)` 用法跟 listenTo 很像，但是事件触发一次后 callback 将被移除。

**Catalog of Events（事件目录）** 下面是 Backbone 内置事件的完整列表，带有参数。 你也可以在 Models（模型），Collection（集合），Views（视图）上自由地触发这些事件，只要你认为合适。 收藏和意见，你认为合适。 `Backbone` 对象本身混入了`Events`，并且可用于触发任何全局事件，只要您的应用程序的需要。

*   **"add"** (model, collection, options) — 当一个 model（模型）被添加到一个 collection（集合）时触发。
*   **"remove"** (model, collection, options) — 当一个 model（模型）从一个 collection（集合）中被删除时触发。
*   **"reset"** (collection, options) — 当该 collection（集合）的全部内容已被替换时触发。
*   **"sort"** (collection, options) — 当该 collection（集合）已被重新排序时触发。
*   **"change"** (model, options) — 当一个 model（模型）的属性改变时触发。
*   **"change:[attribute]"** (model, value, options) — 当一个 model（模型）的某个特定属性被更新时触发。
*   **"destroy"** (model, collection, options) —当一个 model（模型）被 destroyed（销毁）时触发。
*   **"request"** (model_or_collection, xhr, options) — 当一个 model（模型）或 collection（集合）开始发送请求到服务器时触发。
*   **"sync"** (model_or_collection, resp, options) — 当一个 model（模型）或 collection（集合）成功同步到服务器时触发。
*   **"error"** (model_or_collection, resp, options) — 当一个 model（模型）或 collection（集合）的请求远程服务器失败时触发。
*   **"invalid"** (model, error, options) — 当 model（模型）在客户端 validation（验证）失败时触发。
*   **"route:[name]"** (params) — 当一个特定 route（路由）相匹配时通过路由器触发。
*   **"route"** (route, params) — 当 _ 任何一个 _route（路由）相匹配时通过路由器触发。
*   **"route"** (router, route, params) — 当 _ 任何一个 _route（路由）相匹配时通过 history（历史记录）触发。
*   **"all"** — 所有事件发生都能触发这个特别的事件，第一个参数是触发事件的名称。

一般来说，事件触发（例如 model.set，collection.add 或者其他事件）后就会执行回调函数，但是如果你想阻止回调函数的执行，你可以传递{silent: true}作为参数。很多时候，这是一个好的方法。通过在回调函数里传输一个特定的判断参数，会让你的程序更加出色。 一般而言，事件触发（`model.set`, `collection.add`,等等...）后就会调用一个函数，但是如果你想阻止事件被触发， 您可以传递`{silent: true}`作为一个选项。注意，这中情况很少， 甚至从来没有， 一个好主意。 通过在选项中传递一个特定的标记，回调函数里传输一个特定的判断参数 并且选择忽略，会让你的程序更加出色。