# Backbone.Router（路由）

## Backbone.Router（路由）

web 应用程序通常需要为应用的重要位置提供可链接，可收藏，可分享的 URLs。 直到最近， 猫点（hash）片段（`#page`）可以被用来提供这种链接， 同时随着 History API 的到来，猫点已经可以用于处理标准 URLs （`/page`）。 **Backbone.Router** 为客户端路由提供了许多方法，并能连接到指定的动作（actions）和事件（events）。 对于不支持 History API 的旧浏览器，路由提供了优雅的回调函数并可以透明的进行 URL 片段的转换。

页面加载期间，当应用已经创建了所有的路由，需要调用 `Backbone.history.start()`，或 `Backbone.history.start({pushState: true})` 来确保驱动初始化 URL 的路由。

**extend**`Backbone.Router.extend(properties, [classProperties])` 开始创建一个自定义的路由类。当匹配了 URL 片段便执行定义的动作，并可以通过 routes 定义路由动作键值对。 请注意，你要避免在路由定义时使用前导斜杠：

```
var Workspace = Backbone.Router.extend({

  routes: {
    "help":                 "help",    // #help
    "search/:query":        "search",  // #search/kiwis
    "search/:query/p:page": "search"   // #search/kiwis/p7
  },

  help: function() {
    ...
  },

  search: function(query, page) {
    ...
  }

}); 
```

**routes**`router.routes` routes 将带参数的 URLs 映射到路由实例的方法上（或只是直接的函数定义，如果你喜欢），这与 View（视图） 的 events hash（事件键值对） 非常类似。 路由可以包含参数， `:param`，它在斜线之间匹配 URL 组件。 路由也支持通配符， `*splat`，可以匹配多个 URL 组件。 路由的可选部分放在括号中`(/:optional)`。

举个例子，路由 `"search/:query/p:page"` 能匹配`#search/obama/p2` , 这里传入了 `"obama"` 和 `"2"` 到路由对应的动作中去了。

路由 `"file/*path"`可以匹配 `#file/nested/folder/file.txt`，这时传入动作的参数为 `"nested/folder/file.txt"`。

路由 `"docs/:section(/:subsection)"`可以匹配`#docs/faq` 和 `#docs/faq/installing`，第一种情况，传入 `"faq"` 到路由对应的动作中去， 第二种情况，传入`"faq"` 和 `"installing"` 到路由对应的动作中去。

结尾的斜杠会被当作 URL 的一部分， 访问时会被（正确地）当作一个独立的路由。 `docs` 和 `docs/`将触发不同的回调。 如果你不能避免产生这两种类型的 URLs 时， 你可以定义一个`"docs(/)"`来匹配捕捉这两种情况。

当访问者点击浏览器后退按钮，或者输入 URL ，如果匹配一个路由，此时会触发一个基于动作名称的 event， 其它对象可以监听这个路由并接收到通知。 下面的示例中，用户访问 `#help/uploading` 将从路由中触发 `route:help` 事件。

```
routes: {
  "help/:page":         "help",
  "download/*path":     "download",
  "folder/:name":       "openFolder",
  "folder/:name-:mode": "openFolder"
} 
```

```
router.on("route:help", function(page) {
  ...
}); 
```

**constructor / initialize**`new Router([options])` 当创建一个新路由是，你可以直接传入 routes 键值对象作为参数。 如果定义该参数， 它们将被传入 `initialize` 构造函数中初始化。

**route**`router.route(route, name, [callback])` 为路由对象手动创建路由，`route` 参数可以是 routing string（路由字符串） 或 正则表达式。 每个捕捉到的被传入的路由或正则表达式，都将作为参数传入回调函数（callback）。 一旦路由匹配， `name` 参数会触发 `"route:name"` 事件。如果`callback`参数省略 `router[name]`将被用来代替。 后来添加的路由可以覆盖先前声明的路由。

```
initialize: function(options) {

  // Matches #page/10, passing "10"
  this.route("page/:number", "page", function(number){ ... });

  // Matches /117-a/b/c/open, passing "117-a/b/c" to this.open
  this.route(/^(.*?)\/open$/, "open");

},

open: function(id) { ... } 
```

**navigate**`router.navigate(fragment, [options])` 每当你达到你的应用的一个点时，你想保存为一个 URL， 可以调用**navigate**以更新的 URL。 如果您也想调用路由功能， 设置**trigger**选项设置为`true`。 无需在浏览器的历史记录创建条目来更新 URL， 设置 **replace**选项设置为`true`。

```
openPage: function(pageNumber) {
  this.document.pages.at(pageNumber).open();
  this.navigate("page/" + pageNumber);
}

# Or ...

app.navigate("help/troubleshooting", {trigger: true});

# Or ...

app.navigate("help/troubleshooting", {trigger: true, replace: true}); 
```

**execute**`router.execute(callback, args)` 这种方法在路由内部被调用， 每当路由和其相应的**callback**匹配时被执行。 覆盖它来执行自定义解析或包装路由， 例如， 在传递他们给你的路由回调之前解析查询字符串，像这样：

```
var Router = Backbone.Router.extend({
  execute: function(callback, args) {
    args.push(parseQueryString(args.pop()));
    if (callback) callback.apply(this, args);
  }
}); 
```