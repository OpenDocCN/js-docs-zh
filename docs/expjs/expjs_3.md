# API 参考

### express()

创建一个 express 应用程序

```
var express = require('express');
var app = express();

app.get('/', function(req, res){
  res.send('hello world');
});

app.listen(3000); 
```

## Application

### app.set(name, value)

将设置项 `name` 的值设为 `value`

```
app.set('title', 'My Site');
app.get('title');
// => "My Site" 
```

### app.get(name)

获取设置项 `name` 的值

```
app.get('title');
// => undefined

app.set('title', 'My Site');
app.get('title');
// => "My Site" 
```

### app.enable(name)

将设置项 `name` 的值设为 `true`.

```
app.enable('trust proxy');
app.get('trust proxy');
// => true 
```

### app.disable(name)

将设置项 `name` 的值设为 `false`.

```
app.disable('trust proxy');
app.get('trust proxy');
// => false 
```

### app.enabled(name)

检查设置项 `name` 是否已启用

```
app.enabled('trust proxy');
// => false

app.enable('trust proxy');
app.enabled('trust proxy');
// => true 
```

### app.disabled(name)

检查设置项 `name` 是否已禁用

```
app.disabled('trust proxy');
// => true

app.enable('trust proxy');
app.disabled('trust proxy');
// => false 
```

### app.configure([env], callback)

当 `env` 和 `app.get('env')`(也就是 `process.env.NODE_ENV`) 匹配时, 调用`callback`。保留这个方法是出于历史原因，后面列出的`if`语句的代码其实更加高效、直接。使用`app.set()`配合其它一些配置方法后,*没有*必要再使用这个方法。

```
// 所有环境
app.configure(function(){
  app.set('title', 'My Application');
})

// 开发环境
app.configure('development', function(){
  app.set('db uri', 'localhost/dev');
})

// 只用于生产环境
app.configure('production', function(){
  app.set('db uri', 'n.n.n.n/prod');
}) 
```

更高效且直接的代码如下：

```
// 所有环境
app.set('title', 'My Application');

// 只用于开发环境
if ('development' == app.get('env')) {
  app.set('db uri', 'localhost/dev');
}

// 只用于生产环境
if ('production' == app.get('env')) {
  app.set('db uri', 'n.n.n.n/prod');
} 
```

### app.use([path], function)

使用中间件 `function`,可选参数`path`默认为"/"。

```
var express = require('express');
var app = express();

// 一个简单的 logger
app.use(function(req, res, next){
  console.log('%s %s', req.method, req.url);
  next();
});

// 响应
app.use(function(req, res, next){
  res.send('Hello World');
});

app.listen(3000); 
```

挂载的路径不会在 req 里出现，对中间件 `function`**不**可见，这意味着你在`function`的回调参数 req 里找不到 path。 这么设计的为了让间件可以在不需要更改代码就在任意"前缀"路径下执行

这里有一个实际应用场景，常见的一个应用是使用./public 提供静态文件服务， 用 `express.static()` 中间件:

```
// GET /javascripts/jquery.js
// GET /style.css
// GET /favicon.ico
app.use(express.static(__dirname + '/public')); 
```

如果你想把所有的静态文件路径都前缀"/static", 你可以使用“挂载”功能。 如果`req.url` 不包含这个前缀, 挂载过的中间件**不会**执行。 当`function`被执行的时候,这个参数不会被传递。 这个只会影响这个函数，后面的中间件里得到的 `req.url`里将会包含"/static"

```
// GET /static/javascripts/jquery.js
// GET /static/style.css
// GET /static/favicon.ico
app.use('/static', express.static(__dirname + '/public')); 
```

使用 `app.use()` “定义的”中间件的顺序非常重要，它们将会顺序执行，use 的先后顺序决定了中间件的优先级。 比如说通常 `express.logger()` 是最先使用的一个组件，纪录每一个请求

```
app.use(express.logger());
app.use(express.static(__dirname + '/public'));
app.use(function(req, res){
  res.send('Hello');
}); 
```

如果你想忽略请求静态文件的纪录，但是对于在 `logger()`之后定义的路由和中间件想继续纪录，只需要简单的把 `static()` 移到前面就行了:

```
app.use(express.static(__dirname + '/public'));
app.use(express.logger());
app.use(function(req, res){
  res.send('Hello');
}); 
```

另一个现实的例子，有可能从多个目录提供静态文件服务，下面的例子中会优先从"./public"目录取文件

```
app.use(express.static(__dirname + '/public'));
app.use(express.static(__dirname + '/files'));
app.use(express.static(__dirname + '/uploads')); 
```

### settings

下面的内建的可以改变 Express 行为的设置

