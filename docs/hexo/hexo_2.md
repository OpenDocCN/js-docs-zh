# API

# API

# 核心

# 核心

# 概述

# 概述

本文件提供您更丰富的 API 信息，使您更容易修改 Hexo 源代码或编写插件。如果您只是想查询 Hexo 的基本使用方法，请参阅 文档。

在开始之前，请注意本文件仅适用于 Hexo 3 及以上版本。

## 初始化

首先，我们必须建立一个 Hexo 实例（instance），第一个参数是网站的根目录，也就是 `base_dir`，而第二个参数则是初始化的选项。接著执行 `init` 方法后，Hexo 会加载插件及配置文件。

```
varrequire'hexo'
varnew
hexo.init().then(function{  // ...
}); 
```

| 参数 | 描述 | 默认值 |
| --- | --- | --- |
| `debug` | 开启调试模式。在终端中显示调试信息，并在根目录中存储 `debug.log` 日志文件。 | `false` |
| `safe` | 开启安全模式。不加载任何插件。 | `false` |
| `silent` | 开启安静模式。不在终端中显示任何信息。 | `false` |
| `config` | 指定配置文件的路径。 | `_config.yml` |

## 载入文件

Hexo 提供了两种方法来载入文件：`load`, `watch`，前者用于载入 `source` 文件夹内的所有文件及主题资源；而后者除了执行 `load` 以外，还会继续监视文件变动。

这两个方法实际上所做的，就是载入文件列表，并把文件传给相对应的处理器（Processor），当文件全部处理完毕后，就执行生成器（Generator）来建立路由。

```
hexo.load().then(function{  // ...
});hexo.watch().then(function{  // 之后可以调用 hexo.unwatch()，停止监视文件
}); 
```

## 执行指令

您可以通过 `call` 方法来调用控制台（Console），第一个参数是控制台的名称，而第二个参数是选项——根据不同控制台有所不同。

```
hexo.call('generate'function{  // ...
}); 
```

## 结束

当指令完毕后，请执行 `exit` 方法让 Hexo 退出结束前的准备工作（如存储资料库）。

```
hexo.call('generate'function{  return
}).catch(functionerr{  return
}); 
```

# 事件

# 事件

