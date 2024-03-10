# 问答

# 问答

### 怎样定义模型?

Express 根本没有涉及到数据库，这个任务留给了第三方的 node 模块，有了第三方的模块基本上可以与任何数据库交互

### 怎样做用户认证?

这是另一个 Express 不会做的事情， 你可以使用任何你想用的认证方案，[这里有一个简单的例子](https://github.com/visionmedia/express/tree/master/examples/auth)。

### Express 支持哪个模板引擎?

任何遵守这样回调的 `(path, locals, callback)` . 为了统一模板引擎接口和缓存，推荐查看[consolidate.js](https://github.com/visionmedia/consolidate.js) 寻找帮助. 有些没有列出来的模板引擎没准也支持 Express.

### 我应该怎样组织我的程序结构?

事实上这个没有一个标准答案，这与你的程序规模和团队强烈相关。 为了尽可能的灵活，Express 没有规定程序的结构

你可以把路由和其它的一些程序特定的逻辑代码以任意的目录结构任意数量的文件存放。 查看下面的例子找点灵感

*   [Route listings](https://github.com/visionmedia/express/blob/master/examples/route-separation/index.js#L19)
*   [Route map](https://github.com/visionmedia/express/blob/master/examples/route-map/index.js#L47)
*   [Route bootstrapping](https://github.com/visionmedia/express/tree/master/examples/route-loading)
*   [MVC style controllers](https://github.com/visionmedia/express/tree/master/examples/mvc)

已经存在的简化这些模式的第三方 Express 扩展:

*   [Resourceful routing](https://github.com/visionmedia/express-resource)
*   [Namespaced routing](https://github.com/visionmedia/express-namespace)

### 我应该怎样从多个目录提供静态文件服务?

你可以会在你的程序中多次使用任意一个中间件。 使用下面的方式，当你请求"GET /javascripts/jquery.js" 时，会先检查 "./public/javascripts/jquery.js", 如果它不存在，随后的中间件会检查 "./files/javascripts/jquery.js".

```
app.use(express.static('public'));
app.use(express.static('files')); 
```

### 怎样在提供静态文件服务的时候加一个前缀路径名?

Connect's 的中间件绑定技术允许你指定一个路径名前缀, 一个常用的例子是你可以前缀一个根本不是请求路径中一部分的字符。 假设你要请求 "GET /files/javascripts/jquery.js", 你可以把中间件挂在 "/files", 暴露出 "/javascripts/jquery.js"作为 `req.url` 来让中间件为这个文件提供服务:

```
app.use('/public', express.static('public')); 
```

### 怎么迁移 Express 2.x 应用程序?

Express 2x 甚至能支持到 node 1.0, 所以可能没有必要由于 Express 3x 的重构和 API 改变就迁移，如果你对 2x 感觉良好，那就停留在那个版本上。真的要迁移可以看[这里](https://github.com/visionmedia/express/wiki/Migrating-from-2.x-to-3.x) 或者查看一下 3.x 的[改动列表](https://github.com/visionmedia/express/wiki/New-features-in-3.x)

### 怎么处理 404s?

在 Express 里 404s 不被认为是出错的结果，所以错误处理中间件不会捕获 404s,这是因为一个 404 只是由于有一些额外的工作没有做，换而言之，Express 已经执行了所有的中间件 / 路由分发，然而没有发现有返回。你所要做的仅仅是在代码底部加一个中间件去处理没有返回的情况，并且手动返回一个 404

```
app.use(function(req, res, next){
  res.send(404, 'Sorry cant find that!');
}); 
```

### Express 里怎样处理异常?

定义错误处理的中间件跟定义普通的中间件没有什么区别，仅仅是参数必须定义为 4 个，它们定义如下 `(err, req, res, next)`:

```
app.use(function(err, req, res, next){
  console.error(err.stack);
  res.send(500, 'Something broke!');
}); 
```

查看 错误处理, 获取更多信息

### 怎样输出纯 HTML 文件?

不要这么做！根本没有必要直接使用`res.render()`输出 HTML 文件, 如果你有一个特定的文件应该使用 `res.sendfile()`,如果你要使用一个目录里大量的静态资源提供服务，请使用 `express.static()` 中间件.

### Express 的代码库有多大？

Express 是一个非常小的框架，3.0.0 正式发布版只有 932 行源码，Express 强烈依赖的 Connect 只有 267 行源码，Connect 可选的中间件和扩展总共 1143 行源码，并且只有到使用时才会加载