*   `env` 运行时环境，默认为 `process.env.NODE_ENV` 或者 "development"
*   `trust proxy` 激活反向代理，默认未激活状态
*   `jsonp callback name` 修改默认`?callback=`的 jsonp 回调的名字
*   `json replacer` JSON replacer 替换时的回调, 默认为 null
*   `json spaces` JSON 响应的空格数量，开发环境下是`2` , 生产环境是`0`
*   `case sensitive routing` 路由的大小写敏感, 默认是关闭状态， "/Foo" 和"/foo" 是一样的
*   `strict routing` 路由的严格格式, 默认情况下 "/foo" 和 "/foo/" 是被同样对待的
*   `view cache` 模板缓存，在生产环境中是默认开启的
*   `view engine` 模板引擎
*   `views` 模板的目录, 默认是"process.cwd() + ./views"

### app.engine(ext, callback)

注册模板引擎的 `callback` 用来处理`ext`扩展名的文件 默认情况下, 根据文件扩展名`require()` 对应的模板引擎。 比如你想渲染一个 "foo.jade" 文件，Express 会在内部执行下面的代码，然后会缓存`require()`，这样就可以提高后面操作的性能

```
app.engine('jade', require('jade').__express); 
```

那些没有提供 `.__express` 的或者你想渲染一个文件的扩展名与模板引擎默认的不一致的时候，也可以用这个方法。 比如你想用 EJS 模板引擎来处理 ".html" 后缀的文件:

```
app.engine('html', require('ejs').renderFile); 
```

这个例子中 EJS 提供了一个`.renderFile()` 方法和 Express 预期的格式: `(path, options, callback)`一致, 可以在内部给这个方法取一个别名`ejs.__express`，这样你就可以使用".ejs" 扩展而不需要做任何改动