Hexo 继承了 [EventEmitter](http://nodejs.org/api/events.html)，您可以用 `on` 方法监听 Hexo 所发布的事件，也可以使用 `emit` 方法对 Hexo 发布事件，更详细的说明请参阅 Node.js 的 API。

### deployBefore

在部署完成前发布。

### deployAfter

在部署成功后发布。

### exit

在 Hexo 结束前发布。

### generateBefore

在静态文件生成前发布。

### generateAfter

在静态文件生成后发布。

### new

在文章文件建立后发布。该事件返回文章参数。

```
hexo.on('new'functionpost{  // 
}); 
```

| 资料 | 描述 |
| --- | --- |
| `post.path` | 文章文件的完整路径 |
| `post.content` | 文章文件的内容 |

### processBefore

在处理原始文件前发布。此事件会返回一个地址，代表 Box（Box）的根目录。

### processAfter

在原始文件处理后发布。此事件会返回一个地址，代表 Box（Box）的根目录。

### ready

在初始化完成后发布。

# 局部变量

# 局部变量

局部变量用于模版渲染，也就是模版中的 `site` 变量。

## 默认变量

| 变量 | 描述 |
| --- | --- |
| `posts` | 所有文章 |
| `pages` | 所有分页 |
| `categories` | 所有分类 |
| `tags` | 所有标签 |

## 获取变量

```
hexo.locals.get('posts' 
```

## 设置变量

```
hexo.locals.set('posts'function{  return
}); 
```

## 移除变量

```
hexo.locals.remove('posts' 
```

## 获取所有变量

```
hexo.locals.toObject(); 
```

## 清除缓存

```
hexo.locals.invalidate(); 
```

# 路由

# 路由

路由存储了网站中所用到的所有路径。

## 获取路径

`get` 方法会传回一个 [Stream](http://nodejs.org/api/stream.html)，例如把该路径的资料存储到某个指定位置。

```
var'index.html'
var'somewhere'
data.pipe(dest); 
```

## 设置路径

您可以在 `set` 方法中使用字符串、[Buffer](http://nodejs.org/api/buffer.html) 或函数，如下：

```
// String
hexo.route.set('index.html''index'
// Buffer
hexo.route.set('index.html'new'index'
// Function (Promise)
hexo.route.set('index.html'function{  returnnewPromisefunctionresolve, reject{    resolve('index'
  });});// Function (Callback)
hexo.route.set('index.html'functioncallback{  callback(null'index'
}); 
```

您还可以设置该路径是否更新，这样在生成文件时便能忽略未更动的文件，加快生成时间。

```
hexo.route.set('index.html'
    data: 'index'
    modified: false
});// hexo.route.isModified('index.html') => false 
```

## 移除路径

```
hexo.route.remove('index.html' 
```

## 获得路由表

```
hexo.route.list(); 
```

## 格式化路径

`format` 方法可将字符串转为合法的路径。

```
hexo.route.format('archives/'
// archives/index.html 
```

# Box

# Box

「Box」是 Hexo 用来处理特定文件夹中的文件的容器，在 Hexo 中有两个 Box，分别是 `hexo.source` 和 `hexo.theme`，前者用于处理 `source` 文件夹，而后者用于处理主题文件夹。

## 载入文件

Box 提供了两种方法来载入文件：`process`, `watch`，前者用于载入文件夹内的所有文件；而后者除了执行 `process` 以外，还会继续监视文件变动。

```
box.process().then(function{  // ...
});box.watch().then(function{  // 之后可调用 box.unwatch()，停止监视文件
}); 
```

## 比对路径

Box 提供了多种比对路径的模式，您可以以使用正则表达式（regular expression）、函数、或是一种类似于 Express 的路径字符串，例如：

```
posts/:id => posts/89
posts/*path => posts/2015/title 
```

您可以以参考 [util.Pattern](https://github.com/hexojs/hexo-util#patternrule) 以获得更多信息。

## 处理器（Processor）

处理器（Processor）是 Box 中非常重要的元素，它用于处理文件，您可以使用上述的路径对比来限制该处理器所要处理的文件类型。使用 `addProcessor` 来添加处理器。

```
box.addProcessor('posts/:id'functionfile{  //
}); 
```

Box 在处理时会把目前处理的文件内容（`file`）传给处理器，您可以通过此参数获得该文件的数据。

| 属性 | 描述 |
| --- | --- |
| `source` | 文件完整路径 |
| `path` | 文件相对于 Box 的路径 |
| `type` | 文件类型。有 `create`, `update`, `skip`, `delete`。 |
| `params` | 从路径对比中取得的信息 |

Box 还提供了一些方法，让您无须手动处理文件 I/O。

| 方法 | 描述 |
| --- | --- |
| `read` | 读取文件 |
| `readSync` | 同步读取文件 |
| `stat` | 读取文件状态 |
| `statSync` | 同步读取文件状态 |
| `render` | 渲染文件 |
| `renderSync` | 同步渲染文件 |

# 渲染

# 渲染

在 Hexo 中，有两个方法可用于渲染文件或字符串，分别是非同步的 `hexo.render.render` 和同步的 `hexo.render.renderSync`，这两个方法的使用方式十分类似，因此以下仅以非同步的 `hexo.render.render` 为例。

## 渲染字符串

在渲染字符串时，您必须指定 `engine`，如此一来 Hexo 才知道该使用哪个渲染引擎来渲染。

```
hexo.render.render({text: 'example''swig'functionresult{  // ...
}); 
```

## 渲染文件

在渲染文件时，您无须指定 `engine`，Hexo 会自动根据扩展名猜测所要使用的渲染引擎，当然您也可以使用 `engine` 指定。

```
hexo.render.render({path: 'path/to/file.swig'functionresult{  // ...
}); 
```

## 渲染选项

在渲染时，您可以向第二个参数中传入参数。

```
hexo.render.render({text: '''foo'functionresult{  // ...
}); 
```

## after_render 过滤器

在渲染完成后，Hexo 会自动执行相对应的 `after_render` 过滤器，举例来说，我们可以通过这个功能实现 JavaScript 的压缩。

```
varrequire'uglify-js'
hexo.extend.filter.register('after_render:js'functionstr, data{  var
  return
}); 
```

## 检查文件是否可被渲染

您可以通过 `isRenderable` 或 `isRenderableSync` 两个方法检查文件路径是否可以被渲染，只有在相对应的渲染器（renderer）已注册的情况下才会返回 true。

```
hexo.render.isRenderable('layout.swig'// true
hexo.render.isRenderable('image.png'// false 
```

## 获取文件的输出扩展名

您可以通过 `getOutput` 方法取得文件路径输出后的扩展名，如果文件无法渲染，则会返回空字符串。

```
hexo.render.getOutput('layout.swig'// html
hexo.render.getOutput('image.png'// ''' 
```

# 文章

# 文章

## 新建文章

```
hexo.post.create(data, replace); 
```

| 参数 | 描述 |
| --- | --- |
| `data` | 数据 |
| `replace` | 替换现有文件 |

您可以在资料中指定文章的属性，除了以下属性之外，其他属性也会被加到 front-matter 中。

| 属性 | 描述 |
| --- | --- |
| `title` | 标题 |
| `slug` | 网址 |
| `layout` | 布局。默认为 `default_layout` 参数。 |
| `path` | 路径。默认会根据 `new_post_path` 参数创建文章路径。 |
| `date` | 日期。默认为当前时间。 |

## 发布草稿

```
hexo.post.publish(data, replace); 
```

| 参数 | 描述 |
| --- | --- |
| `data` | 资料 |
| `replace` | 替换现有文件 |

您可以在资料中指定文章的属性，除了以下的属性之外，其他属性也会被加到 front-matter 中。

| 属性 | 描述 |
| --- | --- |
| `slug` | 文件名称（必须） |
| `layout` | 布局。默认为 `default_layout` 参数。 |

## 渲染

```
hexo.post.render(source, data); 
```

| 参数 | 描述 |
| --- | --- |
| `source` | 文件的完整路径（可忽略） |
| `data` | 数据 |

资料中必须包含 `content` 属性，如果没有的话，会尝试读取原始文件。此函数的执行顺序为：

*   执行 `before_post_render` 过滤器
*   使用 Markdown 或其他渲染器渲染（根据扩展名而定）
*   使用 [Nunjucks](http://mozilla.github.io/nunjucks/) 渲染
*   执行 `after_post_render` 过滤器

# 脚手架（Scaffold）

# 脚手架（Scaffold）

## 获得脚手架

```
hexo.scaffold.get(name); 
```

## 设置脚手架

```
hexo.scaffold.set(name, content); 
```

## 移除脚手架

```
hexo.scaffold.remove(name); 
```

# 主题

# 主题

`hexo.theme` 除了继承 Box 外，还具有存储模板的功能。

## 获取模板

```
hexo.theme.getView(path); 
```

## 设置模板

```
hexo.theme.setView(path, data); 
```

## 移除模板

```
hexo.theme.removeView(path); 
```

## 模板

模板本身有两个方法可供使用：`render` 和 `renderSync`。两者功能一样，只是前者为非同步函数，而后者为同步函數，因此仅以 `render` 演示调用方法。

```
var'layout.swig'
view.render({foo: 12functionresult{  // ...
}); 
```

您可以以向 `render` 方法传入对象作为参数，`render` 方法会先使用对应的渲染引擎进行解析，并加载 辅助函数。渲染完成后，会检测布局（layout）是否存在，当 `layout` 设为 `false` 或不存在时，就会直接返回渲染结果。

# 扩展

# 扩展

# 控制台（Console）

# 控制台（Console）

控制台是 Hexo 与开发者之间沟通的桥梁。

## 概要

```
hexo.extend.console.register(name, desc, options, functionargs{  // ...
}); 
```

| 参数 | 描述 |
| --- | --- |
| `name` | 名称 |
| `desc` | 描述 |
| `options` | 选项 |

在函数中会传入 `args` 参数，此参数是使用者在终端中所传入的参数，是一个经 [Minimist](https://github.com/substack/minimist) 解析的对象。

## 选项

### 用法

控制台的操作方法，例如：

```
{usage: '[layout] <title>'
// hexo new [layout] <title> 
```

### 参数

控制台各个参数的说明，例如：

```
{  arguments
    {name: 'layout''Post layout'
    {name: 'title''Post title'
  ]} 
```

### 选项

控制台的选项，例如：

```
{  options: [    {name: '-r, --replace''Replace existing files'
  ]} 
```

### 描述

控制台更详细的说明。

## 范例

```
hexo.extend.console.register('config''Display configuration'functionargs{  console
}); 
```

# 部署器（Deployer）

# 部署器（Deployer）

部署器帮助开发者将网站快速部署到远程服务器上，避免了复杂的指令。

## 概要

```
hexo.extend.deployer.register(name, functionargs{  // ...
}); 
```

在函数中会传入 `args` 参数，该参数包含了 `_config.yml` 中的 `deploy` 参数值，以及开发者在终端中所传入的参数。

# 过滤器（Filter）

# 过滤器（Filter）

过滤器用于修改特定文件，Hexo 将这些文件依序传给过滤器，而过滤器可以针对文件进行修改，这个概念借鉴自 [WordPress](http://codex.wordpress.org/Plugin_API#Filters)。

## 概要

```
hexo.extend.filter.register(type, function{}, priority); 
```

您可以指定过滤器的优先级 `priority`，`priority` 值越低，过滤器会越早执行，默认的 `priority` 是 10。

## 执行过滤器

```
hexo.extend.filter.exec(type, data, options);hexo.extend.filter.execSync(type, data, options); 
```

| 选项 | 描述 |
| --- | --- |
| `context` | Context |
| `args` | 参数。必须为数组。 |

`data` 会作为第一个参数传入每个过滤器，而您可以在过滤器中通过返回值改变下一个过滤器中的 `data`，如果什么都没有返回的话则会保持原本的 `data`。您还可以使用 `args` 指定过滤器的其他参数。举例来说：

```
hexo.extend.filter.register('test'functiondata, arg1, arg2{  // data === 'some data'
  // arg1 === 'foo'
  // arg2 === 'bar'
    return'something'
});hexo.extend.filter.register('test'functiondata, arg1, arg2{  // data === 'something'
});hexo.extend.filter.exec('test''some data'
  args: 'foo''bar'
}); 
```

您也可以使用以下方法来执行过滤器：

```
hexo.execFilter(type, data, options);hexo.execFilterSync(type, data, options); 
```

## 移除过滤器

```
hexo.extend.filter.unregister(type, filter); 
```

## 过滤器列表

以下是 Hexo 所使用的过滤器。

### before_post_render

在文章开始渲染前执行。您可以参考 [文章渲染 以了解执行顺序。

举例来说，把标题转为小写：

```
hexo.extend.filter.register('before_post_render'functiondata{  data.title = data.title.toLowerCase();  return
}); 
```

### after_post_render

在文章渲染完成后执行。您可以参考 文章渲染 以了解执行顺序。

举例来说，把 `@username` 取代为 Twitter 的开发者链接。

```
hexo.extend.filter.register('after_post_render'functiondata{  data.content = data.content.replace(/@(\d+)/'<a href="http://twitter.com/$1">#$1</a>'
  return
}); 
```

### before_exit

在 Hexo 即将结束时执行，也就是在 `hexo.exit` 被调用后执行。

```
hexo.extend.filter.register('before_exit'function{  // ...
}); 
```

### before_generate

在生成器解析前执行。

```
hexo.extend.filter.register('before_generate'function{  // ...
}); 
```

### after_generate

在生成器解析后执行。

```
hexo.extend.filter.register('after_generate'function{  // ...
}); 
```

### template_locals

修改模板的 局部变量。

举例来说，在模板的局部变量中新增当前时间：

```
hexo.extend.filter.register('template_locals'functionlocals{  locals.now = Date
  return
}); 
```

### after_init

在 Hexo 初始化完成后执行，也就是在 `hexo.init` 执行完成后执行。

```
hexo.extend.filter.register('after_init'function{  // ...
}); 
```

### new_post_path

用来决定新建文章的路径，在建立文章时执行。

```
hexo.extend.filter.register('new_post_path'functiondata, replace{  // ...
}); 
```

### post_permalink

用来决定文章的永久链接。

```
hexo.extend.filter.register('post_permalink'functiondata{  // ...
}); 
```

### after_render

在渲染后执行，您可以参考 渲染 以了解更多信息。

### server_middleware

新增服务器的 Middleware。`app` 是一个 [Connect](https://github.com/senchalabs/connect) 实例。

举例来说，在响应头中新增 `X-Powered-By: Hexo`。

```
hexo.extend.filter.register('server_middleware'functionapp{  app.use(functionreq, res, next{    res.setHeader('X-Powered-By''Hexo'
    next();  });}); 
```

# 生成器（Generator）

# 生成器（Generator）

生成器根据处理后的原始文件建立路由。

## 概要

```
hexo.extend.generator.register(name, functionlocals{}); 
```

在函数中会传入一个 `locals` 参数，等同于 网站变量，请尽量利用此参数取得网站数据，避免直接存取资料库。

## 更新路由

```
hexo.extend.generator.register('test'functionlocals{  // Object
  return
    path: 'foo'
    data: 'foo'
  };    // Array
  return
    {path: 'foo''foo'
    {path: 'bar''bar'
  ];}); 
```

| 属性 | 描述 |
| --- | --- |
| `path` | 路径。不可包含开头的 `/`。 |
| `data` | 数据 |
| `layout` | 布局。指定用于渲染的模板，可为字符串或数组，如果省略此属性的话则会直接输出 `data`。 |

在原始文件更新时，Hexo 会执行所有生成器并重建路由，**请直接回传资料，不要直接操作路由**。

## 范例

### 归档页面

在 `archives/index.html` 建立一归档页面，把所有文章当作资料传入模板内，这个资料也就等同于模板中的 `page` 变量。

然后，设置 `layout` 属性好让 Hexo 使用主题模板来渲染，在此例中同时设定了两个布局，当 `archive` 布局不存在时，会继续尝试 `index` 布局。

```
hexo.extend.generator.register('archive'functionlocals{  return
    path: 'archives/index.html'
    data: locals.posts,    layout: ['archive''index'
  }}); 
```

### 有分页的归档页面

您可以通过 [hexo-pagination](https://github.com/hexojs/hexo-pagination) 这个方便的官方工具来轻松建立分页归档。

```
varrequire'hexo-pagination'
hexo.extend.generator.register('archive'functionlocals{  return'archives/index.html'
    perPage: 10
    layout: 'archive''index'
    data: {}  });}); 
```

### 生成所有文章

遍历 `locals.posts` 中的所有文章并生成所有文章的路由。

```
hexo.extend.generator.register('post'functionlocals{  returnfunctionpost{    return
      path: post.path,      data: post,      layout: 'post'
    };  });}); 
```

### 复制文件

这次不直接在 `data` 中返回数据而是返回一个函数，如此一来这个路由唯有在使用时才会建立 `fs.ReadStream`。

```
varrequire'hexo-fs'
hexo.extend.generator.register('asset'functionlocals{  return
    path: 'file.txt'
    data: function{      return'path/to/file.txt'
    }  };}); 
```

# 辅助函数（Helper）

# 辅助函数（Helper）

辅助函数帮助您在模板中快速插入内容，建议您把复杂的代码放在辅助函数而非模板中。

## 概要

```
hexo.extend.helper.register(name, function{}); 
```

## 范例

```
hexo.extend.helper.register('js'functionpath{  return'<script type="text/javascript" src="''"></script>'
}); 
```

```
<%- js('script.js'
// <script type="text/javascript" src="script.js"></script> 
```

# 迁移器（Migrator）

# 迁移器（Migrator）

迁移器帮助开发者从其他系统迁移到 Hexo。

## 概要

```
hexo.extend.migrator.register(name, functionargs{  // ...
}); 
```

在函数中需要传入 `args` 参数，该参数包含了开发者在终端中所传入的参数。

# 处理器（Processor）

# 处理器（Processor）

处理器用于处理 `source` 文件夹内的原始文件。

## 概要

```
hexo.extend.processor.register(rule, functionfile{}); 
```

完整说明请参考 [Box。

# 渲染引擎（Renderer）

# 渲染引擎（Renderer）

渲染引擎用于渲染内容。

## 概要

```
hexo.extend.renderer.register(name, output, functiondata, options{}, sync); 
```

| 参数 | 描述 |
| --- | --- |
| `name` | 输入的扩展名（小写，不含开头的 `.`） |
| `output` | 输出的扩展名（小写，不含开头的 `.`） |
| `sync` | 同步模式 |

渲染函数中会传入两个参数：

| 参数 | 描述 |
| --- | --- |
| `data` | 包含两个属性：文件路径 `path` 和文件内容 `text`。`path` 不一定存在。 |
| `option` | 选项 |

## 范例

### 非同步模式

```
varrequire'stylus'
// Callback
hexo.extend.renderer.register('styl''css'functiondata, options, callback{  stylus(data.text).set('filename'
});// Promise
hexo.extend.renderer.register('styl''css'functiondata, options{  returnnewPromisefunctionresolve, reject{    resolve('test'
  });}); 
```

### 同步模式

```
varrequire'ejs'
hexo.extend.renderer.register('ejs''html'functiondata, options{  options.filename = data.path;  return
}, true 
```

# 标签插件（Tag）

# 标签插件（Tag）

标签插件帮助开发者在文章中快速插入内容。

## 概要

```
hexo.extend.tag.register(name, functionargs, content{}, options); 
```

标签函数会传入两个参数：`args` 和 `content`，前者代表开发者在使用标签插件时传入的参数，而后者则是标签插件所覆盖的内容。

从 Hexo 3 开始，因为新增了非同步渲染功能，而改用 [Nunjucks](http://mozilla.github.io/nunjucks/) 作为渲染引擎，其行为可能会与过去使用的 [Swig](http://paularmstrong.github.io/swig/) 有些许差异。

## 选项

### ends

使用结束标签，此选项默认为 `false`。

### async

开启非同步模式，此选项默认为 `false`。

## 范例

### 没有结束标签

插入 Youtube 影片。

```
hexo.extend.tag.register('youtube'functionargs{  var0
  return'<div class="video-container"><iframe width="560" height="315" src="http://www.youtube.com/embed/''" frameborder="0" allowfullscreen></iframe></div>'
}); 
```

### 有结束标签

插入 pull quote。

```
hexo.extend.tag.register('pullquote'functionargs, content{  var' '
  return'<blockquote class="pullquote''">''</blockquote>'
}, {ends: true 
```

### 非同步渲染

插入文件。

```
varrequire'hexo-fs'
varrequire'path'
hexo.extend.tag.register('include_code'functionargs{  var0
  var
    returnfunctioncontent{    return'<pre><code>''</code></pre>'
  });}, {asynctrue 
```