有些模板引擎没有遵循这种转换， 这里有一个小项目[consolidate.js](https://github.com/visionmedia/consolidate.js) 专门把所有的 node 流行的模板引擎进行了包装，这样它们在 Express 内部看起来就一样了。

```
var engines = require('consolidate');
app.engine('haml', engines.haml);
app.engine('html', engines.hogan); 
```

### app.param([name], callback)

路由参数的处理逻辑。比如当 `:user` 出现在一个路由路径中，你也许会自动载入加载用户的逻辑，并把它放置到 `req.user` , 或者校验一下输入的参数是否正确。

下面的代码片段展示了`callback`很像中间件，但是在参数里多加了一个值，这里名为`id`. 它会尝试加载用户信息，然后赋值给`req.user`, 否则就传递错误`next(err)`.

```
app.param('user', function(req, res, next, id){
  User.find(id, function(err, user){
    if (err) {
      next(err);
    } else if (user) {
      req.user = user;
      next();
    } else {
      next(new Error('failed to load user'));
    }
  });
}); 
```

另外你也可以只传一个`callback`, 这样你就有机会改变 `app.param()` API. 比如[express-params](http://github.com/visionmedia/express-params)定义了下面的回调，这个允许你使用一个给定的正则去限制参数。

下面的这个例子有一点点高级，检查如果第二个参数是一个正则，返回一个很像上面的"user"参数例子行为的回调函数。

```
app.param(function(name, fn){
  if (fn instanceof RegExp) {
    return function(req, res, next, val){
      var captures;
      if (captures = fn.exec(String(val))) {
        req.params[name] = captures;
        next();
      } else {
        next('route');
      }
    }
  }
}); 
```

这个函数现在可以非常有效的用来校验参数，或者提供正则捕获后的分组。

```
app.param('id', /^\d+$/);

app.get('/user/:id', function(req, res){
  res.send('user ' + req.params.id);
});

app.param('range', /^(\w+)\.\.(\w+)?$/);

app.get('/range/:range', function(req, res){
  var range = req.params.range;
  res.send('from ' + range[1] + ' to ' + range[2]);
}); 
```

### app.VERB(path, [callback...], callback)

`app.VERB()` 方法为 Express 提供路由方法, **VERB** 是指某一个 HTTP 动作, 比如 `app.post()`。 可以提供多个 callbacks,这多个 callbacks 都将会被平等对待 ，它们的行为跟中间件一样，也有一个例外的情况，如果某一个 callback 执行了`next('route')`，它后面的 callback 就被忽略。这种情形会应用在当满足一个路由前缀，但是不需要处理这个路由，于是把它向后传递。

下面的代码片段展示最简单的路由定义。Express 会把路径字符串转为正则表达式，然后在符合规则的请求到达时立即使用。 请求参数*不会* 被考虑进来，比如 "GET /" 会匹配下面的这个路由, 而"GET /?name=tobi"同样也会匹配。

```
app.get('/', function(req, res){
  res.send('hello world');
}); 
```

同样也可以使用正则表达式，并且它能够在你指定特定路径的时候发挥大作用。 比如下面的例子可以匹配"GET /commits/71dbb9c" ， 同时也能匹配 "GET /commits/71dbb9c..4c084f9".

```
app.get(/^\/commits\/(\w+)(?:\.\.(\w+))?$/, function(req, res){
  var from = req.params[0];
  var to = req.params[1] || 'HEAD';
  res.send('commit range ' + from + '..' + to);
}); 
```

可以传递一些回调，这对复用一些加载资源、校验的中间件很有用。

```
app.get('/user/:id', user.load, function(){
  // ... 
}) 
```

这些回调同样可以通过数组传递，简单的放置在数组中即可。

```
var middleware = [loadForum, loadThread];

app.get('/forum/:fid/thread/:tid', middleware, function(){
  // ...
})

app.post('/forum/:fid/thread/:tid', middleware, function(){
  // ...
}) 
```

### app.all(path, [callback...], callback)

这个方法很像`app.VERB()` , 但是它匹配所有的 HTTP 动作

这个方法在给特定前缀路径或者任意路径上处理时会特别有用。 比如你想把下面的路由放在所有其它路由之前，它需要所有从这个路由开始的加载验证，并且自动加载一个用户 记住所有的回调都不应该被当作终点， `loadUser` 能够被当作一个任务，然后`next()`去匹配接下来的路由。

```
app.all('*', requireAuthentication, loadUser); 
```

Or the equivalent:

```
app.all('*', requireAuthentication)
app.all('*', loadUser); 
```

另一个非常赞的例子是全局白名单函数。这里有一个例子跟前一个很像，但是它限制前缀为"/api":

```
app.all('/api/*', requireAuthentication); 
```

### app.locals

应用程序本地变量会附加给所有的在这个应用程序内渲染的模板。 这是一个非常有用的模板函数，就像应用程序级数据一样。

```
app.locals.title = 'My App';
app.locals.strftime = require('strftime'); 
```

`app.locals` 对象是一个 JavaScript `Function`, 执行的时候它会把属性合并到它自身，提供了一种简单展示已有对象作为本地变量的方法

```
app.locals({
  title: 'My App',
  phone: '1-250-858-9990',
  email: 'me@myapp.com'
});

app.locals.title
// => 'My App'

app.locals.email
// => 'me@myapp.com' 
```

`app.locals`对象最终会是一个 JavaScript 函数对象，你不可以使用 Functions 和 Objects 内置的属性，比如`name, apply, bind, call, arguments, length, constructor`

```
app.locals({name: 'My App'});

app.locals.name
// => 返回 'app.locals' 而不是 'My App' (app.locals 是一个函数 !)
// => 如果 name 变量用在一个模板里，发返回一个 ReferenceError 
```

全部的保留字列表可以在很多规范里找到。 [JavaScript 规范](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference) 介绍了原来的属性，有一些还会被现代的 JS 引擎识别，[EcmaScript 规范](http://www.ecma-international.org/ecma-262/5.1/) 在它的基础上，统一了值，添加了一些，删除了一些废弃的。如果感兴趣，可以看看 Functions 和 Objects 的属性值。

默认情况下 Express 只有一个应用程序级本地变量，它是 `settings`.

```
app.set('title', 'My App');
// 在 view 里使用 settings.title 
```

### app.render(view, [options], callback)

渲染 `view`, `callback` 用来处理返回的渲染后的字符串。 这个是 `res.render()` 的应用程序级版本，它们的行为是一样的。

```
app.render('email', function(err, html){
  // ...
});

app.render('email', { name: 'Tobi' }, function(err, html){
  // ...
}); 
```

### app.routes

`app.routes` 对象存储了所有的被 HTTP verb 定义路由。 这个对象可以用在一些内部功能上，比如 Express 不仅用它来做路由分发，同时在没有`app.options()`定义的情况下用它来处理默认的<string>OPTIONS</string>行为。 你的应用程序或者框架也可以很轻松的通过在这个对象里移除路由来达到删除路由的目的。

```
console.log(app.routes)

{ get: 
   [ { path: '/',
       method: 'get',
       callbacks: [Object],
       keys: [],
       regexp: /^\/\/?$/i },
   { path: '/user/:id',
       method: 'get',
       callbacks: [Object],
       keys: [{ name: 'id', optional: false }],
       regexp: /^\/user\/(?:([^\/]+?))\/?$/i } ],
delete: 
   [ { path: '/user/:id',
       method: 'delete',
       callbacks: [Object],
       keys: [Object],
       regexp: /^\/user\/(?:([^\/]+?))\/?$/i } ] } 
```

### app.listen()

在给定的主机和端口上监听请求，这个和 node 的文档[http.Server#listen()](http://nodejs.org/api/http.html#http_server_listen_port_hostname_backlog_callback)是一致的

```
var express = require('express');
var app = express();
app.listen(3000); 
```

`express()`返回的`app`实际上是一个 JavaScript`Function`,它被设计为传给 node 的 http servers 作为处理请求的回调函数。因为`app`不是从 HTTP 或者 HTTPS 继承来的，它只是一个简单的回调函数，你可以以同一份代码同时处理 HTTP and HTTPS 版本的服务。

```
var express = require('express');
var https = require('https');
var http = require('http');
var app = express();

http.createServer(app).listen(80);
https.createServer(options, app).listen(443); 
```

`app.listen()` 方法只是一个快捷方法，如果你想使用 HTTPS，或者同时提供 HTTP 和 HTTPS，可以使用上面的代码

```
app.listen = function(){
  var server = http.createServer(this);
  return server.listen.apply(server, arguments);
}; 
```

## Request

### req.params

这是一个数组对象，命名过的参数会以键值对的形式存放。 比如你有一个路由`/user/:name`, "name"属性会存放在`req.params.name`. 这个对象默认为 `{}`.

```
// GET /user/tj
req.params.name
// => "tj" 
```

当使用正则表达式定义路由的时候，`req.params[N]`会是这个应用这个正则后的捕获分组, `N` 是代表的是第 N 个捕获分组。这个规则同样适用于全匹配的路由，如 `/file/*`:

```
// GET /file/javascripts/jquery.js
req.params[0]
// => "javascripts/jquery.js" 
```

### req.query

这是一个解析过的请求参数对象，默认为`{}`.

```
// GET /search?q=tobi+ferret
req.query.q
// => "tobi ferret"

// GET /shoes?order=desc&shoe[color]=blue&shoe[type]=converse
req.query.order
// => "desc"

req.query.shoe.color
// => "blue"

req.query.shoe.type
// => "converse" 
```

### req.body

这个对应的是解析过的请求体。这个特性是`bodyParser()` 中间件提供,其它的请求体解析中间件可以放在这个中间件之后。当`bodyParser()`中间件使用后，这个对象默认为 `{}`。

```
// POST user[name]=tobi&user[email]=tobi@learnboost.com
req.body.user.name
// => "tobi"

req.body.user.email
// => "tobi@learnboost.com"

// POST { "name": "tobi" }
req.body.name
// => "tobi" 
```

### req.files

这是上传的文件的对象。这个特性是`bodyParser()` 中间件提供,其它的请求体解析中间件可以放在这个中间件之后。当`bodyParser()`中间件使用后，这个对象默认为 `{}`。

例如 **file** 字段被命名为"image", 当一个文件上传完成后，`req.files.image` 将会包含下面的 `File` 对象:

```
{ size: 74643,
  path: '/tmp/8ef9c52abe857867fd0a4e9a819d1876',
  name: 'edge.png',
  type: 'image/png',
  hash: false,
  lastModifiedDate: Thu Aug 09 2012 20:07:51 GMT-0700 (PDT),
  _writeStream: 
   { path: '/tmp/8ef9c52abe857867fd0a4e9a819d1876',
     fd: 13,
     writable: false,
     flags: 'w',
     encoding: 'binary',
     mode: 438,
     bytesWritten: 74643,
     busy: false,
     _queue: [],
     _open: [Function],
     drainable: true },
  length: [Getter],
  filename: [Getter],
  mime: [Getter] } 
```

`bodyParser()` 中间件是在内部使用[node-formidable](https://github.com/felixge/node-formidable)来处理文件请求，所以接收的参数是一致的。 举个例子，使用 formidable 的选项`keepExtensions` , 它默认为 **false** , 在上面的例子可以看到给出的文件名"/tmp/8ef9c52abe857867fd0a4e9a819d1876" 不包含".png" 扩展名. 为了让它可以保留扩展名，你可以把参数传给 `bodyParser()`:

```
app.use(express.bodyParser({ keepExtensions: true, uploadDir: '/my/files' })); 
```

### req.param(name)

返回 `name` 参数的值。

```
// ?name=tobi
req.param('name')
// => "tobi"

// POST name=tobi
req.param('name')
// => "tobi"

// /user/tobi for /user/:name 
req.param('name')
// => "tobi" 
```

查找的优先级如下:

*   `req.params`
*   `req.body`
*   `req.query`

直接访问 `req.body`, `req.params`, 和 `req.query` 应该更合适，除非你真的需要从这几个对象里同时接受输入。

### req.route

这个对象里是当前匹配的 `Route` 里包含的属性，比如原始路径字符串，产生的正则，等等

```
app.get('/user/:id?', function(req, res){
  console.log(req.route);
}); 
```

上面代码的一个输出:

```
{ path: '/user/:id?',
  method: 'get',
  callbacks: [ [Function] ],
  keys: [ { name: 'id', optional: true } ],
  regexp: /^\/user(?:\/([^\/]+?))?\/?$/i,
  params: [ id: '12' ] } 
```

### req.cookies

当使用 `cookieParser()`中间件之后，这个对象默认为`{}`, 它也包含了用户代理传过来的 cookies。

```
// Cookie: name=tj
req.cookies.name
// => "tj" 
```

### req.signedCookies

当使用了`cookieParser(secret)` 中间件后，这个对象默认为`{}`, 否则包含了用户代理传回来的签名后的 cookie，并等待使用。签名后的 cookies 被放在一个单独的对象里，恶意攻击者可以很简单的替换掉`req.cookie` 的值。需要注意的是签名的 cookie 不代表它是隐藏的或者加密的，这个只是简单的阻止篡改 cookie。

```
// Cookie: user=tobi.CP7AWaXDfAKIRfH49dQzKJx7sKzzSoPq7/AcBBRVwlI3
req.signedCookies.user
// => "tobi" 
```

### req.get(field)

获取请求头里的`field`的值，大小写不敏感. *Referrer* 和 *Referer* 字段是可以互换的。

```
req.get('Content-Type');
// => "text/plain"

req.get('content-type');
// => "text/plain"

req.get('Something');
// => undefined 
```

别名为 `req.header(field)`.

### req.accepts(types)

. 检查给定的`types` 是不是可以接受类型，当可以接受时返回最匹配的，否则返回`undefined` - 这个时候你应该响应一个 406 "Not Acceptable".

`type` 的值可能是单一的一个 mime 类型字符串,比如 "application/json", 扩展名为"json", 也可以为逗号分隔的列表或者数组。当给定的是数组或者列表，返回*最佳*匹配的。

```
// Accept: text/html
req.accepts('html');
// => "html"

// Accept: text/*, application/json
req.accepts('html');
// => "html"
req.accepts('text/html');
// => "text/html"
req.accepts('json, text');
// => "json"
req.accepts('application/json');
// => "application/json"

// Accept: text/*, application/json
req.accepts('image/png');
req.accepts('png');
// => undefined

// Accept: text/*;q=.5, application/json
req.accepts(['html', 'json']);
req.accepts('html, json');
// => "json" 
```

### req.accepted

返回一个从高质量到低质量排序的接受媒体类型数组

```
[ { value: 'application/json',
    quality: 1,
    type: 'application',
    subtype: 'json' },
{ value: 'text/html',
     quality: 0.5,
     type: 'text',
     subtype: 'html' } ] 
```

### req.is(type)

检查请求的文件头是不是包含"Content-Type" 字段, 它匹配给定的`type`.

```
// With Content-Type: text/html; charset=utf-8
req.is('html');
req.is('text/html');
req.is('text/*');
// => true

// When Content-Type is application/json
req.is('json');
req.is('application/json');
req.is('application/*');
// => true

req.is('html');
// => false 
```

### req.ip

返回远程地址，或者当“信任代理”使用时，返回上一级的地址

```
req.ip
// => "127.0.0.1" 
```

### req.ips

当设置"trust proxy" 为 `true`时, 解析"X-Forwarded-For" 里的 ip 地址列表，并返回一个数组 否则返回一个空数组 举个例子，如果"X-Forwarded-For" 的值为"client, proxy1, proxy2" 你将会得到数组`["client", "proxy1", "proxy2"]` 这里可以看到 "proxy2" 是最近一个使用的代理

### req.path

返回请求的 URL 的路径名

```
// example.com/users?sort=desc
req.path
// => "/users" 
```

### req.host

返回从"Host"请求头里取的主机名,不包含端口号。

```
// Host: "example.com:3000"
req.host
// => "example.com" 
```

### req.fresh

判断请求是不是新的-通过对 Last-Modified 或者 ETag 进行匹配, 来标明这个资源是不是"新的".

```
req.fresh
// => true 
```

### req.stale

判断请求是不是旧的-如果 Last-Modified 或者 ETag 不匹配, 标明这个资源是"旧的". Check if the request is stale - aka Last-Modified and/or the ETag do not match, indicating that the resource is "stale".

```
req.stale
// => true 
```

### req.xhr

判断请求头里是否有"X-Requested-With"这样的字段并且值为"XMLHttpRequest", jQuery 等库发请求时会设置这个头

```
req.xhr
// => true 
```

### req.protocol

返回标识请求协议的字符串，一般是"http"，当用 TLS 请求的时候是"https"。 当"trust proxy" 设置被激活， "X-Forwarded-Proto" 头部字段会被信任。 如果你使用了一个支持 https 的反向代理，那这个可能是激活的。

```
req.protocol
// => "http" 
```

### req.secure

检查 TLS 连接是否已经建立。 这是下面的缩写:

```
'https' == req.protocol; 
```

### req.subdomains

把子域当作一个数组返回

```
// Host: "tobi.ferrets.example.com"
req.subdomains
// => ["ferrets", "tobi"] 
```

### req.originalUrl

这个属性很像 `req.url`, 但是它保留了原始的 url。 这样你在做内部路由的时候可以重写`req.url`。 比如 app.use()的挂载功能会重写 `req.url`，把从它挂载的点开始

```
// GET /search?q=something
req.originalUrl
// => "/search?q=something" 
```

### req.acceptedLanguages

返回一个从高质量到低质量排序的接受语言数组

```
Accept-Language: en;q=.5, en-us
// => ['en-us', 'en'] 
```

### req.acceptedCharsets

返回一个从高质量到低质量排序的可接受的字符集数组

```
Accept-Charset: iso-8859-5;q=.2, unicode-1-1;q=0.8
// => ['unicode-1-1', 'iso-8859-5'] 
```

### req.acceptsCharset(charset)

检查给定的`charset` 是不是可以接受的

### req.acceptsLanguage(lang)

检查给定的 `lang` 是不是可以接受的

## Response

### res.status(code)

支持链式调用的 node's `res.statusCode=`.

```
res.status(404).sendfile('path/to/404.png'); 
```

### res.set(field, [value])

设置响应头字段`field` 值为 `value`, 也可以一次传入一个对象设置多个值。

```
res.set('Content-Type', 'text/plain');

res.set({
  'Content-Type': 'text/plain',
  'Content-Length': '123',
  'ETag': '12345'
}) 
```

`res.header(field, [value])`的别名。

### res.get(field)

返回一个大小写不敏感的响应头里的 `field`的值

```
res.get('Content-Type');
// => "text/plain" 
```

### res.cookie(name, value, [options])

设置 cookie `name` 值为`value`, 接受字符串参数或者 JSON 对象。 `path` 属性默认为 "/".

```
res.cookie('name', 'tobi', { domain: '.example.com', path: '/admin', secure: true });
res.cookie('rememberme', '1', { expires: new Date(Date.now() + 900000), httpOnly: true }); 
```

`maxAge` 属性是一个便利的设置"expires",它是一个从当前时间算起的毫秒。 下面的代码和上一个例子中的第二行是同样的作用。

```
res.cookie('rememberme', '1', { maxAge: 900000, httpOnly: true }) 
```

可以传一个序列化的 JSON 对象作为参数， 它会自动被`bodyParser()` 中间件解析。

```
res.cookie('cart', { items: [1,2,3] });
res.cookie('cart', { items: [1,2,3] }, { maxAge: 900000 }); 
```

这个方法也支持签名的 cookies。 只需要简单的传递`signed` 参数。 `res.cookie()` 会使用通过 `express.cookieParser(secret)` 传 入的 secret 来签名这个值

```
res.cookie('name', 'tobi', { signed: true }); 
```

稍后你就可以通过 req.signedCookie 对象访问到这个值。

### res.clearCookie(name, [options])

把`name`的 cookie 清除. `path`参数默认为 "/".

```
res.cookie('name', 'tobi', { path: '/admin' });
res.clearCookie('name', { path: '/admin' }); 
```

### res.redirect([status], url)

使用可选的状态码跳转到`url` 状态码`status`默认为 302 "Found".

```
res.redirect('/foo/bar');
res.redirect('http://example.com');
res.redirect(301, 'http://example.com');
res.redirect('../login'); 
```

Express 支持几种跳转，第一种便是使用一个完整的 URI 跳转到一个完全不同的网站。

```
res.redirect('http://google.com'); 
```

第二种是相对根域路径跳转，比如你现在在 `http://example.com/admin/post/new`, 下面的的代码跳转到 `/admin` 将会把你带到`http://example.com/admin`:

```
res.redirect('/admin'); 
```

这是一种相对于应用程序挂载点的跳转。 比如把一个 blog 程序挂在 `/blog`, 事实上它无法知道它被挂载，所以当你使用跳转 `/admin/post/new` 时，将到跳到`http://example.com/admin/post/new`, 下面的相对于挂载点的跳转会把你带到 `http://example.com/blog/admin/post/new`:

```
res.redirect('admin/post/new'); 
```

路径名.跳转同样也是支持的。 比如你在`http://example.com/admin/post/new`, 下面的跳转会把你带到 `http//example.com/admin/post`:

```
res.redirect('..'); 
```

最后也是最特别的跳转是 `back` 跳转, 它会把你带回 Referer（也有可能是 Referrer）的地址 当 Referer 丢失的时候默认为 `/`

```
res.redirect('back'); 
```

### res.location

设置 location 请求头.

```
res.location('/foo/bar');
res.location('foo/bar');
res.location('http://example.com');
res.location('../login');
res.location('back'); 
```

可以使用与 `res.redirect()`里相同的`urls`。

举个例子，如果你的程序根地址是`/blog`, 下面的代码会把 `location` 请求头设置为`/blog/admin`:

```
res.location('admin') 
```

### res.charset

设置字符集。默认为"utf-8"。

```
res.charset = 'value';
res.send('some html');
// => Content-Type: text/html; charset=value 
```

### res.send([body|status], [body])

发送一个响应。

```
res.send(new Buffer('whoop'));
res.send({ some: 'json' });
res.send('some html');
res.send(404, 'Sorry, we cannot find that!');
res.send(500, { error: 'something blew up' });
res.send(200); 
```

这个方法在输出 non-streaming 响应的时候自动完成了大量有用的任务 比如如果在它前面没有定义 Content-Length, 它会自动设置; 比如加一些自动的 *HEAD*; 比如对 HTTP 缓存的支持 .

当参数为一个 `Buffer`时 Content-Type 会被设置为 "application/octet-stream" 除非它之前有像下面的代码：

```
res.set('Content-Type', 'text/html');
res.send(new Buffer('some html')); 
```

当参数为一个`String`时 Content-Type 默认设置为"text/html":

```
res.send('some html'); 
```

当参数为 `Array` 或者 `Object` 时 Express 会返回一个 JSON :

```
res.send({ user: 'tobi' })
res.send([1,2,3]) 
```

最后一条当一个`Number` 作为参数， 并且没有上面提到的任何一条在响应体里， Express 会帮你设置一个响应体 比如 200 会返回字符"OK", 404 会返回"Not Found"等等.

```
res.send(200)
res.send(204)
res.send(500) 
```

### res.json([status|body], [body])

返回一个 JSON 响应。 当`res.send()` 的参数是一个对象或者数组的时候， 会调用这个方法。 当然它也在复杂的空值(null, undefined, etc)JSON 转换的时候很有用， 因为规范上这些对象不是合法的 JSON。

```
res.json(null)
res.json({ user: 'tobi' })
res.json(500, { error: 'message' }) 
```

### res.jsonp([status|body], [body])

返回一个支持 JSONP 的 JSON 响应。 Send a JSON response with JSONP support. 这个方法同样使用了`res.json()`, 只是加了一个可以自定义的 JSONP 回调支持。

```
res.jsonp(null)
// => null

res.jsonp({ user: 'tobi' })
// => { "user": "tobi" }

res.jsonp(500, { error: 'message' })
// => { "error": "message" } 
```

默认情况下 JSONP 回调的函数名就是`callback`。 你可以通过 jsonp callback name 来修改这个值。 下面是一些使用 JSONP 的例子。

```
// ?callback=foo
res.jsonp({ user: 'tobi' })
// => foo({ "user": "tobi" })

app.set('jsonp callback name', 'cb');

// ?cb=foo
res.jsonp(500, { error: 'message' })
// => foo({ "error": "message" }) 
```

### res.type(type)

设置 Sets the Content-Type to the mime lookup of `type`, or when "/" is present the Content-Type is simply set to this literal value.

```
res.type('.html');
res.type('html');
res.type('json');
res.type('application/json');
res.type('png'); 
```

`res.contentType(type)`方法的别名。

### res.format(object)

设置特定请求头的响应。 这个方法使用 `req.accepted`， 这是一个通过质量值作为优先级顺序的数组， 第一个回调会被执行。 当没有匹配时，服务器返回一个 406 "Not Acceptable", 或者执行`default` 回调

Content-Type 在 callback 被选中执行的时候会被设置好, 如果你想改变它，可以在 callback 内使用`res.set()`或者 `res.type()` 等

下面的例子展示了在请求头设置为"application/json" 或者 "*/json"的时候 会返回`{ "message": "hey" }` 如果设置的是"*/*" 那么所有的返回都将是"hey"

```
res.format({
  'text/plain': function(){
    res.send('hey');
  },

  'text/html': function(){
    res.send('hey');
  },

  'application/json': function(){
    res.send({ message: 'hey' });
  }
}); 
```

除了使用标准的 MIME 类型，你也可以使用扩展名来映射这些类型 下面是一个不太完整的实现：

```
res.format({
  text: function(){
    res.send('hey');
  },

  html: function(){
    res.send('hey');
  },

  json: function(){
    res.send({ message: 'hey' });
  }
}); 
```

### res.attachment([filename])

设置响应头的 Content-Disposition 字段值为 "attachment". 如果有`filename` 参数，Content-Type 将会依据文件扩展名通过`res.type()`自动设置, 并且 Content-Disposition 的"filename="参数将会被设置

```
res.attachment();
// Content-Disposition: attachment

res.attachment('path/to/logo.png');
// Content-Disposition: attachment; filename="logo.png"
// Content-Type: image/png 
```

### res.sendfile(path, [options], [fn]])

`path`所传输附件的路径。

它会根据文件的扩展名自动设置响应头里的 Content-Type 字段。 回调函数`fn(err)`在传输完成或者发生错误时会被调用执行。

Options:

*   `maxAge` 毫秒，默认为 0
*   `root` 文件相对的路径

这个方法可以非常良好的支持有缩略图的文件服务。

```
app.get('/user/:uid/photos/:file', function(req, res){
  var uid = req.params.uid
    , file = req.params.file;

  req.user.mayViewFilesFrom(uid, function(yes){
    if (yes) {
      res.sendfile('/uploads/' + uid + '/' + file);
    } else {
      res.send(403, 'Sorry! you cant see that.');
    }
  });
}); 
```

### res.download(path, [filename], [fn])

`path`所需传输附件的路径， 通常情况下浏览器会弹出一个下载文件的窗口。 浏览器弹出框里的文件名和响应头里的 Disposition "filename=" 参数是一致的, 你也可以通过传入`filename`来自由设置。

当在传输的过程中发生一个错误时，可选的回调函数`fn`会被调用执行。 这个方法使用 res.sendfile()传输文件。

```
res.download('/report-12345.pdf');

res.download('/report-12345.pdf', 'report.pdf');

res.download('/report-12345.pdf', 'report.pdf', function(err){
  if (err) {
    // 处理错误，请牢记可能只有部分内容被传输，所以
    // 检查一下 res.headerSent
  } else {
    // 减少下载的积分值之类的
  }
}); 
```

### res.links(links)

合并给定的`links`, 并且设置给响应头里的"Link" 字段.

```
res.links({
  next: 'http://api.example.com/users?page=2',
  last: 'http://api.example.com/users?page=5'
}); 
```

转换后:

```
Link: <http://api.example.com/users?page=2>; rel="next", 
      <http://api.example.com/users?page=5>; rel="last" 
```

### res.locals

在某一次请求范围下的响应体的本地变量，只对此次请求期间的 views 可见。 另外这个 API 其实和 app.locals 是一样的.

这个对象在放置请求级信息时非常有用，比如放置请求的路径名，验证过的用户，用户设置等等

```
app.use(function(req, res, next){
  res.locals.user = req.user;
  res.locals.authenticated = ! req.user.anonymous;
  next();
}); 
```

### res.render(view, [locals], callback)

渲染`view`, 同时向 callback 传入渲染后的字符串。 callback 如果不传的话，直接会把渲染后的字符串输出至请求方， 一般如果不需要再对渲染后的模板作操作，就不需要传 callback。 当有错误发生时`next(err)`会被执行. 如果提供了 callback 参数，可能发生的错误和渲染的字符串都会被当作参数传入, 并且没有默认响应。

```
res.render('index', function(err, html){
  // ...
});

res.render('user', { name: 'Tobi' }, function(err, html){
  // ...
}); 
```

## Middleware

### basicAuth()

基本的认证中间件，在`req.user`里添加用户名

用户名和密码的例子:

```
app.use(express.basicAuth('username', 'password')); 
```

校验回调:

```
app.use(express.basicAuth(function(user, pass){
  return 'tj' == user && 'wahoo' == pass;
})); 
```

异步校验接受参数`fn(err, user)`, 下面的例子`req.user` 将会作为 user 对象传递.

```
app.use(connect.basicAuth(function(user, pass, fn){
  User.authenticate({ user: user, pass: pass }, fn);
})) 
```

### bodyParser()

支持 JSON, urlencoded 和 multipart requests 的请求体解析中间件。 这个中间件是`json()`, `urlencoded()`,和`multipart()` 这几个中间件的简单封装

```
app.use(express.bodyParser());

// 等同于:
app.use(express.json());
app.use(express.urlencoded());
app.use(express.multipart()); 
```

从安全上考虑，如果你的应用程序不需要文件上传功能，最好关闭它。我们只使用我们需要的中间件。例如：我们不使用`bodyParser`、`multipart()` 这两个中间件。

```
app.use(express.json());
app.use(express.urlencoded()); 
```

如果你的应用程序需要使用文件上传，设置一下就行。 [一个简单的介绍如何使用](https://groups.google.com/d/msg/express-js/iP2VyhkypHo/5AXQiYN3RPcJ).

### compress()

通过 gzip / deflate 压缩响应数据. 这个中间件应该放置在所有的中间件最前面以保证所有的返回都是被压缩的

```
app.use(express.logger());
app.use(express.compress());
app.use(express.methodOverride());
app.use(express.bodyParser()); 
```

### cookieParser()

解析请求头里的 Cookie, 并用 cookie 名字的键值对形式放在 `req.cookies` 你也可以通过传递一个`secret` 字符串激活签名了的 cookie

```
app.use(express.cookieParser());
app.use(express.cookieParser('some secret')); 
```

### cookieSession()

提供一个以 cookie 为基础的 sessions, 设置在`req.session`里。 这个中间件有以下几个选项:

*   `key` cookie 的名字，默认是 `connect.sess`
*   `secret` prevents cookie tampering
*   `cookie` session cookie 设置, 默认是 `{ path: '/', httpOnly: true, maxAge: null }`
*   `proxy` 当设置安全 cookies 时信任反向代理 (通过 "x-forwarded-proto")

```
app.use(express.cookieSession()); 
```

清掉一个 cookie, 只需要在响应前把 null 赋值给 session:

```
req.session = null 
```

### csrf()

CSRF 防护中间件

默认情况下这个中间件会产生一个名为"_csrf"的标志，这个标志应该添加到那些需要服务器更改的请求里，可以放在一个表单的隐藏域，请求参数等。这个标志可以通过 `req.csrfToken()`方法进行校验。

`bodyParser()` 中间件产生的 `req.body` , `query()`产生的`req.query`,请求头里的"X-CSRF-Token"是默认的 `value` 函数检查的项

这个中间件需要 session 支持，因此它的代码应该放在`session()`之后.

### directory()

文件夹服务中间件，用 `path` 提供服务。

```
app.use(express.directory('public'))
app.use(express.static('public')) 
```

这个中间件接收如下参数：

*   `hidden` 显示隐藏文件，默认为 false.
*   `icons` 显示图标，默认为 false.
*   `filter` 在文件上应用这个过滤函数。默认为 false.