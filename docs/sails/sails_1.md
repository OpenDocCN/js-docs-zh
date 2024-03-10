# 入门指南

# 入门教程

## 安装

使用命令行工具安装最新稳定版：

```
sudo npm -g install sails 
```

在 `Windows` 上(或者在有`Homebrew`的`Mac OS`系统上)，不需要使用`sudo`:

```
npm install -g sails 
```

## 创建`sails`新工程

创建新应用:

```
sails new testProject 
```

启动服务器:

```
cd testProject
sails lift 
```

这时，访问 `http://localhost:1337/` 会看到默认主页。

现在，可以让`Sails`做点更酷的事情了。

<docmeta value="Installation" name="displayName" class="calibre17"></docmeta>

# node.js 新手？

# [Node.js](https://soundcloud.com/marak/marak-the-node-js-rap) 新手?

好吧，让我们帮你“领上道”吧。

官网 [nodejs.org](http://nodejs.org) 的介绍是这样的：

> "Node.js 是一个构建在`谷歌 javascript 运行器`(Chrome's JavaScript runtime)上的平台， 易于构建快速、可扩展的网络应用。Node.js 使用事件驱动，非柱塞 I/O 模型，使得数据密集型实时应用运行在跨分布式设备上（更加）轻量、高效和完美。"

更简单地说，Node.js 允许我们在浏览器之外迅速有效地运行 JavaScript 代码，使得应用同一种语言开发前端和后端成为可能。

## 需要什么操作系统？

Node.js 可以安装在大部分主流的操作系统上，MacOSX，许多流行的 Linux，以及 Windows 都支持。

现在，你可以根据自己的操作系统，选择浏览下面的介绍文章：

[Mac OSX](http://sailsjs.org/get-started#?install-on-osx)

[Linux](http://sailsjs.org/get-started#?install-on-linux)

[Windows](http://sailsjs.org/get-started#?install-on-windows)

## [](http://sailsjs.org/getStarted?q=--install-on-osx-)OSX 安装

使用 [一个包](http://nodejs.org/download/):

*简单 [下载 Macintosh Installer](http://nodejs.org/download/).*

使用 [homebrew](https://github.com/mxcl/homebrew):

```
brew install node 
```

使用 [macports](http://www.macports.org/):

```
port install nodejs 
```

## [](http://sailsjs.org/getStarted?--install-on-linux-)Linux 安装

### Ubuntu, Mint

例如:

```
sudo apt-get install python-software-properties python g++ make
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs 
```

这会将当前稳定的 node.js 安装在当前稳定版的 Ubuntu.上。Quantal (12.10) 用户可能需要为`add-apt-repository`命令安装 *software-properties-common* 包，才能运行 `sudo apt-get install software-properties-common`

与包(Amateur Packet Radio Node Program)有一个名字冲突，二进制的 nodejs 已经将名字从`node`改为`nodejs`。你需要符号链接`/usr/bin/node` 到`/usr/bin/nodejs`，或者卸载 Amateur Packet Radio Node 程序，避免冲突。

### Fedora

Fedora 18 和更新版本，提供了[Node.js](https://apps.fedoraproject.org/packages/nodejs) 和 [npm](https://apps.fedoraproject.org/packages/npm)。仅仅使用您喜欢的图形包管理器，或在命令行安装即可:

```
sudo yum install npm 
```

### RHEL/CentOS/Scientific Linux 6

[Fedora Extra Packages for Enterprise Linux (EPEL)](https://fedoraproject.org/wiki/EPEL) 提供了 Node.js and npm *测试* 库。如果你还没有这么做，首先[启用 EPEL](https://fedoraproject.org/wiki/EPEL#How_can_I_use_these_extra_packages.3F)，然后运行下面的命令：

```
su -c 'yum --enablerepo=epel-testing install npm' 
```

### Arch Linux

社区库提供了 Node.js

```
pacman -S nodejs 
```

### Gentoo

官方 gentoo 仓库树里提供了 Node.js ，你需要 unmask 它。

```
# emerge -aqv --autounmask-write nodejs
# etc-update
# emerge -aqv nodejs 
```

### Debian, LMDE

对于 *Debian sid (不稳定版)*, [官方库提供了 Node.js](http://packages.debian.org/search?searchon=names&keywords=nodejs).

对于 *Debian Wheezy (最新稳定版)*, [wheezy-backports 提供了 Node.js](http://packages.debian.org/wheezy-backports/nodejs). 为了安装 [backports](http://backports.debian.org/Instructions/)，添加下面一行到 sources.list (`/etc/apt/sources.list`):

```
deb http://YOURMIRROR.debian.org/debian wheezy-backports main 
```

然后，运行：

```
apt-get update
apt-get install nodejs 
```

对于 *Debian Squeeze (旧稳定版)*，最好自己编译 (as `root`):

```
apt-get install python g++ make
mkdir ~/nodejs && cd $_
wget -N http://nodejs.org/dist/node-latest.tar.gz
tar xzvf node-latest.tar.gz && cd `ls -rd node-v*`
./configure
make install 
```

### openSUSE & SLE

[Node.js 稳定版仓库列表](https://build.opensuse.org/package/show?package=nodejs&project=devel%3Alanguages%3Anodejs)。node.js 也可在 openSUSE:Factory repository 中找到。

可用的 RPM 包: openSUSE 11.4, 12.1, Factory and Tumbleweed; SLE 11 (with SP1 and SP2 variations).

例如， 安装在 openSUSE 12.1 上:

```
sudo zypper ar http://download.opensuse.org/repositories/devel:/languages:/nodejs/openSUSE_12.1/ NodeJSBuildService
sudo zypper in nodejs nodejs-devel 
```

### FreeBSD and OpenBSD

Node.js 可通过 ports 系统使用。

```
/usr/ports/www/node 
```

开发版本也可使用 ports

```
cd /usr/ports/www/node-devel/ && make install clean 
```

或者 FreeBSD 上的包

```
pkg_add -r node-devel 
```

在 FreeBSD 上，Node 包管理并不默认与 Node.js 一起安装，但对于开发和安装以来还是需要的。

```
/usr/ports/www/npm 
```

还要注意，FreeBSD 10 与偶尔使用的构建脚本（好像是 gcc，用于 node-gyp）冲突，可以通过设置一个环境变量解决。

```
CXX=c++ 
```

## [](http://sailsjs.org/getStarted?q=--install-on-windows-)Windows 安装

使用 [一个包](http://nodejs.org/download/):

*简单 [下载 Windows 安装器](http://nodejs.org/download/)*

使用 [chocolatey](http://chocolatey.org) 安装 [Node](http://chocolatey.org/packages/nodejs):

```
cinst nodejs 
```

或者 [与 NPM 一起完全安装](http://chocolatey.org/packages/nodejs.install):

```
cinst nodejs.install 
```

## 关于 Sails.js

一旦 Node.js 安装完毕， 就可以继续 [安装 Sails](http://sailsjs.org/get-started#?getting-started-installation)。

## 更多帮助

计划赶不上变化，如果你仍然有问题，请. If you still have any issue with this, 请随时访问 node.js IRC 频道 或者 我们的 IRC 频道.

<docmeta value="New To Node?" name="displayName" class="calibre17"></docmeta>

# sails 是什么？

# Sails 是什么？

当然，`Sails`是一个`web 框架`。但退一步，这又是什么意思呢？有时，当我们提到`web`的时候，我们指的是"front-end web"(web 前端）。 我们想到的是 Web 标准的概念，像 HTML5 或 CSS3；以及框架，`Backbone`、`Angular`, 或 `jQuery`。`sails`可不是“这种”的`web`框架。 `Sails`可以与`Angular`和`Backbone`工作的很好，但绝不会使用`Sails`取代这些包。

换句话说，当我们谈论`Web 框架`的时候，我们指的是“back-end web”（服务器端）。这里提到的概念是`REST`、`HTTP`,或`WebSockets`， 以及`Java`、`Ruby`、`Node.js`等技术。一个“back-end web”框架有助于你构建 API，处理 HTML 文件成千上万的并发用户。`Sails`就是 “这种”`web 框架`。

## 约定优于配置

Sails 完成许多与其他 MVC 网站应用程序框架相同的目标，使用许多相同的方法学。这样做是有目的的。一致的方式使得参与其中的任何人开发应用程序更具可预测性且高效率的。

想像一下，开始一份新的工作，在一家公司建立 Sails 应用程序。如果任何在你团队中的人曾使用如 Zend、Laravel、CodeIgniter、Cake、Grails、Django、ASP.NET MVC 或 Rails，会觉得很熟悉 Sails。不仅如此，一般来说，他们还可以了解 Sails 工程，如何撰写他们在过去已反复实践的基本模式；无论他们的背景是 PHP、Ruby、Java、C# 或 Node.js。那么你的第二个应用程序或第三个？每当你建立新的 Sails 应用程序，你以一个健全、熟悉的样版开始，让你更有效率。在许多情况下，你甚至可以回收重复使用一些后端程序码。

> **历史**
> 
> Sails 没有发明这个概念，它[已经存在多年](https://en.wikipedia.org/wiki/Convention_over_configuration)。即使在 Ruby on Rails 那句「约定优于配置」（或称 CoC）流行之前，JavaBeans 借用了常见于 90 年代末期到 21 世纪初期，传统的 Java 网站框架极其冗长的 XML 设置到许多核心规范中。简单来说就是用简单的约定（Convention）来取代繁杂的配置（Configuration），简化开发者的工作。

## Loose Coupling

> TODO: explain why pushing towards an open standard for programming apps is important.
> 
> TODO: more specifically, give some background why small, loosely coupled modules are good.
> 
> TODO: explain how Sails core is a set of standalone, loosely coupled components (link to MODULES.md).
> 
> TODO: discuss how a Sails app is a set of standalone, loosely coupled components:
> 
> *   how each model, or controller, etc. is a node module.
> *   how policies are designed to be general-purpose and shared between apps and/or developers.
> *   how Sails strives to make adapter development as easy as possible, even for non-database integrations.
> 
> TODO: explain how Sails is designed for any part to be rip-outable, overridden, or extended (hooks, generators, adapters)
> 
> TODO: Explain how Sails can be used without any boilerplate files, just like Express, to fit an imperative programming style, or plug in as part of your existing Node / Node+Express app.
> 
> Links:
> 
> *   [Unix philosophy](http://blog.izs.me/post/48281998870/unix-philosophy-and-node-js)
> *   [Node culture](https://blog.nodejitsu.com/the-nodejs-philosophy/)

## Pragmatism

> TODO: set the stage- the purpose of any practical web framework should be to solve real-world use cases. Node, being built on JavaScript, is the most intensely pragmatic thing to hit the scene since the introduction of Java. It [will replace Java](http://readwrite.com/2013/08/09/why-javascript-will-become-the-dominant-programming-language-of-the-enterprise) [in the enterprise](http://blog.appfog.com/node-js-is-taking-over-the-enterprise-whether-you-like-it-or-not/).
> 
> TODO: explain where this fits into the Node.js ecosystem, and pay homage to the PHP community (pragmatism is the best thing PHP has going for it)
> 
> TODO: provide some examples of choices we've made w/

# 附件

# 资源（Assets）

### 概述

资源指的是在你的服务器上想让外界存取的[静态文档](http://en.wikipedia.org/wiki/Static_web_page)（js、css、图档等等）。在 Sails，这些文档都放在 [`assets/`](http://beta.sailsjs.org/#/documentation/anatomy/myApp/assets) 目录，当你启动应用程序，他们会被处理并同步到一个隐藏的暂存目录(`.tmp/public/`)。这个 `.tmp/public` 文件夹就是 Sails 实际提供的内容，大致等同于 [express](https://github.com/expressjs) 的「public」文件夹，或是其他你或许熟悉的网站服务器如 Apache 的「www」文件夹。这中间的过程允许 Sails 准备或预先编译在用户端上使用的资源，像是 LESS、CoffeeScript、SASS、spritesheets、Jade 模板等等。

### 静态中间件（Static middleware）

在幕后，Sails 使用 Express 的[静态中间件](http://www.senchalabs.org/connect/static.html)来提供你的资源。你可以在 `/config/http.js` 设置这个中间件（例如 cache 设置）。

##### `index.html`

如同大多数网页服务器，Sails 实践了 `index.html` 约定。举例来说，如果你在新的 Sails 工程建立 `assets/foo.html`，便可通过 `http://localhost:1337/foo.html` 存取。但是，如果你建立 `assets/foo/index.html`，则可通过 `http://localhost:1337/foo/index.html` 及 `http://localhost:1337/foo` 存取。

##### 优先权

重要的是需注意静态[中间件](http://stephensugden.com/middleware_guide/)是安装在 Sails 路由**之后**。所以，如果你定义了一个自定义路由，但在你的资源目录也有文档与该路径冲突，自定义路由会在到达静态中间件前拦截请求。举例来说，如果你建立 `assets/index.html` 且没有定义路由在 `config/routes.js` 文档，它会被当成你的首页。但是如果你定义一个自定义路由 `'/': 'FooController.bar'`，将优先采用此路由。

<docmeta value="Assets220313" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Assets" name="displayName" class="calibre17"></docmeta>

# 默认任务

# 默认任务（Default Tasks）

### 概述

Sails 内的 asset pipeline 是一组能增加工程一致性和效率的 Grunt 任务设置。整个前端资源工作流程可完全自定义，它提供了一些可立即使用的默认任务。Sails 可以很容易的设置新任务，以满足你的需求。

这些 Sails 默认的 Grunt 组件设置可协助你：

*   自动编译 LESS
*   自动编译 JST
*   自动编译 Coffeescript
*   自定义的资源自动注入、压缩及合并
*   建立网站公用目录
*   监视和同步文档
*   优化生产环境的资源

### 默认 Grunt 任务行为

以下是包含在 Sails 工程的 Grunt 任务及每个任务的简短说明。此外，还包含了每个任务的使用说明连结。

##### clean

> 这个 grunt 任务是用来清理 sails 工程里 `.tmp/public/` 的内容。
> 
> [使用说明](https://github.com/gruntjs/grunt-contrib-clean)

##### coffee

> 从 `assest/js/` 将 coffeeScript 文档编译成 Javascript 并放到 `.tmp/public/js/` 目录。
> 
> [使用说明](https://github.com/gruntjs/grunt-contrib-coffee)

##### concat

> 合并 javascript 和 css 并将合并后的文档放到 `.tmp/public/concat/` 目录。
> 
> [使用说明](https://github.com/gruntjs/grunt-contrib-concat)

##### copy

> **dev 任务设置** 从 sails 资源文件夹复制 coffeescript 和 less 以外的所有目录与文档到 `.tmp/public/` 目录。
> 
> **build 任务设置** 从 `.tmp/public/` 目录复制所有目录及文档到 www 目录。
> 
> [使用说明](https://github.com/gruntjs/grunt-contrib-copy)

##### cssmin

> 压缩 css 文档并放到 `.tmp/public/min/` 目录。
> 
> [使用说明](https://github.com/gruntjs/grunt-contrib-cssmin)

##### jst

> 预先将 Underscore 模板编译成 `.jst` 文档。（也就是说，它需要模板文档并将其转换成微小的 javascript 函数）。这可以加速在用户端的模板呈现，及减少频宽的消耗。
> 
> [使用说明](https://github.com/gruntjs/grunt-contrib-jst)

##### less

> 将 LESS 文档编译成 CSS。只有 `assets/styles/importer.less` 会被编译。这让你可以自行控制顺序，即在其他样式之前汇入你的相依（Dependencies）、混入（Mixins）、变数（Variables）、重置（Resets）等等。
> 
> [使用说明](https://github.com/gruntjs/grunt-contrib-less)

##### sails-linker

> 自动为 javascript 文档注入 `<script>` 标签以及为 css 文档注入 `<link>` 标签。还可以自动连接输出文档到使用 `<script>` 标签的预先编译模板。这个任务的详细说明可以在[这里](https://github.com/balderdashy/sails-generate-frontend/blob/master/docs/overview.md#a-litte-bit-more-about-sails-linking)找到，但最大的改变是*只有*当文档包含 `<!--SCRIPTS--><!--SCRIPTS END-->` 和/或 `<!--STYLES--><!--STYLES END-->` 才会做 script 和 stylesheet 注入。这些都包含在新 Sails 工程默认的 **views/layout.ejs** 文档。如果不想在工程使用连接器，只需删除这些标签。
> 
> [使用说明](https://github.com/Zolmeister/grunt-sails-linker)

##### sync

> 保持目录同步的 grunt 任务。它与 grunt-contrib-copy 非常类似，但仅会尝试复制那些真正有改变的文档。它明确的从 `assets/` 文件夹同步文档到 `.tmp/public/`，并覆盖任何已存在的文档。
> 
> [使用说明](https://github.com/tomusdrw/grunt-sync)

##### uglify

> 压缩用户端 javascript 资源。
> 
> [使用说明](https://github.com/gruntjs/grunt-contrib-uglify)

##### watch

> 当被监视的文档类型被新增、修改或删除，执行预先定义的任务。监视 `assets/` 文件夹的文档异动，并重新执行对应的任务（例如编译 less 和 jst）。这让你可以看到应用程序的资源变更，而无需重新启动 Sails 服务器。
> 
> [使用说明](https://github.com/gruntjs/grunt-contrib-watch)

<docmeta value="DefaultTasks764297" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Default Tasks" name="displayName" class="calibre17"></docmeta>

# 禁用 Grunt

# 禁用 Grunt（Disabling Grunt）

要禁用整合在 Sails 的 Grunt，只需删除 Gruntfile（和/或 `tasks/` 文件夹）。你还可以禁用 Grunt hook。只要像这样在 `.sailsrc` hooks 设置 `grunt` 属性为 `false`：

```
{
    "hooks": {
        "grunt": false
    }
} 
```

### 我可以为 SASS、Angular、用户端 Jade 模板等自定义任务吗？

是的！只需取代 `tasks/` 目录中对应的 grunt 任务，或新增一个。如同 [SASS](https://github.com/sails101/using-sass) 例子。

如果你仍然想使用 Grunt 做其他用途，但不想要任何默认的网页前端工作，只要删除工程的资源文件夹并从 `grunt/register/` 和 `grunt/config/` 文件夹移除前端相关任务。你还可以在往后的工程执行 `sails new myCoolApi --no-frontend` 来省略资源文件夹和前端相关 Grunt 任务。你也可以用社区的产生器或[建立自己的](https://github.com/balderdashy/sails-generate-generator)产生器来取代 `sails-generate-frontend` 模组。这让 `sails new` 可以建立原生 iOS 应用程序、Android 应用程序、Cordova 应用程序、SteroidsJS 应用程序等等的模板。

<docmeta value="DisablingGrunt970874" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Disabling Grunt" name="displayName" class="calibre17"></docmeta>

# 自动化任务

# 任务自动化（Task Automation）

### 概述

`tasks/` 目录包含了一系列 [Grunt 任务](http://gruntjs.com/creating-tasks)和它们的[组件设置](http://gruntjs.com/configuring-tasks)。

任务主要是用在打包前端资源（如 stylesheets、scripts 及用户端标记模板），但它们也可以用在自动化重复各种开发时的琐事，从 [browserify](https://github.com/jmreidy/grunt-browserify) 编译到[资料库迁移](https://www.npmjs.org/package/grunt-db-migrate)皆可使用。

为了方便起见，Sails 打包了一些默认任务，但随著[数以百计](http://gruntjs.com/plugins)的插件可供选择，你可以几乎毫不费力的使用任务自动完成任何事情。如果没有你需要的，你可以[撰写](http://gruntjs.com/creating-tasks)并[发布自己的 Grunt 插件](http://gruntjs.com/creating-plugins)到 [npm](http://npmjs.org)！

> 如果你以前从未使用过 [Grunt](http://gruntjs.com/)，一定要查看[新手上路](http://gruntjs.com/getting-started)指南，因为它解释了如何建立 [Gruntfile](http://gruntjs.com/sample-gruntfile) 以及安装和使用 Grunt 插件。

### Asset pipeline

Asset pipeline 是让你组织要注入到检视的资源的地方，可以在 `tasks/pipeline.js` 文档找到它。设置这些资源很简单，使用 grunt [任务文档组件设置](http://gruntjs.com/configuring-tasks#files)和[匹配模式](http://gruntjs.com/configuring-tasks#globbing-patterns)。它们被分为三个部分。

##### 要注入的 CSS 文档

这是一个 css 文档阵列，会注入到 html 的 `<link>` 标签。这些标签会放在所有检视的 `<!--STYLES--><!--STYLES END-->` 注解之间。

##### 要注入的 Javascript 文档

这是一个 Javascript 文档阵列，会注入到 html 的 `<script>` 标签。这些标签会放在所有检视的 `<!--SCRIPTS--><!--SCRIPTS END-->` 注解之间。文档会依照在阵列中的顺序被注入（也就是你应该按照文档相依关系来调整注入的顺序）。

##### 要注入的模板文档

这是一个 html 文档阵列，会编译成 jst 函数并放在一个 jst.js 文档。这些文档会注入到 `<script>` 标签，放在 html 的 `<!--TEMPLATES--><!--TEMPLATES END-->` 注解之间。

> 如果你想改变它们的话，相同的 grunt 匹配模式和任务文档组件设置也使用在一些任务组件设置文档自身。

### 任务组件设置（Task configuration）

每个已设置的任务都是一组规则，Gruntfile 会遵循此规则执行。他们位于 `tasks/config/` 目录且可完全自定义。你可以修改、忽略或取代任何一个 Grunt 任务，以满足你的需求。你也可以加入自己的 Grunt 任务，只需在此目录新增一个 `someTask.js` 文档来设置新的任务，然后用适当的父任务注册它（请查看 `grunt/register/*.js` 内的文档）。请记住，Sails 具备一套实用的默认任务，是为了让你在无需任何组件设置下执行。

##### 设置自定义任务

设置一个自定义任务到你的工程非常简单，使用 Grunt 的[设置](http://gruntjs.com/api/grunt.config)和[任务](http://gruntjs.com/api/grunt.task) APIs 允许你建立自己的任务模组。让我们实践一个建立新任务取代已存在任务的简单例子。比方说，我们希望 [Handlebars](http://handlebarsjs.com/) 模板引擎来取代默认具备的 underscore 模板引擎：

*   第一步是在终端机使用以下指令安装 handlebars 的 grunt 插件：

```
npm install grunt-contrib-handlebars --save-dev 
```

*   建立组件设置文档在 `tasks/config/handlebars.js`。这是我们要放 handlebars 设置的地方。

```javascript // tasks/config/handlebars.js // -------------------------------- // handlebar 任务组件设置。

module.exports = function(grunt) {

// 我们使用 grunt.config api 的 set 方法来设置一个对象到定义的字串。 // 在这个例子中，'handlebars' 任

# 设置

# 设置（Configuration）

### 概述

虽然 Sails 尽责的坚守[约定优于配置](http://en.wikipedia.org/wiki/Convention_over_configuration)的理念，但了解如何自定义这些方便的默认值是很重要的。对于几乎每个 Sails 的约定，允许你调整或覆盖附带的设置选项，以满足你的需求。本章节的文件完整包含了 Sails 可用的设置选项。

Sails 应用程序可以通过[程序设置](https://github.com/mikermcneil/sails-generate-new-but-like-express/blob/master/templates/app.js#L15)，通过指定[环境变数](http://en.wikipedia.org/wiki/Environment_variable)或命令行参数，通过改变区域或全局 [`.sailsrc` 文档](http://beta.sailsjs.org/#/documentation/anatomy/myApp/sailsrc.html)，或（最常见）使用约定位于工程内 [`config/`](http://beta.sailsjs.org/#/documentation/anatomy/myApp/config) 文件夹的模板设置文档。执行时期可通过 `sails` 全局变数的 `sails.config` 在应用程序使用合并后的设置。

### 标准设置文档 (`config/*`)

在默认情况下，新的 Sails 应用程序包含许多的设置文档。这些模板文档包含了一些行内注解，目的是为了提供一个快速、即时的参考，而不必来回跳转于文件与文字编辑器之间。

在多数情况下，`sails.config` 对象的顶层键（例如 `sails.config.views`）对应在应用程序内特定的设置文档（例如 `config/views.js`）；而设置可以安排在 `config/` 目录内任何你喜欢的文档中。重要的部分是设置的名称（即键），不是它从哪个文档来。

举例来说，假设你新增一个新文档，`config/foo.js`：

```
// config/foo.js
// 对象会被合并到 `sails.config.blueprints`：
module.exports.blueprints = {
  shortcuts: false
}; 
```

对于个别设置项目的详细参考资料，默认存在于该设置文档中，请参考本章节内的参考资料页面，或查看 Sails 应用程序剖析的[「`config/`」](http://beta.sailsjs.org/#/documentation/anatomy/myApp/config)取得更多的说明。

### 在你的应用程序存取 `sails.config`

`config` 对象存在于 Sails 应用程序实例（`sails`）。默认情况下，在启动时会置于[全局范围](http://beta.sailsjs.org/#/documentation/concepts/Globals)，因此存在于应用程序的任何地方。

##### 例子

```
// 这个例子检查在生产环境时 csrf 必需启动。
// 否则，抛出错误并终止应用程序。
if (sails.config.environment === 'production' && !sails.config.csrf) {
  throw new Error('STOP IMMEDIATELY ! CSRF should always be enabled in a production deployment!');
} 
```

### 自定义组件设置

Sails 能辨认顶层键下的许多不同设置、命名空间（如 `sails.config.sockets` 和 `sails.config.blueprints`）。但你也可以在你的自定义组件设置使用 `sails.config`（如`sails.config.someProprietaryAPI.secret`）。

##### 例子

```
// config/linkedin.js
module.exports.linkedin = {
  apiKey: '...',
  apiSecret: '...'
}; 
```

```
// 在你的 controller/service/model/hook/whatever:
// ...
var apiKey = sails.config.linkedin.apiKey;
var apiSecret = sails.config.linkedin.apiSecret;
// ... 
```

### 设置 `sails` 命令行界面

当谈到设置，大部分时间你会专注于管理特定应用程序的执行时期设置：连接埠、资料库连线，等等。然而，为了简化你的工作流程，减少重复性任务，执行自定义的自动化建置等，自定义 Sails 命令行界面也是很有用的。值得庆幸的是，Sails v0.11 增加了强大的新工具来做到这一点。

[`.sailsrc` 文档](http://beta.sailsjs.org/#/documentation/anatomy/myApp/sailsrc.html)与其他在 Sails 中的设置文档不同，它也可以被用于设置 Sails 命令行界面－无论是全系统、目录群组或仅当你 `cd` 到特定文件夹。这样做的主要理由是自定义用于执行 `sails generate` 和 `sails new` 的产生器

# Usingsailsrcfiles

# 使用 .sailsrc 文档（Using .sailsrc Files）

除了设置应用程序的其他方法外，从 0.10 版开始，你可以在 `.sailsrc` 文档里为指定一个或多个应用程序的设置（感谢 Dominic Tarr 的优秀 [`rc` 模组](https://github.com/dominictarr/rc)）。`rc` 文档对于设置命令行和/或套用组件设置到所有执行在你电脑上的 Sails 应用程序最有用。

当 Sails 命令行界面执行一个指令时，它会先在当前目录和你的家目录（即 `~/.sailsrc`）（任何新建立的 Sails 应用程序附带的模板 `.sailsrc` 文档）寻找 `.sailsrc` 文档（JSON 或 [.ini](http://en.wikipedia.org/wiki/INI_file) 格式）。然后将它们合并到现有的组件设置。

> 其实，Sails 会从其它几个地方寻找 `.sailsrc` 文档（遵循 [rc 约定](https://github.com/dominictarr/rc#standards)）。你可以放置 `.sailsrc` 文档到这些路径。也就是说，你最好能遵循约定，放置公用 `.sailsrc` 文档的地方是你的家目录（即 `~/.sailsrc`）。

<docmeta value="sailsrc374211" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Using `.sailsrc` Files" name="displayName" class="calibre17"></docmeta>

# 控制器

# 定制响应

# 自定义回应（Custom Responses）

### 概述

Sails v.10 允许自定义服务器回应。Sails 默认附带一些常见的回应类型。可以在工程的 `/api/responses` 目录找到它们。只需编辑对应的 .js 文档，就可以自定义。

作为一个简单的例子，思考以下的控制器动作：

```
foo: function(req, res) {
   if (!req.param('id')) {
     res.status(400);
     res.view('400', {message: 'Sorry, you need to tell us the ID of the FOO you want!'});
   }
   ...
} 
```

这个程序码通过发送一个 400 错误状态及简短问题描述来处理错误请求。然而，这个程序码有几个缺点，主要是：

*   它不是*标准化*的：该代码是特定于此情况，我们必须在任何地方努力保持相同的格式
*   它不是*被分离*的：当我们想要在其他地方使用类似的方法，就需要复制／贴上程序码
*   它不是*内容协商*的：如果用户端期待一个 JSON 回应，那别指望了

现在，思考一下这个修改：

```
foo: function(req, res) {
   if (!req.param('id')) {
     res.badRequest('Sorry, you need to tell us the ID of the FOO you want!');
   }
   ...
} 
```

这种方法具有许多优点：

*   错误被标准化
*   有考虑到生产环境与开发环境的日志记录
*   错误代码是一致的
*   有考虑到内容协商（JSON 与 HTML）
*   可在适当的共用回应文档快速的调整 API

### 回应方法和文档（Responses methods and files）

任何储存在 `/api/responses` 文件夹的 `.js` 脚本可通过在控制器内呼叫 `res.[responseName]` 来执行。例如，可以通过呼叫 `res.serverError(errors)` 来执行 `/api/responses/serverError.js`。在回应脚本内可以通过 `this.req` 和 `this.res` 取得请求及回应对象；这让实际的回应方法可以取得任意参数。（如 `serverError` 的 `errors` 参数）。

### 默认回应

以下的回应已绑定在所有新的 Sails 应用程序的 `/api/responses` 文件夹内。当用户端期望收到 JSON，会回应一个包含了 HTTP 状态代码的 `status` 键及任何错误相关资讯的标准化 JSON 对象。

#### res.serverError(errors)

这个回应会将错误标准化为适当、可读取的 `Error` 对象。 `errors` 可以是一个或多个字串或 `Error` 对象。它会记录所有错误到 Sails 记录器（通常是终端机），并当用户端期望收到 HTML 时回应 `views/500.*` 检视文档，或当用户端期望收到 JSON 时回应一个 JSON 对象。在开发模式下，错误清单会包含在回应中。在生产环境下，实际的错误会受到抑制。

#### res.badRequest(validationErrors, redirectTo)

对于期望收到 JSON 的请求者，这个回应包含了 400 状态码及被作为 `validationErrors` 所传送的任何相关资料。

对于传统的（非 AJAX）网页表单，当使用者提交无效的表单资料，这个中间件遵循了最佳做法：

*   首先，一个暂存变数可能被填入了一个字串或语义验证错误对象。
*   然后，将使用者重新导向回 `redirectTo`，即发出错误请求的来源 URL。
*   还有，控制器和／或检视可能使用暂存变数 `errors` 来显示讯息或突显无效的 HTML 表单栏位。

#### res.notFound()

当请求者期望收到 JSON，这个回应会发送 404 状态码及一个 `{status: 404}` 对象。

否则，将发送位于 `myApp/views/404.*` 内的检视。若找不到检视，那么便发送 JSON 回应。

#### res.forbidden(message)

当请求者期望收到 JSON，这个回应会发送 403 状态码及 `message` 的内容。

否则，将发送位于 `myApp/views/403.*` 内的检视。若找不到检视，那么便发送 JSON 回应。

### 自定义回应

要加入你自己的自定义回应方法，只需新增与方法名称相同的文档到 `/api/responses`。该文档应该导出函数，可以附带任何你喜欢的参数。

``` /**

*   api/responses/myResponse.js *
*   This will be available in controllers as res.myResponse('foo'); */

module.exports = function(message) {

var

# 部署

# 部署（Deployment）

### 概述

#### 在部署之前

在你启动任何网页应用程序前，你应该问自己几个问题：

*   你预期的流量为何？
*   你的合约是否要求满足任何正常执行时间保证，如服务层级协议（SLA）？
*   哪种前端应用程序会触及你的网页应用程序？
    *   Android 应用程序
    *   iOS 应用程序
    *   桌面版网页浏览器
    *   行动版网页浏览器（平板电脑、电话、iPad mini？）
    *   电视、手表、烤面包机…？
*   以及它们会要求什么东西？
    *   JSON？
    *   HTML？
    *   XML？
*   你会利用 Socket.io 的即时发布订阅功能？
    *   例如聊天、即时分析、应用程序内通知／讯息
*   你是如何追踪崩溃与错误？
    *   看看 Sails 的日志设置

#### 部署在单一服务器

Node.js 非常快速。对于许多应用程序，在一开始一台服务器就足够处理预期的流量。

##### 设置

*   所有生产环境设置都储存在 `config/env/production.js`
*   设置应用程序执行于连接埠 80（如果不是在如 nginx 之类的代理之后）。如果你使用的是 nginx，一定要对其设置中继 WebSocket 到应用程序。你可以在 nginx 文件 [WebSocket proxying](http://nginx.org/en/docs/http/websocket.html) 找到指南。
*   设置「正式」环境，让所有的 css/js 被打包，且内部服务器被切换到适当的环境（需要[连接器](https://github.com/balderdashy/sails-wiki/blob/0.9/assets.md)）。
*   务必确认资料库已设置在正式服务器。更重要的一点是，如果你使用的是关联式资料库如 MySQL，当执行于生产环境时， Sails 会设置所有的模型为 `migrate:safe`，这代表启动应用程序时不会进行自动移转。你可以用以下方法设置资料库：
    *   在服务器上建立资料库，使用正式服务器作为资料库，然后在本地使用 `migrate:alter` 设置执行 Sails 应用程序。这样就自动设置好了。
    *   如果你无法远端连线服务器，你可以倒出在本地端的结构，并将其汇入到资料库服务器。
*   启用 CSRF 来保护 POST、PUT 及 DELETE 请求
*   启用 SSL
*   如果你使用 SOCKETS：
    *   设置 `config/sockets.js` 并使用 socket.io 的[生产环境建议设置](https://github.com/LearnBoost/Socket.IO/wiki/Configuring-Socket.IO#recommended-production-settings)
        *   例如启用 `flashsocket` 传输

##### 部署

在生产环境中，你会想要使用 forever 或 PM2 来取代 `sails lift`，以确保即使应用程序崩溃了也会继续运作。

*   安装 forever：`sudo npm install -g forever`
    *   更多关于 forever 的资讯：[`github.com/nodejitsu/forever`](https://github.com/nodejitsu/forever)
*   或安装 PM2：`sudo npm install pm2 -g --unsafe-perm`
    *   更多关于 PM2 的资讯：[`github.com/Unitech/pm2`](https://github.com/Unitech/pm2)
*   从你的应用程序目录，使用 `forever start app.js --prod` 或 `pm2 start app.js -x -- --prod` 启动服务器
    *   这和 `sails lift --prod` 所做的事相同，但是当服务器崩溃时，它会自动重新启动。

<docmeta value="Deployment402941" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Deployment" name="displayName" class="calibre17"></docmeta>

# FAQ

# 常见问题（FAQ）

##### 我可以使用环境变数吗？

你可以在 Sails 使用环境变数设置 `port` 和 `environment`。 `NODE_ENV=production sails lift` `PORT=443 sails lift`

##### 在哪边放置我的生产环境资料库凭证（credentials）或其它设置？

对于其它部署／特定机器的设置，也就是任何形式的凭证，你应该使用 `config/local.js`。 它默认包含在 `.gitignore` 文档，这样你就不会无意中提交凭证到程序码储存库。

**config/local.js**

```
// Local configuration
// 
// Included in the .gitignore by default,
// this is where you include configuration overrides for your local system
// or for a production deployment.
//
// For example, to use port 80 on the local machine, override the `port` config
module.exports = {
    port: 80,
    environment: 'production',
    adapters: {
        mysql: {
            user: 'root',
            password: '12345'
        }
    }
} 
```

##### 如何让应用程序运作在服务器上？

你的 Node.js 实例已正常运作吗？在第一次的时候，当你有一个 IP 位址，便可以 ssh 连线到它，执行 `sudo npm install -g forever` 来安装 Sails 和 forever。

然后，`git clone` 你的工程（或 `scp` 到服务器，如果它不在 git 储存库中）到服务器并 `cd` 进入，接著 `forever start app.js`。

### 效能基准

Sails 的效能可与你所期望的标准 Node.js/Express 应用程序相比。换句话说，就是「快」！我们在 Sails 和 Waterline 做了一些优化，但本质上，我们的重点是不要把已经非常快的东西搞糟了。最重要的，我们要感谢 @ry、@visionmedia、@isaacs、#v8、@joyent 和在 Node.js 核心团队的其他成员。

*   [`serdardogruyol.com/?p=111`](http://serdardogruyol.com/?p=111)

<docmeta value="FAQ475097" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="FAQ" name="displayName" class="calibre17"></docmeta>

# Hosting

# 托管（Hosting）

以下是不完整的 Sails.js 托管服务供应商清单。

##### 部署到 Modulus？

*   [`blog.modulus.io/sails-js`](http://blog.modulus.io/sails-js)

##### 部署到 NodeJitsu？

要部署到 NodeJitsu，你需要稍微修改设置文档： 在应用程序文件夹开启 `config/local.js`。你需要加入以下几行到此设置文档。

```
// Port this Sails application will live on
port: 80,
host: 'subdomain.jit.su', 
```

`host:` 不是默认建立的属性。你需要加入这个属性。当执行 `jitsu deploy` 时，Nodejitsu 会询问你的 `subdomain`

*   [`blog.nodejitsu.com/keep-a-nodejs-server-up-with-forever/`](https://blog.nodejitsu.com/keep-a-nodejs-server-up-with-forever/)
*   [`github.com/balderdashy/sails/issues/455`](https://github.com/balderdashy/sails/issues/455)

##### 部署到 OpenShift？

要部署到 OpenShift，你需要稍微修改设置文档： 在应用程序文件夹开启 `config/local.js`。你需要加入以下几行到此设置文档。

```
port: process.env.OPENSHIFT_NODEJS_PORT,
host: process.env.OPENSHIFT_NODEJS_IP, 
```

##### 使用 DigitalOcean？

*   [`www.digitalocean.com/community/articles/how-to-create-an-node-js-app-using-sails-js-on-an-ubuntu-vps`](https://www.digitalocean.com/community/articles/how-to-create-an-node-js-app-using-sails-js-on-an-ubuntu-vps)
*   [`www.digitalocean.com/community/articles/how-to-use-pm2-to-setup-a-node-js-production-environment-on-an-ubuntu-vps`](https://www.digitalocean.com/community/articles/how-to-use-pm2-to-setup-a-node-js-production-environment-on-an-ubuntu-vps)
*   [`www.digitalocean.com/community/articles/how-to-host-multiple-node-js-applications-on-a-single-vps-with-nginx-forever-and-crontab`](https://www.digitalocean.com/community/articles/how-to-host-multiple-node-js-applications-on-a-single-vps-with-nginx-forever-and-crontab)

##### 部署到 Heroku？

*   [SailsCasts：Deploying a Sails App to Heroku](http://irlnathan.github.io/sailscasts/blog/2013/11/05/building-a-sails-application-ep26-deploying-a-sails-app-to-heroku/)
*   [`groups.google.com/forum/#!topic/sailsjs/vgqJFr7maSY`](https://groups.google.com/forum/#!topic/sailsjs/vgqJFr7maSY)
*   [`github.com/chadn/heroku-sails`](https://github.com/chadn/heroku-sails)
*   [`dennisrongo.com/deploying-sails-js-to-heroku/#.UxQKPfSwI9w`](http://dennisrongo.com/deploying-sails-js-to-heroku/#.UxQKPfSwI9w)
*   [`stackoverflow.com/a/20184907/486547`](http://stackoverflow.com/a/20184907/486547)

##### 部署到 AWS？

*   [`blog.grio.com/2014/01/your-own-mini-heroku-on-aws.html`](http://blog.grio.com/2014/01/your-own-mini-heroku-on-aws.html)
*   [`serverfault.com/questions/531560/creating-an-sails-js-application-on-aws-ami-instance`](http://serverfault.com/questions/531560/creating-an-sails-js-application-on-aws-ami-instance)
*   [`bussing-dharaharsh.blogspot.com/2013/08/creating-sailsjs-application-on-aws-ami.html`](http://bussing-dharaharsh.blogspot.com/2013/08/creating-sailsjs-application-on-aws-ami.html)
*   [`cloud.dzone.com/articles/how-deploy-nodejs-apps-aws-mac`](http://cloud.dzone.com/articles/how-deploy-nodejs-apps-aws-mac)

##### 使用 PM2？

*   [`devo.ps/blog/2013/06/26/goodbye-node-forever-hello-pm2.html`](http://devo.ps/blog/2013/06/26/goodbye-node-forever-hello-pm2.html)

##### 部署到 CloudControl？

*   [`www.cloudcontrol.com/dev-center/Guides/NodeJS/Sailsjs`](https://www.cloudcontrol.com/dev-center/Guides/NodeJS/Sailsjs)

##### 取得专业协助

这些日子以来，拥有一定技术的情况下，部署强大的应用程序变得越来越简单。尽管如此，你不一定有时间来自己处理这些事情。 Sails.js 是由我的公司维护，[Balderdash](http://balderdash.co)，一间在美国德州奥斯丁的 Node.js 顾问公司。如果你的公司需要专业协助，我们很乐意提供帮助。部署不是很困难，而且在大多情况下，它不应该超过几个小时。

<docmeta value="Hosting276234" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Hosting" name="displayName" class="calibre17"></docmeta>

# Scaling

# 扩充（Scaling）

如果你预料到会有大流量到应用程序（或者更好的是，你已经拥有大流量！），你要建立一个可扩充的架构，让应用程序可以随著越来越多人使用而进行扩充。

### 效能基准（Benchmarks）

在大多数情况下，Sails 效能与任何 Connect、Express 或 Socket.io 应用程序相同。这已在几个不同的场合下被证实，最近一次是在[这里](http://serdardogruyol.com/?p=111)。如果你有自己的效能基准想和大家分享，请在 Github 发送 pull request 到本页面。

### 例子架构

```
Sails.js 服务器
　　　　　                ....                 
　　　　　       /  Sails.js 服务器  \      /  资料库（如 Mongo、Postgres 等）
负载平衡器  <-->    Sails.js 服务器    <-->    Socket 储存区（Redis）
　　　　　       \  Sails.js 服务器  /      \  会话（Session）储存区（Redis）
　　　　　                ....                 
　　　　　          Sails.js 服务器 
```

### 设置应用程序的丛集部署

*   确保模型所使用的资料库（如 MySQL、Postgres、Mongo）具有可扩充性（如分片丛集）
*   设置应用程序使用共享的会话（Session）储存区
    *   内建支持 redis（查看 `config/session.js` 内的 `adapter` 选项）
*   如果你使用 SOCKETS：
    *   设置应用程序使用共享的 socket 储存区
    *   内建支持 redis（查看 `config/sockets.js` 内的 `adapter` 选项）
    *   注意：如果你不想设置 socket 储存区，这种状况下可行的解决方案是在负载平衡器使用黏性会话（sticky sessions）。
*   确保应用程序可能会使用的其他相依功能没有依赖于共享记忆体。

### 部署 Sails 丛集到多台服务器

*   在负载平衡器之后部署多个实例（又称服务器执行应用程序的副本）
    *   在每个实例使用 `forever` 启动 Sails
    *   更多关于负载平衡器的资讯：[`en.wikipedia.org/wiki/Load_balancing_(computing`](http://en.wikipedia.org/wiki/Load_balancing_(computing))
*   设置负载平衡器终止 SSL 请求
    *   因为传输已经被解密，你不需要在 Sails 使用 SSL 设置

<docmeta value="Scaling291270" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Scaling" name="displayName" class="calibre17"></docmeta>

# 文件上传

# 文档上传（File Uploads）

> TODO: Normalize/expand this section

### 例子

#### 产生一个 `api`

首先，我们需要替 serving/storing 产生一个新的 `api` 文档。用 sails 命令行工具执行此动作。

```
 dude@littleDude:~/node/myApp$ sails generate api file

debug: Generated a new controller `file` at api/controllers/FileController.js!
debug: Generated a new model `File` at api/models/File.js!

info: REST API generated @ http://localhost:1337/file
info: and will be available the next time you run `sails lift`.

dude@littleDude:~/node/myApp$ 
```

#### 撰写控制器动作

让我们建立一个 `index` 动作来开始文档上传及 `upload` 动作来接收文档。

```
 // myApp/api/controllers/FileController.js

module.exports = {

  index: function (req,res){

    res.writeHead(200, {'content-type': 'text/html'});
    res.end(
    '<form action="http://localhost:1337/file/upload" enctype="multipart/form-data" method="post">'+
    '<input type="text" name="title"><br>'+
    '<input type="file" name="avatar" multiple="multiple"><br>'+
    '<input type="submit" value="Upload">'+
    '</form>'
    )
  },
  upload: function  (req, res) {
    req.file('avatar').upload(function (err, files) {
      if (err)
        return res.serverError(err);

      return res.json({
        message: files.length + ' file(s) uploaded successfully!',
        files: files
      });
    });
  }

}; 
```

#### 它们去哪了？

使用默认的 `receiver`，上传的文档会在 `myApp/.tmp/uploads/` 目录。你可以在 `upload` 动作内做你想做的任何事情。

#### 上传到自定义文件夹

在上面的例子中，我们可以将文档上传到 .tmp/uploads。那么我们该如何设置为自定义文件夹，例如 `assets/images`。我们可以通过增加选项到上传功能来实现这一目标，如下所示：

```
 var uploadPath = './assets/images';
  uploadFile.upload({ dirname: uploadPath },function onUploadComplete (err, files) {             

      if (err) 
        return res.serverError(err);

      return res.json({
        message: files.length + ' file(s) uploaded successfully!',
        path:uploadPath
        file:files
      });
  }); 
```

> 请查看 [Skipper 文件](https://github.com/balderdashy/skipper)取得更多资讯及其他可用的 `receivers` 清单！

<docmeta value="fileuploads72947" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="File Uploads" name="displayName" class="calibre17"></docmeta>

# 全局变量

# 全局变数（Globals）

### 概述

为了方便起见，Sails 公开了一些全局变数。默认情况下，应用程序的[模型](http://beta.sailsjs.org/#/documentation/reference/Models)、[服务](http://beta.sailsjs.org/#/documentation/reference/Services)，和全局 `sails` 对象都存在于全局范围；这代表你可以在后端程序码的任何地方通过名称参考使用它们（只要 Sails [已经载入](https://github.com/balderdashy/sails/tree/master/lib/app)）。

在 Sails 核心没有什么东西是依赖于这些全局变数，每个公开的全局变数也可以在 `sails.config.globals` 内禁用（通常设置在 `config/globals.js`）。

### 应用程序对象（`sails`）

在大多数情况下，你会想保留 `sails` 对象的全局存取，它使你的程序码更加干净。但是，如果你*确实*需要禁用*所有*全局变数，包含 `sails`，你可以从请求对象（`req`）存取 `sails`。

### 模型和服务

应用程序的[模型](http://beta.sailsjs.org/#/documentation/reference/Models)和[服务](http://beta.sailsjs.org/#/documentation/reference/Services)被通过它们的 `globalId` 公开为全局变数。例如，定义在 `api/models/Foo.js` 文档的模型可以通过 `Foo` 在全局存取，而定义在 `api/services/Baz.js` 的服务则可通过 `Baz` 存取。

### Async（`async`）和 Lodash（`_`）

Sails 也公开 `_` 为 [lodash](http://lodash.com) 的实例，以及 `async` 为 [async](https://github.com/caolan/async) 的实例。默认已提供这些常用的套件，这样你就不必在每个新工程 `npm install` 它们。如同 sails 的其他全局变数，它们可以被禁用。

### 禁用全局变数

Sails 通过检查 [`sails.config.globals`](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.globals.html) 来决定要公开哪个全局变数，通常设置在 [`config/globals.js`](http://beta.sailsjs.org/#/documentation/anatomy/myApp/config/globals.js.html)。

要禁用所有全局变数，只需将组件设置为 `false`：

```
// config/globals.js
module.exports.globals = false; 
```

要禁用*一些*全局变数，指定一个对象来代替，例如：

```
// config/globals.js
module.exports.globals = {
  _: false,
  async: false,
  models: false,
  services: false
}; 
```

### 注意事项

> *   请记住，在 sails 被载*入前*，没有一个全局变数，包含 `sails`，可以被存取。换句话说，你不能使用 `sails.models.user` 或 `User` 功能（因为 `sails` 还没载入完成。）

<docmeta value="Globals668238" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Globals" name="displayName" class="calibre17"></docmeta>

# 国际化

# 国际化（Internationalization）

### 概述

如果你的应用程序会触及从世界各地而来的人或系统，国际化（i18n）和本地化（l10n）会是你国际化策略重要的一部分。Sails 提供内建支持，用于侦测用户语言偏好设置和翻译静态单字／句子，这要归功于 [i18n-node](https://github.com/mashpie/i18n-node)（[npm](https://www.npmjs.org/package/i18n)）。

### 用法

在检视内：

```
 #  <%= __('Hello')="" %=""> 

#  <%= __('Hello="" %s,="" how="" are="" you="" today?',="" 'Mike')="" %=""> 

 <%= i18n('That\'s="" right--="" you="" can="" use="" either="" i18n()="" or="" __()')="" %=""> 
```

在控制器或政策内：

```
req.__('Hello'); // => Hola
req.__('Hello %s', 'Marcus'); // => Hola Marcus
req.__('Hello {{name}}', { name: 'Marcus' }); // => Hola Marcus 
```

或者，你已经知道语系 ID，你可以在应用程序内的任何地方使用 `sails.__` 翻译：

```
sails.__({
  phrase: 'Hello',
  locale: 'es'
});
// => 'Hola!' 
```

### 语系

i18n 挂勾（hook）会从工程的「locales」目录（默认是 `config/locales`）读取 JSON 格式翻译文档。每个文档对应一个 Sails 后端所支持的[语系](http://en.wikipedia.org/wiki/Locale)（通常是语言）。

这些文档包含特定的语系字串（为 JSON 键值对），你可以使用在检视、控制器等地方。

这里有一个语系例子文档（`config/locales/es.json`）：

```
{
    "Hello!": "Hola!",
    "Hello %s, how are you today?": "¿Hola %s, como estas?",
} 
```

请注意，语系档内的键（例如 "Hello %s, how are you today?"）有**区分大小写**且需要精准匹配。这里有几个不同思想流派的最佳翻译，要选择哪个翻译取决于未来最常会由谁编辑语系档与 HTML。特别是如果你会手动编辑，将键的名称全部小写会最提供最佳的可维护性。

例如，这里有另一个翻译在 `config/locales/es.json`：

```
{
    "hello": "Hola!",
    "hello-how-are-you-today": "Hola %s, ¿cómo estás?",
} 
```

以及这里 `config/locales/en.json`：

```
{
    "hello": "Hello!",
    "hello-how-are-you-today": "Hello, how are you today?",
} 
```

### 侦测和／或覆写请求的所需语系

使用新的语系代码呼叫 [`req.setLocale()`](https://github.com/mashpie/i18n-node#setlocale) 来覆写请求的自动侦测语言／本地化偏好设置：

```
// 强制让请求使用德文：
req.setLocale('de');
//（这会使用在 `config/locales/de.json` 的字串来翻译） 
```

默认情况下，node-i18n 会通过检查请求的 Language 标头来侦测所需的语言。Language 标头是设置在用户的浏览器，且它们大多是正确的，你可能需要灵活覆写所侦测到的语系并提供翻译。

例如，如果你的应用程序允许使用者选择偏好语言，你可能会建立一个[政策](http://beta.sailsjs.org/#/documentation/concepts/Policies)用来检查使用者会话（Session）内的自定义语言，如果存在的话，设置相应语系以便在后续的政策、控制器动作和检视使用：

```
// api/policies/localize.js
module.exports = function(req, res, next) {
  req.setLocale(req.session.languagePreference);
  next();
}; 
```

<!--

Alternatively, here's another extended example: (todo: at the very least pull this into a sep

# 记录日志

# 日志（Logging）

### 概述

Sails 内建一个名为 [`captains-log`](https://github.com/balderdashy/captains-log) 的简单日志记录器。它的用法与 Node 的 [`console.log`](http://nodejs.org/api/stdio.html) 非常类似，但有一些额外的功能；即支持在终端机输出多种含前缀字和颜色的日志等级。

### 组件设置

Sails 日志记录器的设置在 [`sails.config.log`](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.log.html)，照约定默认对应 Sails 工程的设置文档（[`config/log.js`](http://beta.sailsjs.org/#/documentation/anatomy/myApp/config/log.js.html)）。

当设置了一个日志输出等级，Sails 会在相同或高于目前设置等级时输出日志讯息。这个日志等级已标准化，且适用于从 socket.io、Waterline 及其它相依功能产生输出。日志等级和相应的优先权分级结构总结为以下图表：

| 优先权 | 等级 | 可见的日志 |
| --- | --- | --- |
| 0 | silent | 无 |
| 1 | error | `.error()` |
| 2 | warn | `.warn()`, `.error()` |
| 3 | debug | `.debug()`, `.warn()`, `.error()` |
| 4 | info | `.info()`, `.debug()`, `.warn()`, `.error()` |
| 5 | verbose | `.verbose()`, `.info()`, `.debug()`, `.warn()`, `.error()` |
| 6 | silly | `.silly()`, `.verbose()`, `.info()`, `.debug()`, `.warn()`, `.error()` |

#### 注意事项

*   默认的日志等级是「info」。当你设置应用程序的日志等级为「info」，Sails 会记录关于服务器／应用程序状态的有限资讯。
*   当日志等级设置为「silly」，Sails 会记录已被绑定的路由、其它详细的框架生命周期资讯、诊断和实践细节等内部资讯。
*   当日志等级设置为「verbose」，Sails 会记录 Grunt 的输出，以及更详细的路由、模型、挂勾（hook）等被载入的资讯。

<docmeta value="Logging277763" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Logging" name="displayName" class="calibre17"></docmeta>

# sails.log

# sails.log()

### 概述

下列方法接受以逗点分隔的参数，没有数量与资料型态限制。如同 `console.log`，作为参数传入 Sails 日志记录器的资料会使用 Node 的 [`util.inspect()`](http://nodejs.org/api/util.html#util_util_inspect_object_options) 自动美化，以方便阅读。因此，适用于标准 Node.js 约定，也就是说，如果你使用 `inspect()` 方法记录一个对象，它会自动执行并返回将被写入到终端机的字串。相同的，对象、日期、阵列和大多数其它资料型态会使用 `util.inspect()` 内建的逻辑来美化（例如，你会看到 `{ pet: { name: 'Hamlet' } }` 而不是 `[object Object]`。）

### `sails.log()`

默认的日志功能，会将「debug」等级的日志输出到 `stderr`。

```
sails.log('hello');
// -> debug: hello. 
```

### `sails.log.error()`

将「error」等级的日志输出到 `stderr`。

```
sails.log.error('Unexpected error occurred.');
// -> error: Unexpected error occurred. 
```

### `sails.log.warn()`

将「warn」等级的日志输出到 `stderr`。

```
sails.log.warn('File upload quota exceeded for user','request aborted.');
// -> warn: File upload quota exceeded for user- request aborted. 
```

### `sails.log.debug()`

*`sails.log()` 的别名*

### `sails.log.info()`

将「info」等级的日志输出到 `stderr`。

```
sails.log.info('A new user (', 'mike@foobar.com', ') just signed up!');
// -> info: A new user ( mike@foobar.com ) just signed up! 
```

### `sails.log.verbose()`

将「verbose」等级的日志输出到 `stderr`。 可用于截取应用程序的详细资讯，你可能只会在少数情况下使用。

```
sails.log.verbose('A user initiated an account transfer...')
// -> verbose: A user initiated an account transfer... 
```

### `sails.log.silly()`

将「silly」等级的日志输出到 `stderr`。 可用于截取应用程序的完整资讯，你可能只会在少数情况下使用。

```
sails.log.silly('A user probably clicked on something..?');
// -> silly: A user probably clicked on something..? 
```

<docmeta value="sailslog321347" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.log()" name="displayName" class="calibre17"></docmeta>

# 中间件

# ORM

# Waterline: SQL/noSQL Data Mapper (ORM/ODM)

Sails comes installed with a powerful [ORM/ODM](http://stackoverflow.com/questions/12261866/what-is-the-difference-between-an-orm-and-an-odm) called [Waterline](https://github.com/balderdashy/waterline), a datastore-agnostic tool that dramatically simplifies interaction with one or more [databases](http://www.cs.umb.edu/cs630/hd1.pdf). It provides an abstraction layer on top of the underlying database, allowing you to easily query and manipulate your data *without* writing vendor-specific integration code.

### Database Agnosticism

In schemaful databases like Postgres, Oracle, and MySQL, models are represented by tables. In MongoDB, they're represented by Mongo "collections". In Redis, they're represented using key/value pairs. Each database has its own distinct query dialect, and in some cases even requires installing and compiling a specific native module to connect to the server. This involves a fair amount of overhead, and garners an unsettling level of [vendor lock-in](http://stackoverflow.com/questions/29868/how-important-is-it-to-choose-and-stick-to-a-technology-stack) to a specific database; e.g. if your app uses a bunch of SQL queries, it will be very hard to switch to Mongo later, or Redis, and vice versa.

Waterline query syntax floats above all that, focusing on business logic like creating new records, fetching/searching existing records, updating records, or destroying records. No matter what database you're contacting, the usage is *exactly the same*. Furthermore, Waterline allows you to [`.populate()`](http://sailsjs.org/#/documentation/reference/waterline/queries/populate.html) associations between models, *even if* the data for each model lives in a different database. That means you can switch your app's models from Mongo, to Postgres, to MySQL, to Redis, and back again - without changing any code. For the times when you need low-level, database-specific functionality, Waterline provides a query interface that allows you to talk directly to your models' underlying database driver (see [.query()](http://beta.sailsjs.org/#/documentation/reference/waterline/models/query.html) and [.native()](http://beta.sailsjs.org/#/documentation/reference/waterline/models/native.html).)

### Scenario

Let's imagine you're building an e-commerce website, with an accompanying mobile app. Users browse products by category or search for products by keyword, then they buy them. That's it! Some parts of your app are quite ordinary; you have an API-driven flow for logging in, signing up, order/payment processing, resetting passwords, etc. However, you know there are a few mundane features lurking in your roadmap that will likely become more involved. Sure enough:

##### Flexibility

*You ask the business what database they would like to use:*

> "Datab... what? Let's not be hasty, wouldn't want to make the wrong choice. I'll get ops/IT on it. Go ahead and get started though."

The traditional methodology of choosing one single database for a web application/API is actually prohibitive for many production use cases. Oftentimes the application needs to maintain compatibility with one or more existing data sets, or it is necessary to use a few different types of databases for performance reasons.

Since Sails uses `sails-disk` by default, you can start building your app with zero configuration, using a local temporary file as storage. When you're ready to switch to the real thing (and when everyone knows what that even is), just change your app's connection configuration.

##### Compatibility

*The product owner/stakeholder walks up to you and says:*

> "Oh hey by the way, the products actually already live in our point of sale system. It's some ERP thing I guess, something like "DB2"? Anyways, I'm sure you'll figure it out- sounds easy right?"

Many enterprise applications must integrate with an existing database. If you're lucky, a one-time data migration may be all that's necessary, but more commonly, the existing dataset is still b

# Associations

# 关联（Associations）

使用 Sails 和 Waterline，你可以跨多个资料储存区来关联模型。这代表，即使你的使用者储存在 [PostgreSQL](http://www.postgresql.org/)，而他们的相片储存在 [MongoDB](http://www.mongodb.com/)，你可以与资料进行互动，就好像他们储存在相同的资料库中。你也可以使用相同桥接器跨越不同[连线](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.connections.html)（即资料储存区／资料库）的关联。举个能派上用场的例子，你的应用程序需要从公司的资料中心的 [MySQL](http://www.mysql.com/) 资料库存取／更新旧的食谱资料，但也要从云端的全新 MySQL 资料库存取材料资料。

<docmeta value="Associations913185" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Associations" name="displayName" class="calibre17"></docmeta>

# Dominance

# Manyto Many

# 多对多（Many-to-Many）

### 概述

多对多关联表示一个模型可以关联到许多其他模型，反之亦然。 因为两个模型都可以有许多关联模型，将需要建立一个新连接资料表来追踪这些关联。

Waterline 会看著你的模型，当它找到两个模型都有 collection 属性指向彼此时，会自动为你建立连接资料表。

因为你可能想要一个模型有多个多对多关联到另一个模型，`collection` 属性必需要有一个 `via` 键。这说明了哪一边的关联 `modal` 属性会用来提供记录。

使用 `User` 和 `Pet` 例子让我们来看看如何建立「一个 `User` 可能有很多 `Pet` 记录，和 `Pet` 可能有多个主人」的架构。

### 多对多例子

在这个例子中，我们将由 users 阵列和 pets 阵列开始。我们将建立资料到阵列的每个元素，然后关联所有的 `Pets` 与所有的 `Users`。如果一切运作正常，我们应该能够查询任何 `User`，看到他们「拥有」所有的 `Pets`。此外，我们应该能够查询任何 `Pet`，看到它被所有 `User` 拥有。

`myApp/api/models/pet.js`

```
 module.exports = {

  attributes: {
    name:'STRING',
    color:'STRING',

    // 加入一个参考到 User
    owners: {
      collection: 'user',
      via: 'pets',
      dominant:true
    }
  }
} 
```

`myApp/api/models/user.js`

```
 module.exports = {

  attributes: {
    name:'STRING',
    age:'INTEGER',

    // 加入一个参考到 Pet
    pets:{
      collection: 'pet',
      via: 'owners'
    }
  }

} 
```

`myApp/config/bootstrap.js`

```
 module.exports.bootstrap = function (cb) {

// 在建立 users 之后，我们会在这储存他们来关联 pets
var storeUsers = []; 

var users = [{name:'Mike',age:'16'},{name:'Cody',age:'25'},{name:'Gabe',age:'107'}];
var ponys = [{ name: 'Pinkie Pie', color: 'pink'},{ name: 'Rainbow Dash',color: 'blue'},{ name: 'Applejack', color: 'orange'}]

// 这边进行实际的关联。
// 它需要一个宠物，然后迭代新建立的 Users 阵列，加入每一个到它的连接资料表 var associate = function(onePony,cb){
  var thisPony = onePony;
  var callback = cb;

  storeUsers.forEach(function(thisUser,index){
    console.log('Associating ',thisPony.name,'with',thisUser.name);
    thisUser.pets.add(thisPony.id);
    thisUser.save(console.log);

    if (index === storeUsers.length-1)
      return callback(thisPony.name);
  })
};

// 这个回呼会在所有 Pets 建立后执行。
// 它送出每个新宠物和我们的 Users 到 'associate'
var afterPony = function(err,newPonys){
  while (newPonys.length){
    var thisPony = newPonys.pop();
    var callback = function(ponyID){
      console.log('Done with pony ',ponyID)
    }
    associate(thisPony,callback);
  }
  console.log('Everyone belongs to everyone!! Exiting.');

  // 这个回呼让我们离开 bootstrap.js 并继续启动应用程序！
  return cb();
};

// 这个回呼会在所有 Users 建立后执行。
// 它需要返回的 User 并储存到 storeUsers 阵列供稍后使用。
var afterUser = function(err,newUsers){
  while (newUsers.length)
    storeUsers.push(newUsers.pop());

  Pet.create(ponys).exec(afterPony);
};

User.create(users).exec(afterUser);

}; 
```

使用 `sails console` 启动应用程序

```sh

dude@littleDude:~/node/myApp$ sails console

info: Starting app in interactive mode...

Associating Applejack with Gabe Associating Applejack with Cody Associating Applejack with Mike Done with pony Applejack Associating Rainbow Dash with Gabe Associating Rainbow Dash with Cody Associating Rainbow Dash with Mike Done with pony Rainbow Dash Associating Pinkie Pie with Gabe Associating Pinkie Pie with Cody Associating Pinkie Pie with Mike Done with pony Pinkie Pie Everyone belongs to everyone!! Exiting. info: Welcome to the Sails console. info: ( to exit, type <ctrl class="calibre25">+ <c class="calibre25">)</c></ctrl>

sails> null { name: 'Gabe', age: 107, createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST), updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CS

# One Way Association

# 单向关联（One Way Association）

### 概述

单向关联就是一个模型关联到另一个模型。你可以查询该模型并提供所关联的模型。但是，你不能查询被关联的模型并提供关联它的模型。

### 单向关联例子

在这个例子中，我们关联了一个 `User` 到 `Pet`，而不是 `Pet` 到 `User`。

`myApp/api/models/pet.js`

```
 module.exports = {

  attributes: {
    name:'STRING',
    color:'STRING'
  }

} 
```

`myApp/api/models/user.js`

```
 module.exports = {

  attributes: {
    name:'STRING',
    age:'INTEGER',
    pony:{
      model: 'pet'
    }
  }

} 
```

使用 `sails console`

```
 sails> Pet.create({name:'Pinkie Pie',color:'pink'}).exec(console.log)
null { name: 'Pinkie Pie',
  color: 'pink',
  createdAt: Tue Feb 11 2014 15:45:33 GMT-0600 (CST),
  updatedAt: Tue Feb 11 2014 15:45:33 GMT-0600 (CST),
  id: 5 }

sails> User.create({name:'Mike',age:21,pony:5}).exec(console.log);
null { name: 'Mike',
  age: 21,
  pony: 5,
  createdAt: Tue Feb 11 2014 15:48:53 GMT-0600 (CST),
  updatedAt: Tue Feb 11 2014 15:48:53 GMT-0600 (CST),
  id: 1 }

sails> User.find({name:'Mike'}).populate('pony').exec(console.log);
null [ { name: 'Mike',
    age: 21,
    pony: 
     { name: 'Pinkie Pie',
       color: 'pink',
       id: 5,
       createdAt: Tue Feb 11 2014 15:45:33 GMT-0600 (CST),
       updatedAt: Tue Feb 11 2014 15:45:33 GMT-0600 (CST) },
    createdAt: Tue Feb 11 2014 15:48:53 GMT-0600 (CST),
    updatedAt: Tue Feb 11 2014 15:48:53 GMT-0600 (CST),
    id: 1 } ] 
```

### 注意事项

> 请查看 [Waterline 文件](https://github.com/balderdashy/waterline-docs/blob/master/associations.md)取得这种类型的关联的更多资讯
> 
> 因为我们只形成一个关联于一个模型，`Pet` 没有归属于 `User` 模型的数量限制。如果我们想要，我们可以改变这一点，让 `Pet` 正好关联到一个 `User` ，且 `User` 正好关联到一个 `Pet`。

<docmeta value="OneWayAssociation708096" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="One Way Association" name="displayName" class="calibre17"></docmeta>

# Oneto Many

# 一对多（One-to-Many）

### 概述

一对多关联表示一个模型可以关联到许多其他模型。要建立这种关联，要加入一个虚拟属性 `collection` 到模型。在一对多关联中，一边必需有 `collection` 属性，另一边必需包含一个 `modal` 属性。这让「Many」那侧知道当使用 `populate` 时，它需要取得哪些记录。

因为你可能想要一个模型有多个一对多关联到另一个模型，`collection` 属性必需要有一个 `via` 键。这说明了哪一边的关联 `modal` 属性会用来提供记录。

### 一对多例子

`myApp/api/models/pet.js`

```
 module.exports = {

  attributes: {
    name:'STRING',
    color:'STRING',
    owner:{
      model:'user'
    }
  }

} 
```

`myApp/api/models/user.js`

```
 module.exports = {

  attributes: {
    name:'STRING',
    age:'INTEGER',
    pets:{
      collection: 'pet',
      via: 'owner'
    }
  }

} 
```

使用 `sails console`

```
 sails> User.create({name:'Mike',age:'21'}).exec(console.log)
null { pets: [Getter/Setter],
  name: 'Mike',
  age: 21,
  createdAt: Tue Feb 11 2014 17:49:04 GMT-0600 (CST),
  updatedAt: Tue Feb 11 2014 17:49:04 GMT-0600 (CST),
  id: 1 }

sails> Pet.create({name:'Pinkie Pie',color:'pink',owner:1}).exec(console.log)
null { name: 'Pinkie Pie',
  color: 'pink',
  owner: 1,
  createdAt: Tue Feb 11 2014 17:58:04 GMT-0600 (CST),
  updatedAt: Tue Feb 11 2014 17:58:04 GMT-0600 (CST),
  id: 2 }

sails> Pet.create({name:'Applejack',color:'orange',owner:1}).exec(console.log)
null { name: 'Applejack',
  color: 'orange',
  owner: 1,
  createdAt: Tue Feb 11 2014 18:02:58 GMT-0600 (CST),
  updatedAt: Tue Feb 11 2014 18:02:58 GMT-0600 (CST),
  id: 4 }

sails> User.find().populate('pets').exec(function(err,r){console.log(r[0].toJSON())});
{ pets: 
   [ { name: 'Pinkie Pie',
       color: 'pink',
       id: 2,
       createdAt: Tue Feb 11 2014 17:58:04 GMT-0600 (CST),
       updatedAt: Tue Feb 11 2014 17:58:04 GMT-0600 (CST),
       owner: 1 },
     { name: 'Applejack',
       color: 'orange',
       id: 4,
       createdAt: Tue Feb 11 2014 18:02:58 GMT-0600 (CST),
       updatedAt: Tue Feb 11 2014 18:02:58 GMT-0600 (CST),
       owner: 1 } ],
  name: 'Mike',
  age: 21,
  createdAt: Tue Feb 11 2014 17:49:04 GMT-0600 (CST),
  updatedAt: Tue Feb 11 2014 17:49:04 GMT-0600 (CST),
  id: 1 }

sails> Pet.find(4).populate('owner').exec(console.log)
null [ { name: 'Applejack',
    color: 'orange',
    owner: 
     { pets: [Getter/Setter],
       name: 'Mike',
       age: 21,
       id: 1,
       createdAt: Tue Feb 11 2014 17:49:04 GMT-0600 (CST),
       updatedAt: Tue Feb 11 2014 17:49:04 GMT-0600 (CST) },
    createdAt: Tue Feb 11 2014 18:02:58 GMT-0600 (CST),
    updatedAt: Tue Feb 11 2014 18:02:58 GMT-0600 (CST),
    id: 4 } ] 
```

### 注意事项

> 请查看 [Waterline 文件](https://github.com/balderdashy/waterline-docs/blob/master/associations.md)取得这种类型的关联的更多资讯

<docmeta value="OnetoMany478093" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="One-to-Many" name="displayName" class="calibre17"></docmeta>

# Oneto One

# 一对一（One-to-One）

### 概述

一对一关联表示一个模型可能只与另一个模型关联。为了使模型知道它与其他哪些模型关联，外键必需包含在记录中。

### 一对一例子

在这个例子中，我们关联了一个 `Pet` 到 `User`。在这种情况下 `User` 可能只有一个 `Pet`，但是 `Pet` 并不局限于单一 `User`。

`myApp/api/models/pet.js`

```
 module.exports = {

  attributes: {
    name:'STRING',
    color:'STRING',
    owner:{
      model:'user'
    }
  }

} 
```

`myApp/api/models/user.js`

```
 module.exports = {

  attributes: {
    name:'STRING',
    age:'INTEGER',
    pony:{
      model: 'pet'
    }
  }

} 
```

使用 `sails console`

```
 sails> User.create({ name: 'Mike', age: 21}).exec(console.log);
null { name: 'Mike',
  age: 21,
  createdAt: Thu Feb 20 2014 17:12:18 GMT-0600 (CST),
  updatedAt: Thu Feb 20 2014 17:12:18 GMT-0600 (CST),
  id: 1 }

sails> Pet.create({ name: 'Pinkie Pie', color: 'pink', owner: 1}).exec(console.log)
null { name: 'Pinkie Pie',
    color: 'pink',
    owner: 1,
    createdAt: Thu Feb 20 2014 17:26:16 GMT-0600 (CST),
    updatedAt: Thu Feb 20 2014 17:26:16 GMT-0600 (CST),
    id: 2 }

sails> Pet.find().populate('owner').exec(console.log)
null [ { name: 'Pinkie Pie',
    color: 'pink',
    owner: 
     { name: 'Mike',
       age: 21,
       id: 1,
       createdAt: Thu Feb 20 2014 17:12:18 GMT-0600 (CST),
       updatedAt: Thu Feb 20 2014 17:12:18 GMT-0600 (CST) },
    createdAt: Thu Feb 20 2014 17:26:16 GMT-0600 (CST),
    updatedAt: Thu Feb 20 2014 17:26:16 GMT-0600 (CST),
    id: 2 } ]

sails> User.find().populate('pony').exec(console.log)
null [ { name: 'Mike',
    age: 21,
    createdAt: Thu Feb 20 2014 18:11:15 GMT-0600 (CST),
    updatedAt: Thu Feb 20 2014 18:11:15 GMT-0600 (CST),
    id: 2,
    pony: undefined } ]

sails> User.update({name:'Mike'},{pony:2}).exec(console.log)
null [ { name: 'Mike',
    age: 21,
    createdAt: Thu Feb 20 2014 17:12:18 GMT-0600 (CST),
    updatedAt: Thu Feb 20 2014 17:30:58 GMT-0600 (CST),
    id: 1,
    pony: 2 } ]

sails> User.findOne(1).populate('pony').exec(console.log)
null { name: 'Mike',
  age: 21,
  createdAt: Thu Feb 20 2014 17:12:18 GMT-0600 (CST),
  updatedAt: Thu Feb 20 2014 17:30:58 GMT-0600 (CST),
  id: 1,
  pony: 
   { name: 'Pinkie Pie',
     color: 'pink',
     id: 2,
     createdAt: Thu Feb 20 2014 17:26:16 GMT-0600 (CST),
     updatedAt: Thu Feb 20 2014 17:26:16 GMT-0600 (CST),
     owner: 1 } } 
```

### 注意事项

> 请查看 [Waterline 文件](https://github.com/balderdashy/waterline-docs/blob/master/associations.md)取得这种类型的关联的更多资讯

<docmeta value="OnetoOne169258" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="One-to-One" name="displayName" class="calibre17"></docmeta>

# Through Associations

# 穿透关联（Through Associations）

### 概述

多对多穿透关联的行为和多对多关联相同，且会自动为你建立例外的连接表。这使你可以附加额外的属性到连接表内的关联。

不幸的是，他们尚未支持。请不要担心，有一个简单的解决方法。

你可以通过使用一个额外的模型为中介来实现这一目标。你可以使用多个一对多关联到中介模型，取代两个模型间的多对多关联。

<docmeta value="ThroughAssociations740718" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Through Associations" name="displayName" class="calibre17"></docmeta>

# Attributes

# Lifecyclecallbacks

# 生命周期回呼（Lifecycle callbacks）

### 概述

Sails 公开了一些模型的生命周期回呼，在做某些动作之前或之后会自动被呼叫。例如，我们有时候会使用生命周期回呼在建立或更新帐号模型前自动加密密码。另一个使用情况是当工程的 `name` 属性更新时自动重新产生网址。

##### `create` 的回呼

*   beforeValidate: fn(values, cb)
*   afterValidate: fn(values, cb)
*   beforeCreate: fn(values, cb)
*   afterCreate: fn(newlyInsertedRecord, cb)

##### `update` 的回呼

*   beforeValidate: fn(valuesToUpdate, cb)
*   afterValidate: fn(valuesToUpdate, cb)
*   beforeUpdate: fn(valuesToUpdate, cb)
*   afterUpdate: fn(updatedRecord, cb)

##### `destroy` 的回呼

*   beforeDestroy: fn(criteria, cb)
*   afterDestroy: fn(destroyedRecords, cb)

### 例子

如果你想在密码储存到资料库前先加密，你可以使用 `beforeCreate` 生命周期回呼。

```
var bcrypt = require('bcrypt');

module.exports = {

  attributes: {

    username: {
      type: 'string',
      required: true
    },

    password: {
      type: 'string',
      minLength: 6,
      required: true,
      columnName: 'encrypted_password'
    }

  },

  // 生命周期回呼
  beforeCreate: function (values, cb) {

    // 密码加密
    bcrypt.hash(values.password, 10, function(err, hash) {
      if(err) return cb(err);
      values.password = hash;
      // 呼叫 cb() 时带入一个参数，会返回错误。当某些条件失败要取消整个操作时很有用。
      cb();
    });
  }
}; 
```

<docmeta value="Lifecyclecallbacks631538" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Lifecycle callbacks" name="displayName" class="calibre17"></docmeta>

# Models

# Models

A model represents a collection of structured data, usually corresponding to a single table or collection in a database. Models are usually defined by creating a file in an app's `api/models/` folder.

![screenshot of a Waterline/Sails model in Sublime Text 2](img/deade1d3.png)

### Using models

Models may be accessed from our controllers, policies, services, responses, tests, and in custom model methods. There are many built-in methods available on models, the most important of which are the query methods: [find](http://beta.sailsjs.org/#/documentation/reference/waterline/models/find.html), [create](http://beta.sailsjs.org/#/documentation/reference/waterline/models/create.html), [update](http://beta.sailsjs.org/#/documentation/reference/waterline/models/update.html), and [destroy](http://beta.sailsjs.org/#/documentation/reference/waterline/models/destroy.html). These methods are [asynchronous](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md) - under the covers, Waterline has to send a query to the database and wait for a response.

Consequently, query methods return a deferred query object. To actually execute a query, `.exec(cb)` must be called on this deferred object, where `cb` is a callback function to run after the query is complete.

Waterline also includes opt-in support for promises. Instead of calling `.exec()` on a query object, we can call `.then()`, `.spread()`, or `.catch()`, which will return a [Bluebird promise](https://github.com/petkaantonov/bluebird).

### Model Methods (aka "static" or "class" methods)

Model class methods are functions built into the model itself that perform a particular task on its instances (records). This is where you will find the familiar CRUD methods for performing database operations like `.create()`, `.update()`, `.destroy()`, `.find()`, etc.

###### Custom model methods

Waterline allows you to define custom methods on your models. This feature takes advantage of the fact that Waterline models ignore unrecognized keys, so you do need to be careful about inadvertently overriding built-in methods and dynamic finders (don't define methods named "create", etc.) Custom model methods are most useful for extrapolating controller code that relates to a particular model; i.e. this allows you to pull code your controllers and into reusuable functions that can be called from anywhere (i.e. don't depend on `req` or `res`.)

Model methods are generally asynchronous functions. By convention, asynchronous model methods should be 2-ary functions, which accept an object of inputs as their first argument (usually called `opts` or `options`) and a Node callback as the second argument. Alternatively, you might opt to return a promise (both strategies work just fine- it's a matter of preference. If you don't have a preference, stick with Node callbacks.)

A best practice is to write your static model method so that it can accept either a record OR its primary key value. For model records that operate on/from *multiple* records at once, you should allow an array of records OR an array of primary key values to be passed in. This takes more time to write, but makes your method much more powerful. And since you're doing this to extrapolate commonly-used logic anyway, it's usually worth the extra effort.

For example:

```js // in api/models/Monkey.js...

// Find monkeys with the same name as the specified person findWithSameNameAsPerson: function (opts, cb) {

var person = opts.person;

// Before doing anything else, check if a primary key value // was passed in instead of a record, and if so, lookup which // person we're even talking about: (function _lookupPersonIfNecessary(afterLookup){ // (this self-calling function is just for concise-ness) if (typeof person === 'object')) return afterLookup(n

# Querylanguage

# Waterline Query Language

The Waterline Query language is an object-based criteria used to retrieve the records from any of the supported database adapters. This means that you can use the same query on MySQL as you do on Redis or MongoDb. This allows you to change your database without changing your code.

### Query Language Basics

The criteria objects are formed using one of four types of object keys. These are the top level keys used in a query object. It is loosely based on the criteria used in MongoDB with a few slight variations.

Queries can be built using either a `where` key to specify attributes, which will allow you to also use query options such as `limit` and `skip` or if `where` is excluded the entire object will be treated as a `where` criteria.

```
Model.find({ where: { name: 'foo' }, skip: 20, limit: 10, sort: 'name DESC' });

// OR

Model.find({ name: 'foo' }) 
```

#### Key Pairs

A key pair can be used to search records for values matching exactly what is specified. This is the base of a criteria object where the key represents an attribute on a model and the value is a strict equality check of the records for matching values.

```
Model.find({ name: 'walter' }) 
```

They can be used together to search multiple attributes.

```
Model.find({ name: 'walter', state: 'new mexico' }) 
```

#### Modified Pairs

Modified pairs also have model attributes for keys but they also use any of the supported criteria modifiers to perform queries where a strict equality check wouldn't work.

```
Model.find({
  name : {
    'contains' : 'alt'
  }
}) 
```

#### In Pairs

IN queries work similarly to mysql 'in queries'. Each element in the array is treated as 'or'.

```
Model.find({
  name : ['Walter', 'Skyler']
}); 
```

#### Not-In Pairs

Not-In queries work similar to `in` queries, except for the nested object criteria.

```
Model.find({
  name: { '!' : ['Walter', 'Skyler'] }
}); 
```

#### Or Pairs

Performing `OR` queries is done by using an array of query pairs. Results will be returned that match any of the criteria objects inside the array.

```
Model.find({
  or : [
    { name: 'walter' },
    { occupation: 'teacher' }
  ]
}) 
```

### Criteria Modifiers

The following modifiers are available to use when building queries.

*   `'<'` / `'lessThan'`
*   `'<='` / `'lessThanOrEqual'`
*   `'>'` / `'greaterThan'`
*   `'>='` / `'greaterThanOrEqual'`
*   `'!'` / `'not'`
*   `'like'`
*   `'contains'`
*   `'startsWith'`
*   `'endsWith'`

#### '<' / 'lessThan'

Searches for records where the value is less than the value specified.

```
Model.find({ age: { '<': 30 }}) 
```

#### '<=' / 'lessThanOrEqual'

Searches for records where the value is less or equal to the value specified.

```
Model.find({ age: { '<=': 21 }}) 
```

#### '>' / 'greaterThan'

Searches for records where the value is more than the value specified.

```
Model.find({ age: { '>': 18 }}) 
```

#### '>=' / 'greaterThanOrEqual'

Searches for records where the value is more or equal to the value specified.

```
Model.find({ age: { '>=': 21 }}) 
```

#### '!' / 'not'

Searches for records where the value is not equal to the value specified.

```
Model.find({ name: { '!': 'foo' }}) 
```

#### 'like'

Searches for records using pattern matching with the `%` sign.

```
Model.find({ food: { 'like': '%beans' }}) 
```

#### 'contains'

A shorthand for pattern matching both sides of a string. Will return records where the value contains the string anywhere inside of it.

```
Model.find({ class: { 'contains': 'history' }})

// The same as

Model.find({ class: { 'like': '%history%' }}) 
```

#### 'startsWith'

A shorthand for pattern matching the right side of a string. Will return records where the value starts with the supplied string value.

```
Model.find({ class: { 'startsWith': 'american' }})

// The same as

Model.find({ class: { 'like': 'american%' }}) 
```

#### 'endsWith'

A shorthand for pattern matching the left side of a string. Will

# Validations

# Validations

Sails bundles support for automatic validations of your models' attributes. Any time a record is updated, or a new record is created, the data for each attribute will be checked against all of your predefined validation rules. This provides a convenient failsafe to ensure that invalid entries don't make their way into your app's database(s).

### Validation Rules

Validations are handled by [Anchor](https://github.com/balderdashy/anchor), a thin layer on top of [Validator](https://github.com/chriso/validator.js), one of the most robust validation libraries for Node.js. Sails supports most of the validations available in Validator, as well as a few extras that require database integration, like `unique`.

| Name of validator | What does it check? | Notes on usage |
| --- | --- | --- |
| after | check if `string` date in this record is after the specified `Date` | must be valid javascript `Date` |
| alpha | check if `string` in this record contains only letters (a-zA-Z) |  |
| alphadashed |  | does this `string` contain only numbers and/or dashes? |
| alphanumeric | check if `string` in this record contains only letters and numbers. |  |
| alphanumericdashed | does this `string` contain only numbers and/or letters and/or dashes? |  |
| array | is this a valid javascript `array` object? | strings formatted as arrays won't pass |
| before | check if `string` in this record is a date that's before the specified date |  |
| binary | is this binary data? | If it's a string, it will always pass |
| boolean | is this a valid javascript `boolean` ? | `string`s will fail |
| contains | check if `string` in this record contains the seed |  |
| creditcard | check if `string` in this record is a credit card |  |
| date | check if `string` in this record is a date | takes both strings and javascript |
| datetime | check if `string` in this record looks like a javascript `datetime` |  |
| decimal |  | contains a decimal or is less than 1? |
| email | check if `string` in this record looks like an email address |  |
| empty | Arrays, strings, or arguments objects with a length of 0 and objects with no own enumerable properties are considered "empty" | lo-dash _.isEmpty() |
| equals | check if `string` in this record is equal to the specified value | `===` ! They must match in both value and type |
| falsey | Would a Javascript engine register a value of `false` on this? |  |
| finite | Checks if given value is, or can be coerced to, a finite number | This is not the same as native isFinite which will return true for booleans and empty strings |
| float | check if `string` in this record is of the number type float |  |
| hexadecimal | check if `string` in this record is a hexadecimal number |  |
| hexColor | check if `string` in this record is a hexadecimal color |  |
| in | check if `string` in this record is in the specified array of allowed `string` values |  |
| int | check if `string` in this record is an integer |  |
| integer | same as above | Im not sure why there are two of these. |
| ip | check if `string` in this record is a valid IP (v4 or v6) |  |
| ipv4 | check if `string` in this record is a valid IP v4 |  |
| ipv6 | check if `string` in this record is aa valid IP v6 |  |
| is |  | something to do with REGEX |
| json | does a try&catch to check for valid JSON. |  |
| len | is `integer` > param1 && < param2 | Where are params defined? |
| lowercase | is this string in all lowercase? |  |
| max |  |  |
| maxLength | is `integer` > 0 && < param2 |  |
| min |  |  |
| minLength |  |  |
| not |  | Something about regexes |
| notContains |  |  |
| notEmpty |  |  |
| notIn | does the value of this model attribute exist inside of the defined validator value (of the same type) | Takes strings and arrays |
| notNull | does this not have a value of `null` ? |  |
| notRegex |  |  |
| null | check if `string` in this record is null |  |
| number | is this a number? | NaN is considered a number |
| numeric | checks if `string` in this record contains only numbers |  |
| object | checks if this attribute is the language type of Object | Passes for arrays, functions, objects, regexes, new Number(0), and new String |

# Model Settings

# 模型设置（Model Settings）

以下的属性可以指定在你的模型定义的上层，来覆写该模型的默认值。修改 [`config/models.js`](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md) 来覆写所有模型共享的默认设置。

### `migrate`

```
migrate: 'safe' 
```

总之，此设置控制了 Sails 是否／如何尝试在你的结构自动重建 tables/collections/sets 等。

在生产环境中（NODE_ENV === "production"）Sails 总是使用 `migrate:"safe"` 来保护意外删除你的资料。然而在开发过程中，你有其他几个方便的选项：

1.  safe - 永远不要自动迁移我的资料库。我会自己去做（手动）
2.  alter - 自动迁移，但尝试保留现有资料（实验性）
3.  drop - 每次启动 Sails 时清除／删除所有资料并重建模型

当你启动 sails 应用程序时，waterline 会验证你的资料库的所有资料。这个标记告诉 waterline 资料毁损时该如何处理资料。你可以设置这个标记为 `safe`，将忽略毁损的资料并继续启动。你还可以将其设置为

| 自动迁移策略 | 说明 |
| --- | --- |
| `safe` | 永远不要自动迁移我的资料库。我会自己手动去做 |
| `alter` | 自动迁移，但尝试保留现有资料（实验性） |
| `drop` | 每次启动 Sails 时清除／删除所有资料并重建模型 |

> 请注意，使用 `drop` 或 `alter` 可能失去你的资料。当心，永远不要在生产环境使用 `drop` 或 `alter`。

### `schema`

```
schema: true 
```

在支持无结构（Schemaless）资料结构资料库切换无结构（Schemaless）或结构（Schema）模式的标记。如果关闭，将允许你储存任意资料的记录。如果开启，只有定义在模型的 `attributes` 属性对象会被储存。

对于不需要结构的桥接器，如 Mongo 或 Redis，默认设置是 `schema:false`。

### `connection`

```
connection: 'my-local-postgresql' 
```

此模型将从已设置的资料库[连线](http://sailsjs.org/#/documentation/reference/sails.config/sails.config.connections.html)取得和储存资料。默认为 `localDiskDb`，默认的连线使用 `sails-disk` 桥接器。

### `identity`

```
identity: 'purchase' 
```

此模型的小写唯一键（Unique key），例如 `user`。默认情况下，会自动从它的文档名称自动推测模型的 `identity`。你永远不应该在模型改变这个属性。

### `globalId`

```
globalId: 'Purchase' 
```

这个标记变更了你可以存取模型的全局名称（如果启用了模型的全局化）。你永远不应该在模型改变这个属性。要停用全局，请参考 [`sails.config.globals`](http://sailsjs.org/#/documentation/concepts/Globals?q=disabling-globals)。

### `autoPK`

```
autoPK: true 
```

切换模型中自动定义主键的标记。此默认 PK 的细节依桥接器而有所不同（例如 MySQL 使用一个自动递增的整数主键，而 MongoDB 使用乱数字串 UUID）。在任何情况下，由 autoPK 产生的主键是唯一的。如果关闭，默认将不会建立主键，你将需要手动定义一个，例如：

```
attributes: {
  sku: {
    type: 'string',
    primaryKey: true,
    unique: true
  }
} 
```

### `autoCreatedAt`

```
autoCreatedAt: true 
```

切换模型中自动定义 `createdAt` 属性的标记。默认情况下，当记录建立时 `createdAt` 属性会自动设置为目前时间戳记，例如：

```
attributes: {
  createdAt: {
    type: 'datetime',
    defaultsTo: function (){ return new Date(); }
  }
} 
```

### `autoUpdatedAt`

```
autoUpdatedAt: true 
```

切换模型中自动定义 `updatedAt` 属性的标记。默认情况下，当记录被更新时 `updatedAt` 属性会自动设置为目前时间戳记，例如：

```
attributes: {
  updatedAt: {
    type: 'datetime',
    defaultsTo: function (){ return new Date(); }
  }
} 
```

### `tableName`

```java

# Policies

# Policies

### Overview

Policies in Sails are versatile tools for authorization and access control-- they let you allow or deny access to your controllers down to a fine level of granularity. For example, if you were building Dropbox, before letting a user upload a file to a folder, you might check that she `isAuthenticated`, then ensure that she `canWrite` (has write permissions on the folder.) Finally, you'd want to check that the folder she's uploading into `hasEnoughSpace`.

Policies can be used for anything: HTTP BasicAuth, 3rd party single-sign-on, OAuth 2.0, or your own custom authorization/authentication scheme.

> NOTE: policies apply **only** to controller actions, not to views. If you define a route in your [routes.js config file](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.routes.html) that points directly to a view, no policies will be applied to it. To make sure policies are applied, you can instead define a controller action which displays your view, and point your route to that action.

### Writing Your First Policy

Policies are files defined in the `api/policies` folder in your Sails app. Each policy file should contain a single function.

When it comes down to it, policies are really just Connect/Express middleware functions which run **before** your controllers. You can chain as many of them together as you like-- in fact they're designed to be used this way. Ideally, each middleware function should really check just *one thing*.

For example, the `canWrite` policy mentioned above might look something like this:

```
// policies/canWrite.js
module.exports = function canWrite (req, res, next) {
  var targetFolderId = req.param('id');
  var userId = req.session.user.id;

  Permission
  .findOneByFolderId( targetFolderId )
  .exec( function foundPermission (err, permission) {

    // Unexpected error occurred-- skip to the app's default error (500) handler
    if (err) return next(err);

    // No permission exists linking this user to this folder.  Maybe they got removed from it?  Maybe they never had permission in the first place?  Who cares?
    if ( ! permission ) return res.redirect('/notAllowed');

    // OK, so a permission was found.  Let's be sure it's a "write".
    if ( permission.type !== 'write' ) return res.redirect('/notAllowed');

    // If we made it all the way down here, looks like everything's ok, so we'll let the user through
    next();
  });
}; 
```

### Protecting Controllers with Policies

Sails has a built in ACL (access control list) located in `config/policies.js`. This file is used to map policies to your controllers.

This file is *declarative*, meaning it describes *what* the permissions for your app should look like, not *how* they should work. This makes it easier for new developers to jump in and understand what's going on, plus it makes your app more flexible as your requirements inevitably change over time.

Your `config/policies.js` file should export a Javascript object whose keys are controller names (or `'*'` for global policies), and whose values are objects mapping action names to one or more policies. See below for more details and examples.

##### To apply a policy to a specific controller action:

```
{
  ProfileController: {
      // Apply the 'isLoggedIn' policy to the 'edit' action of 'ProfileController'
      edit: 'isLoggedIn'
      // Apply the 'isAdmin' AND 'isLoggedIn' policies, in that order, to the 'create' action
      create: ['isAdmin', 'isLoggedIn']
  }
} 
```

##### To apply a policy to an entire controller:

```
{
  ProfileController: {
    // Apply 'isLogged' in by default to all actions that are NOT specified below
    '*': 'isLoggedIn',
    // If an action is explicitly listed, its policy list will override the default list.
    // So, we have to list 'isLoggedIn' again for the 'edit' action if we want it to be applied.
    edit: ['isAdmin', 'isLoggedIn']
  }
} 
```

> **Note:** Default policy mappings do not "cascade" or "trickle down." Specified mappings for the controller'

# Routes

# Routes

### Overview

The most basic feature of any web application is the ability to interpret a request sent to a URL, then send back a response. In order to do this, your application has to be able to distinguish one URL from another.

Like most web frameworks, Sails provides a router: a mechanism for mapping URLs to controllers and views. **Routes** are rules that tell Sails what to do when faced with an incoming request. There are two main types of routes in Sails: **custom** (or "explicit") and **automatic** (or "implicit").

### Custom Routes

Sails lets you design your app's URLs in any way you like- there are no framework restrictions.

Every Sails project comes with [`config/routes.js`](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.routes.html), a simple [Node.js module](http://nodejs.org/api/modules.html) that exports an object of custom, or "explicit" **routes**. For example, this `routes.js` file defines six routes; some of them point to a controller's action, while others route directly to a view.

```
// config/routes.js
module.exports = {
  'get /signup': { view: 'conversion/signup' },
  'post /signup': 'AuthController.processSignup',
  'get /login': { view: 'portal/login' },
  'post /login': 'AuthController.processLogin',
  '/logout': 'AuthController.logout',
  'get /me': 'UserController.profile'
} 
```

Each **route** consists of an **address** (on the left, e.g. `'get /me'`) and a **target** (on the right, e.g. `'UserController.profile'`) The **address** is a URL path and (optionally) a specific [HTTP method](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods). The **target** can be defined a number of different ways ([see the expanded concepts section on the subject](http://beta.sailsjs.org/#/documentation/concepts/Routes/RouteTargetSyntax.html)), but the two different syntaxes above are the most common. When Sails receives an incoming request, it checks the **address** of all custom routes for matches. If a matching route is found, the request is then passed to its **target**.

For example, we might read `'get /me': 'UserController.profile'` as:

> "Hey Sails, when you receive a GET request to `http://mydomain.com/me`, run the `profile` action of `UserController`, would'ya?"

What if I want to change the view layout within the route itself? No problem we could:

```
'get /privacy': {
    view: 'users/privacy',
    locals: {
      layout: 'users'
    }
  }, 
```

#### Notes

*   Just because a request matches a route address doesn't necessarily mean it will be passed to that route's target *directly*. For instance, HTTP requests will usually pass through some [middleware](http://beta.sailsjs.org/#/documentation/concepts/Middleware) first. And if the route points to a controller [action](http://beta.sailsjs.org/#/documentation/concepts/Controllers?q=actions), the request will need to pass through any configured [policies](http://beta.sailsjs.org/#/documentation/concepts/Policies) first. Finally, there are a few special [route options](http://beta.sailsjs.org/#/documentation/concepts/Routes/RouteTargetSyntax.html?q=route-target-options) which allow a route to be "skipped" for certain kinds of requests.
*   The router can also programmatically **bind** a **route** to any valid route target, including canonical Node middleware functions (i.e. `function (req, res, next) {}`). However, you should always use the conventional [route target syntax](http://beta.sailsjs.org/#/documentation/concepts/Routes/RouteTargetSyntax.html) when possible- it streamlines development, simplifies training, and makes your app more maintainable.

### Automatic Routes

In addition to your custom routes, Sails binds many routes for you automatically. If a URL doesn't match a custom route, it may match one of the automatic routes and still generate a response. The main types of automatic routes in Sails are:

*   [Blueprint routes](http://beta.sailsjs.org/#/documentation/reference/blueprint-api?q=blueprint-routes), which provide your controllers. Note the initial `/` in the path--all paths should start with one in order to work properly.

#### Wildcards and dynamic parameters

In addition to specifying a static path like **foo/bar**, you can use `*` as a wildcard:

```
'/*' 
```

will match all paths, where as:

```
'/user/foo/*' 
```

will match all paths that *start* with **/user/foo**.

You can capture the parts of the address that are matched by wildcards into named parameters by using the `:paramName` wildcard syntax instead of the `*`:

```
'/user/foo/:name/bar/:age' 
```

Will match the same URLs as:

```
'/user/foo/*/bar/*' 
```

but will provide the values of the wildcard portions of the route to the route handler as `req.param('name')` and `req.param('age')`, respectively.

#### Regular expressions in addresses

In addition to the wildcard address syntax, you may also use Regular Expressions to define the URLs that a route should match. The syntax for defining an address with a regular expression is:

`"r|<regular expression string>|<comma-delimited list of param names>"`

That's the letter "**r**", followed by a pipe character `|`, a regular expression string *without delimiters*, another pipe, and a list of parameter names that should be mapped to parenthesized groups in the regular expression. For example:

`"r|^/\\d+/(\\w+)/(\\w+)$|foo,bar": "MessageController.myaction"`

Will match `/123/abc/def`, running the `myaction` action of `MessageController` and supplying the values `abc` and `def` as `req.param('foo')` and `req.param('bar')`, respectively.

Note the double-backslash in `\\d` and `\\w`; this escaping is necessary for the regular expression to work correctly!

#### About route ordering

When using wildcards or regular expressions in your addresses, keep in mind that the ordering of your routes in **config/routes.js** matters; URLs are matched against addresses in the list from the top down. If you have two configurations in this order:

```
'/user': 'UserController.doSomething',
'/*'   : 'CatchallController.doSomethingElse' 
```

then a request to `/user` will not be matched by the second configuration unless the first configuration's handler calls `next()` in its code, which is discouraged (only [policies](http://beta.sailsjs.org/#/documentation/concepts/Policies) should call `next()`). Unless you're doing something very advanced, it is safe to assume that every request will be handled by at most one route in your **config/routes.js** file.

### Route Target

The address portion of a custom route specifies which URLs the route should match. The *target* portion specifies what Sails should do after the match is made. A target can take one of several different forms. In some cases you may want to chain multiple targets to a single address by placing them in an array, but in most cases each address will have only one target. The different types of targets are discussed below, followed by a discussion of the various options that can be applied to them.

#### Controller / action target syntax

The most common type of target is one which binds a route to a custom [controller action](http://beta.sailsjs.org/#/documentation/concepts/Controllers?q=actions). The following four routes are equivalent:

``` 'GET /foo/go': 'FooController.myGoAction', 'GET /foo/go': 'Foo.myGoAction', 'GET /foo/go': {controller: "Foo", action: "myGoAction"}, 'GET /

# URL Slugs

# URL Slugs

A common use case for explicit routes is the design of slugs or [vanity URLs](http://en.wikipedia.org/wiki/Clean_URL#Slug). For example, consider the URL of a repository on Github, [`http://www.github.com/balderdashy/sailsjs`](http://www.github.com/balderdashy/sailsjs). In Sails, we might define this route at the **bottom of our `config/routes.js` file** like so:

```
 'get /:account/:repo': {
    controller: 'RepoController',
    action: 'show',
    skipAssets: true
  } 
```

In your `RepoController`'s `show` action, we'd use `req.param('account')` and `req.param('repo')` to look up the data for the appropriate repository, then pass it in to the appropriate [view](http://beta.sailsjs.org/#/documentation/concepts/Views) as [locals](http://beta.sailsjs.org/#/documentation/concepts/Views/Locals.html). The [`skipAssets` option](http://beta.sailsjs.org/#/documentation/concepts/Routes/RouteTargetSyntax.html?q=route-target-options) ensures that the vanity route doesn't accidentally match any of our [assets](http://beta.sailsjs.org/#/documentation/concepts/Assets) (e.g. `/images/logo.png`), so they are still accessible.

<docmeta value="URLSlugs805236" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="URL Slugs" name="displayName" class="calibre17"></docmeta>

# Security

# Security

### Overview

Sails and Express provide built-in, easily configurable protection against most known types of web-application-level attacks.

<docmeta value="Security59375" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Security" name="displayName" class="calibre17"></docmeta>

# CORS

# Cross-Origin Resource Sharing (CORS)

[CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing) is a mechanism that allows browser scripts on pages served from other domains (e.g. myothersite.com) to talk to your server (e.g. api.mysite.com). Like JSONP, the goal of CORS is to function as a secure method to circumvent the [same-origin policy](http://en.wikipedia.org/wiki/Same-origin_policy); allowing your Sails server to successfully respond to requests from client-side JavaScript code running on a page from some other domain. But unlike JSONP, it works with more than just GET requests.

Sails can be configured to allow cross-origin requests from a list of domains you specify, or from every domain. This can be done on a per-route basis, or globally for every route in your app.

### Enabling CORS

For security reasons, CORS is disabled by default in Sails. But enabling it is dead-simple.

To allow cross-origin requests from *any* domain to *any* route in your app, simply enable `allRoutes` in [`config/cors.js`](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.cors.html):

```
allRoutes: true 
```

See [`sails.config.cors`](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.cors.html) for a comprehensive reference of all available options.

### Configuring CORS For Individual Routes

Besides the global CORS configuration, you can set up individual routes in `config/routes.js` to accept (or deny) cross-origin requests. To indicate that a route should accept CORS requests using the configuration parameters in `config/cors.js`, set its `cors` property to `true`:

```
"get /foo": {
   controller: "FooController",
   action: "index",
   cors: true
} 
```

If you have the `allRoutes` parameter set to `true` in `config.cors.js`, but you want to exempt a specific route, you can do so by explicitly setting its `cors` property to `false`:

```
"get /foo": {
   controller: "FooController",
   action: "index",
   cors: false
} 
```

To override specific CORS configuration parameters for a route, add a `cors` property object:

```
"get /foo": {
   controller: "FooController",
   action: "index",
   cors: {
     origin: "http://sailsjs.org, http://sailsjs.com",
     credentials: false
} 
```

<docmeta value="cors198259" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="CORS" name="displayName" class="calibre17"></docmeta>

# CSRF

# CSRF

Cross-site request forgery ([CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) is a type of attack which forces an end user to execute unwanted actions on a web application backend with which he/she is currently authenticated. In other words, without protection, cookies stored in a browser like Google Chrome can be used to send requests to Chase.com from a user's computer whether that user is currently visiting Chase.com or Horrible-Hacker-Site.com.

### Enabling CSRF Protection

Sails bundles optional CSRF protection out of the box. To enable the built-in enforcement, just make the following adjustment to sails.config.csrf (conventionally located in your project's [`config/csrf.js`](http://beta.sailsjs.org/#/documentation/anatomy/myApp/config/csrf.js.html) file):

```
csrf: true 
```

Note that if you have existing code that communicates with your Sails backend via POST, PUT, or DELETE requests, you'll need to acquire a CSRF token and include it as a parameter or header in those requests. More on that in a sec.

### CSRF Tokens

Like most Node applications, Sails and Express are compatibile with Connect's [CSRF protection middleware](http://www.senchalabs.org/connect/csrf.html) for guarding against such attacks. This middleware implements the [Synchronizer Token Pattern](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)_Prevention_Cheat_Sheet#General_Recommendation:_Synchronizer_Token_Pattern). When CSRF protection is enabled, all non-GET requests to the Sails server must be accompanied by a special token, identified by either a header or a parameter in the query string or HTTP body.

CSRF tokens are temporary and session-specific; e.g. Imagine Mary and Muhammad are both shoppers accessing our e-commerce site running on Sails, and CSRF protection is enabled. Let's say that on Monday, Mary and Muhammad both make purchases. In order to do so, our site needed to dispense at least two different CSRF tokens- one for Mary and one for Muhammad. From then on, if our web backend received a request with a missing or incorrect token, that request will be rejected. So now we can rest assured that when Mary navigates away to play online poker, the 3rd party website cannot trick the browser into sending malicious requests to our site using her cookies.

### Dispensing CSRF Tokens

To get a CSRF token, you should either bootstrap it in your view using [locals](http://beta.sailsjs.org/#/documentation/concepts/Views/Locals.html) (good for traditional multi-page web applications) or fetch it using sockets or AJAX from a special protected JSON endpoint (handy for single-page-applications (SPAs).)

##### Using View Locals:

For old-school form submissions, it's as easy as passing the data from a view into a form action. You can grab hold of the token in your view, where it may be accessed as a view local: `<%= _csrf %>`

e.g.:

```
<form action="/signup" method="POST">
 <input type="text" name="emailaddress"/>
 <input type='hidden' name='_csrf' value='<%= _csrf %>'>
 <input type='submit'>
</form> 
```

If you are doing a `multipart/form-data` upload with the form, be sure to place the `_csrf` field before the `file` input, otherwise you run the risk of a timeout and a 403 firing before the file finishes uploading.

##### Using AJAX/WebSockets

In AJAX/Socket-heavy apps, you might prefer to send a GET request to the built-in `/csrfToken` route, where it will be returned as JSON, e.g.:

```
{
  "_csrf": "ajg4JD(JGdajhLJALHDa"
} 
```

### Spending CSRF Tokens

Once you've enabled CSRF protection, any POST, PUT, or DELETE requests (**including** virtual requests, e.g. from Socket.io) made to your Sails app will need to send an accompanying CSRF token as a header or parameter. Otherwise, they'll be rejected with a 403 (Forbidden) response.

For example, if you're sending an AJAX request from a webpage with jQuery: ```js $.post('/checkout', { order: '8abfe13491afe', electronicReceiptOK: true, _csrf: 'USER_CSRF_TOKEN'

# Clickjacking

# Clickjacking

[Clickjacking](https://www.owasp.org/index.php/Clickjacking) (aka "UI redress attacks") are where an attacker manages to trick your users into triggering "unintended" UI events (e.g. DOM events.)

### X-FRAME-OPTIONS

One simple way to help prevent clickjacking attacks is to enable the X-FRAME-OPTIONS header.

##### Using [lusca](https://github.com/krakenjs/lusca#luscaxframevalue)

> `lusca` is open-source under the [Apache license](https://github.com/krakenjs/lusca/blob/master/LICENSE.txt)

```
# In your sails app
npm install lusca --save 
```

Then in the `middleware` config object in `config/http.js`:

```
 // ...
  // maxAge ==> Number of seconds strict transport security will stay in effect.
  xframe: require('lusca').xframe('SAMEORIGIN')
  // ...
  order: [
    // ...
    'xframe'
    // ...
  ] 
```

### Additional Resources

*   [Clickjacking (OWasp)](https://www.owasp.org/index.php/Clickjacking)

<docmeta value="Clickjacking879453" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Clickjacking" name="displayName" class="calibre25"></docmeta>

<docmeta value="clickjacking,ui redress attack" name="tags" class="calibre17"></docmeta>

# Content Security Policy

# Content Security Policy

> TODO: flesh this section out [`www.owasp.org/index.php/Content_Security_Policy`](https://www.owasp.org/index.php/Content_Security_Policy)

stuff stuff stuff

<docmeta value="ContentSecurityPolicy649437" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Content Security Policy" name="displayName" class="calibre17"></docmeta>

# DDOS

# DDOS

The prevention of [denial of service attacks](https://www.owasp.org/index.php/Application_Denial_of_Service) is a [complex problem](http://en.wikipedia.org/wiki/Denial-of-service_attack#Handling) which involves multiple layers of protection, up and down the networking stack. This type of attack has achieved [notoriety](http://www.darkreading.com/vulnerabilities-and-threats/10-strategies-to-fight-anonymous-ddos-attacks/d/d-id/1102699) in recent years due to widespread media coverage of groups like Anonymous.

At the API layer, there isn't much that can be done in the way of prevention. However, Sails offers a few settings to mitigate certain types of DDOS attacks:

*   The session in Sails can be [configured](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.session.html) to use a separate session store (e.g. [Redis](http://redis.io/)), allowing your application to run without relying on the memory state of any one API server. This means that multiple copies of your Sails app may be deployed to as many servers as is necessary to handle traffic. This is achieved by using a [load balancer](http://en.wikipedia.org/wiki/Load_balancing_(computing)), which directs each incoming request to a free server with the resources to handle it, eliminating any one app server as a single point of failure.
*   Socket.io connections may be [configured](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.sockets.html) to use a separate [socket store](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md) (e.g. Redis) for managing pub/sub state and message queueing. This eliminates the need for sticky sessions at the load balancer, preventing would-be attackers from directing their attacks against the same server again and again.

### Additional Resources

*   [Backpressure and Unbounded Concurrency in Node.js](http://engineering.voxer.com/2013/09/16/backpressure-in-nodejs/) ([Voxer](http://voxer.com/))
*   [Building a Node.js Server That Won't Melt](https://hacks.mozilla.org/2013/01/building-a-node-js-server-that-wont-melt-a-node-js-holiday-season-part-5/) ([Mozilla](https://hacks.mozilla.org/))
*   [Security in Node.js](https://www.harrytorry.co.uk/security-in-node-js/) - see the "Denial of Service" section ([Harry Torry](https://www.harrytorry.co.uk))
*   [Slowloris DDoSAttacks](http://www.ddosattacks.biz/attacks/slowloris-ddos-attack-aka-slow-and-low/)

<docmeta value="DDOS139869" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="DDOS" name="displayName" class="calibre17"></docmeta>

# P 3 P

# P3P

### Background

P3P stands for the "Platform for Privacy Preferences", a browser/web standard designed to facilitate better consumer web privacy control. Currently (as of 2014), out of all the major browsers, it is only supported by Internet Explorer. It comes into play most often when dealing with legacy applications.

Many modern organizations are willfully ignoring P3P. Here's what whate [Facebook has to say](https://www.facebook.com/help/327993273962160/) on the subject:

> The organization that established P3P, the World Wide Web Consortium, suspended its work on this standard several years ago because most modern web browsers don't fully support P3P. As a result, the P3P standard is now out of date and doesn't reflect technologies that are currently in use on the web, so most websites currently don't have P3P policies.
> 
> See also: [`www.zdnet.com/blog/facebook/facebook-to-microsoft-p3p-is-outdated-what-else-ya-got/9332`](http://www.zdnet.com/blog/facebook/facebook-to-microsoft-p3p-is-outdated-what-else-ya-got/9332)

### Supporting P3P with Sails

But all that aside, sometimes you just have to support P3P anyways.

Fortunately, a few different modules exist that bring P3P support to Express and Sails by enabling the relevant P3P headers. To use one of these modules for handling P3P headers, install it from npm using the directions below, then open `config/http.js` in your project and configure it as a custom middleware. To do that, define your P3P middleware as "p3p", and add the string "p3p" to your `middleware.order` array wherever you'd like it to run in the middleware chain (a good place to put it might be right before `cookieParser`):

E.g. in `config/http.js`:

```
// .....
module.exports.http = {

  middleware: {

    p3p: require('p3p')(p3p.recommmended), // <==== set up the custom middleware here and named it "p3p"

    order: [
      'startRequestTimer',
      'p3p', // <============ configured the order of our "p3p" custom middleware here
      'cookieParser',
      'session',
      'bodyParser',
      'handleBodyParserError',
      'compress',
      'methodOverride',
      'poweredBy',
      '$custom',
      'router',
      'www',
      'favicon',
      '404',
      '500'
    ],
    // .....
  }
}; 
```

Check out the examples below for more guidance - and be sure and follow the links to see the docs for the module you're using for the latest information, comparative analysis of its features, any recent bug fixes, and advanced usage details.

##### Using [node-p3p](https://github.com/troygoode/node-p3p)

> `node-p3p` is open-source under the [MIT license](https://github.com/troygoode/node-p3p/blob/master/LICENSE).

```
# In your sails app
npm install p3p --save 
```

Then in the `middleware` config object in `config/http.js`:

```
 // ...
  // node-p3p provides a recommended compact privacy policy out of the box
  p3p: require('p3p')(require('p3p').recommended)
  // ... 
```

##### Using [lusca](https://github.com/krakenjs/lusca#luscap3pvalue)

> `lusca` is open-source under the [Apache license](https://github.com/krakenjs/lusca/blob/master/LICENSE.txt)

```
# In your sails app
npm install lusca --save 
```

Then in the `middleware` config object in `config/http.js`:

```
 // ...
  // "ABCDEF" ==> The compact privacy policy to use.
  p3p: require('lusca').p3p('ABCDEF')
  // ... 
```

### Additional Resources:

*   [Description of the P3P Project (Microsoft)](http://support.microsoft.com/kb/290333)
*   ["P3P Work suspended" (W3C)](http://www.w3.org/P3P/)
*   [P3P Compact Specification (CompactPrivacyPolicy.org)](http://compactprivacypolicy.org/compact_specification.htm)

<docmeta value="P3P183449" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="P3P" name="displayName" class="calibre17"></docmeta>

# Socket Hijacking

# Socket Hijacking

Unfortunately, cross-site request forgery attacks are not limited to the HTTP protocol. WebSocket hijacking (sometimes known as [CSWSH](http://www.christian-schneider.net/CrossSiteWebSocketHijacking.html)) is a commonly overlooked vulnerability in most realtime applications. Fortunately, since Sails treats both HTTP and WebSocket requests as first-class citizens, its built-in [CSRF protection](http://beta.sailsjs.org/#/documentation/concepts/Security/CSRF.html) and [configurable CORS rulesets](http://beta.sailsjs.org/#/documentation/concepts/Security/CORS.html) apply to both protocols.

You can prepare your Sails app against CSWSH attacks by enabling the built-in protection in [`config/csrf.js`](http://beta.sailsjs.org/#/documentation/anatomy/myApp/config/csrf.js.html) and ensuring that a `_csrf` token is sent with all relevant incoming socket requests. Additionally, if you're planning on allowing sockets to connect to your Sails app cross-origin (i.e. from a different domain, subdomain, or port) you'll want to configure your CORS settings accordingly. You can also define the `authorization` setting in [`config/sockets.js`](http://beta.sailsjs.org/#/documentation/anatomy/myApp/config/sockets.js.html) as a custom function which allows or denies the initial socket connection based on your needs.

#### Notes

*   CSWSH prevention is only a concern in scenarios where people use the same client application to connect sockets to multiple web services (e.g. cookies in a browser like Google Chrome can be used to connect a socket to Chase.com from both Chase.com and Horrible-Hacker-Site.com.)

<docmeta value="SocketHijacking397141" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Socket Hijacking" name="displayName" class="calibre17"></docmeta>

# Strict Transport Security

# HTTP Strict Transport Security

### Enabling STS

Implementing STS is actually very simple and [only takes a few lines of code](https://github.com/krakenjs/lusca/blob/master/lib/hsts.js). But better yet, a few different open-source modules exist that bring support for this feature to Express and Sails. To use one of these modules, install it from npm using the directions below, then open `config/http.js` in your project and [configure it as a custom middleware](http://beta.sailsjs.org/#/documentation/concepts/Middleware). The example(s) below cover basic usage and configuration. For more guidance and advanced usage details, be sure and follow the link to the docs.

##### Using [lusca](https://github.com/krakenjs/lusca#luscahstsoptions)

> `lusca` is open-source under the [Apache license](https://github.com/krakenjs/lusca/blob/master/LICENSE.txt)

```
# In your sails app
npm install lusca --save 
```

Then in the `middleware` config object in `config/http.js`:

```
 // ...
  // maxAge ==> Number of seconds strict transport security will stay in effect.
  strictTransportSecurity: require('lusca').hsts({ maxAge: 31536000 })
  // ... 
```

### Additional Resources

*   [HTTP Strict Transport Security (OWasp)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security)

<docmeta value="HSTSecurity397141" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Strict Transport Security" name="displayName" class="calibre17"></docmeta>

# XSS

# XSS

Cross-site scripting (XSS) is a type of attack in which a malicious agent manages to inject client-side JavaScript into your website, so that it runs in the trusted environment of your users' browsers.

### Additional Resources

*   [XSS (OWasp)](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS))
*   [XSS Prevention Cheatsheet](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet)

<docmeta value="XSS397141" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="XSS" name="displayName" class="calibre17"></docmeta>

# Services

# Services

## Overview

Services can be thought of as libraries which contain functions that you might want to use in many places of your application. For example, you might have an EmailService which wraps some default email message boilerplate code that you would want to use in many parts of your application. The main benefit of using services in Sails is that they are *globalized*--you don't have to use `require()` to access them.

## How do I create a service?

Simply save a Javascript file containing a function or object into your **api/services** folder. The filename will be used as the globally-accessible variable name for the service. For example, an email service might look something like this:

```
// EmailService.js - in api/services
module.exports = {

    sendInviteEmail: function(options) {

        var opts = {"type":"messages","call":"send","message":
            {
                "subject": "YourIn!",
                "from_email": "info@balderdash.co",
                "from_name": "AmazingStartupApp",
                "to":[
                    {"email": options.email, "name": options.name}
                ],
                "text": "Dear "+options.name+",\nYou're in the Beta! Click <insert link> to verify your account"
            }
        };

        myEmailSendingLibrary.send(opts);

    }
}; 
```

You can then use `EmailService` anywhere in your app:

```
// Somewhere in a controller
  EmailService.sendInviteEmail({email: 'test@test.com', name: 'test'}); 
```

<docmeta value="Services157331" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Services" name="displayName" class="calibre17"></docmeta>

# Testing

# Testing your code

## Preparation

For our test suite, we use [mocha](http://visionmedia.github.com/mocha/). Before you start building your test cases, you should first organise your `./test` directory structure, for example in the following way:

```
./myApp
├── api
├── assets
├── ...
├── test
│  ├── unit
│  │  ├── controllers
│  │  │  └── UsersController.test.js
│  │  ├── models
│  │  │  └── Users.test.js
│  │  └── ...
│  ├── fixtures
│  ├── ...
│  ├── bootstrap.test.js
│  └── mocha.opts
└── views 
```

### bootstrap.test.js

This file is useful when you want to execute some code before and after running your tests (e.g. lifting and lowering your sails application):

```
var Sails = require('sails');

before(function(done) {
  Sails.lift({
    // configuration for testing purposes
  }, function(err, sails) {
    if (err) return done(err);
    // here you can load fixtures, etc.
    done(err, sails);
  });
});

after(function(done) {
  // here you can clear fixtures, etc.
  sails.lower(done);
}); 
```

### mocha.opts

This file should contain mocha configuration as described here: [mocha.opts] ([`visionmedia.github.io/mocha/#mocha.opts`](http://visionmedia.github.io/mocha/#mocha.opts))

## Writing tests

Once you have prepared your directory you can start writing your unit tests.

./test/unit/models/Users.test.js

```
describe.only('UsersModel', function() {

  describe('#find()', function() {
    it('should check find function', function (done) {
      Users.find()
        .then(function(results) {
          // some tests
          done();
        })
        .catch(done);
    });
  });

}); 
```

#### Testing controllers

To test controller responses you can use [Supertest](https://github.com/visionmedia/supertest) library which provides several useful methods for testing HTTP requests.

./test/unit/controllers/UsersController.test.js

```
var request = require('supertest');

describe('UsersController', function() {

  describe('#login()', function() {
    it('should redirect to /mypage', function (done) {
      request(sails.hooks.http.app)
        .post('/users/login')
        .send({ name: 'test', password: 'test' })
        .expect(302)
        .expect('location','/mypage', done);
    });
  });

}); 
```

## Code coverage

Another popular method for testing your code is [Code Coverage](http://en.wikipedia.org/wiki/Code_coverage).

You can use [mocha](http://visionmedia.github.io/mocha/) and [istanbul](https://github.com/gotwarlost/istanbul) to check your code and prepare various coverage reports (HTML, Cobertura) which can be used in continuous integration services such as [Jenkins](http://jenkins-ci.org).

To test your code and prepare a simple HTML report run the following commands:

```
istanbul cover -x "**/config/**" _mocha -- --timeout 5000
istanbul report html 
```

<docmeta value="Testing765149" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Testing" name="displayName" class="calibre17"></docmeta>

# Upgrading

# Upgrading

> TODO: move this to the appropriate part of the docs (shouldn't show up in reference-- instead it should appear at the top of the other migration guide/changelog stuff in the "Support" section)

Sails v0.11 is finally here.

For the most part, running `sails lift` in an existing v0.9 project should **just work**. The core contributors have taken a number of steps to make the upgrade as easy as possible, and if you follow the deprecation messages in the console, you should do just fine.

Sails v0.11 comes with some big changes. The sections below provide a high level overview of what's changed, major bug fixes, enhancements and new features, as well as a basic tutorial on how to upgrade your v0.9.x Sails app to v0.11.

The Sails/Waterline communities have been extremely supportive to newer users throughout the beta. If you run into problems, please reach out for help in IRC, the Google Group and on Stack Overflow.

If you believe you've encountered an upgrade issue not addressed in this document, please let the core team know by sending a pull request to [this file on Github](https://github.com/balderdashy/sails-docs/edit/master/reference/Upgrading.md). If you don't know the answer to a question, explain the upgrade issue you've having in the appropriate section (or a new one), and someone will do their best to answer it/provide a migration strategy.

Thanks!

@mikermcneil

========================================

### Contents

|  | Jump to... |
| --- | --- |
|  | File Uploads |
|  | Blueprints |
|  | Policies |
|  | Associations |
|  | Pubsub |
|  | `.done()` vs. `.exec()` |
|  | Generators |
|  | Command-Line Tool |
|  | Custom Server Responses |
|  | Legacy Data in `sails-disk` |
|  | Validations |
|  | Adapter/Connections Configuration |
|  | Blueprints/Controllers Configuration |
|  | Layout Paths |

========================================

### File Uploads

The Connect multipart middleware [will soon be officially deprecated](http://www.senchalabs.org/connect/multipart.html). But since this module was used as the built-in HTTP body parser in Sails v0.9 and Express v3, this is a breaking change for v0.9 Sails projects relying on `req.files`.

By default in v0.11, Sails includes [`skipper`](http://github.com/balderdashy/skipper), a body parser which allows for streaming file uploads without buffering tmp files to disk. For run-of-the-mill file upload use cases, Skipper comes with bundled support for uploads to local disk (via [skipper-disk](https://github.com/balderdashy/skipper-disk)), but streaming uploads can be plugged in to any of its supported adapters.

For examples/documentation, please see the Skipper repository as well as the Sails documentation on `req.file()`.

#### Why?

A body parser's job is to parse the "body" of incoming multipart HTTP requests. Sometimes, that "body" includes text parameters, but sometimes, it includes file uploads.

Connect multipart is great code, and it supports both file uploads AND text parameters in multipart requests. But like most modules of its kind, it accomplishes this by buffering file uploads to disk. This can quickl

# Views

# Views

### Overview

In Sails, views are markup templates that are compiled *on the server* into HTML pages. In most cases, views are used as the response to an incoming HTTP request, e.g. to serve your home page.

Alternatively, a view can be compiled directly into an HTML string for use in your backend code (see [`sails.renderView()`](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md).) For instance, you might use this approach to send HTML emails, or to build big XML strings for use with a legacy API.

##### Creating a view

By default, Sails is configured to use EJS ([Embedded Javascript](http://embeddedjs.com/)) as its view engine. The syntax for EJS is highly conventional- if you've worked with php, asp, erb, gsp, jsp, etc., you'll immediately know what you're doing.

If you prefer to use a different view engine, there are a multitude of options. Sails supports all of the view engines compatible with [Express](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md) via [Consolidate](https://github.com/visionmedia/consolidate.js/).

Views are defined in your app's [`views/`](http://beta.sailsjs.org/#/documentation/anatomy/myApp/views) folder by default, but like all of the default paths in Sails, they are [configurable](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md). If you don't need to serve dynamic HTML pages at all (say, if you're building an API for a mobile app), you can remove the directory from your app.

##### Compiling a view

Anywhere you can access the `res` object (i.e. a controller action, custom response, or policy), you can use [`res.view`](http://beta.sailsjs.org/#/documentation/reference/res/res.view.html) to compile one of your views, then send the resulting HTML down to the user.

You can also hook up a view directly to a route in your `routes.js` file. Just indicate the relative path to the view from your app's `views/` directory. For example:

```
{
  'get /': {
    view: 'homepage'
  },
  'get /signup': {
    view: 'signupFlow/basicInfo'
  },
  'get /signup/password': {
    view: 'signupFlow/chooseAPassword'
  },
  // and so on.
} 
```

##### What about single-page apps?

If you are building a web application for the browser, part (or all) of your navigation may take place on the client; i.e. instead of the browser fetching a new HTML page each time the user navigates around, the client-side code preloads some markup templates which are then rendered in the user's browser without needing to hit the server again directly.

In this case, you have a couple of options for bootstrapping the single-page app:

*   Use a single view, e.g. `views/publicSite.ejs`. Advantages:
    *   You can use the view engine in Sails to pass data from the server directly into the HTML that will be rendered on the client. This is an easy way to get stuff like user data to your client-side javascript, without having to send AJAX/WebSocket requests from the client.
*   Use a single HTML page in your assets folder , e.g. `assets/index.html`. Advantages:
    *   Although you can't pass server-side data directly to the client this way, this approach allows you to further decouple the client and server-side parts of your application.
    *   Anything in your assets folder can be moved to a static CDN (like Cloudfront or CloudFlare), allowing you to take advantage of that provider's geographically distributed data centers to get your content closer to your users.

<docmeta value="Views426660" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Views" name="displayName" class="calibre17"></docmeta>

# Layouts

# Layouts

When building an app with many different pages, it can be helpful to extrapolate markup shared by several HTML files into a layout. This [reduces the total amount of code](http://en.wikipedia.org/wiki/Don't_repeat_yourself) in your project and helps you avoid making the same changes in multiple files down the road.

In Sails and Express, layouts are implemented by the view engines themselves. For instance, `jade` has its own layout system, with its own syntax.

For convenience, Sails bundles special support for layouts **when using the default view engine, EJS**. If you'd like to use layouts with a different view engine, check out that view engine's documentation to find the appropriate syntax.

### Creating Layouts

Sails layouts are special `.ejs` files in your app's `views/` folder you can use to "wrap" or "sandwich" other views. Layouts usually contain the preamble (e.g. `!DOCTYPE html<html><head>....</head><body>`) and conclusion (`</body></html`). Then the original view file is included using `<%- body %>`. Layouts are never used without a view- that would be like serving someone a bread sandwich.

Layout support for your app can be configured or disabled in [`config/views.js`](http://beta.sailsjs.org/#/documentation/anatomy/myApp/config/views.js.html), and can be overridden for a particular route or action by setting a special local called `layout`. By default, Sails will compile all views using the layout located at `views/layout.ejs`.

### Notes

> #### Why do layouts only work for EJS?
> 
> In Express 3, built-in support for layouts/partials was deprecated. Instead, developers are expected to rely on the view engines themselves to implement this features. (See [`github.com/balderdashy/sails/issues/494`](https://github.com/balderdashy/sails/issues/494) for more info on that.)
> 
> Since adopting Express 3, Sails has chosen to support the legacy `layouts` feature for convenience, backwards compatibility with Express 2.x and Sails 0.8.x apps, and in particular, familiarity for new community members coming from other MVC frameworks. As a result, layouts have only been tested with the default view engine (ejs).
> 
> If layouts aren’t your thing, or (for now) if you’re using a server-side view engine other than ejs, (e.g. Jade, handlebars, haml, dust) you’ll want to set `layout:false` in [`sails.config.views`](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.views.html), then rely on your view engine’s custom layout/partial support.

<docmeta value="Layouts870655" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Layouts" name="displayName" class="calibre17"></docmeta>

# Locals

# Locals

The variables accessible in a particular view are called `locals`. Locals represent server-side data that is *accessible* to your view-- locals are not actually *included* in the compiled HTML unless you explicitly reference them using special syntax provided by your view engine.

```
Logged in as <%= name="" %="">. 
```

##### Using locals in your views

The notation for accessing locals varies between view engines. In EJS, you use special template markup (e.g. `<%= someValue %>`) to include locals in your views.

There are three kinds of template tags in EJS:

*   `<%= someValue %>`
    *   HTML-escapes the `someValue` local, and then includes it as a string.
*   `<%- someRawHTML %>`
    *   Includes the `someRawHTML` local verbatim, without escaping it.
    *   Be careful! This tag can make you vulnerable to XSS attacks if you don't know what you're doing.
*   `<% if (!loggedIn) { %> <a>Logout</a> <% } %>`
    *   Runs the javascript inside the `<% ... %>` when the view is compiled.
    *   Useful for conditionals (`if`/`else`), and looping over data (`for`/`each`).

Here's an example of a view (`views/backOffice/profile.ejs`) using two locals, `user` and `corndogs`:

```
<div>
  <h1><%= user.name %>'s first view</h1>
  <h2>My corndog collection:</h2>
  <ul>
    <% _.each(corndogs, function (corndog) { %>
    <li><%= corndog.name %></li>
    <% }) %>
  </ul>
</div> 
```

> You might have noticed another local, `_`. By default, Sails passes down a few locals to your views automatically, including lodash (`_`).

If the data you wanted to pass down to this view was completely static, you don't necessarily need a controller- you could just hard-code the view and its locals in your `config/routes.js` file, i.e:

```
 // ...
  'get /profile': {
    view: 'backOffice/profile',
    locals: {
      user: {
        name: 'Frank',
        emailAddress: 'frank@enfurter.com'
      },
      corndogs: [
        { name: 'beef corndog' },
        { name: 'chicken corndog' },
        { name: 'soy corndog' }
      ]
    }
  },
  // ... 
```

On the other hand, in the more likely scenario that this data is dynamic, we'd need to use a controller action to load it from our models, then pass it to the view using the [res.view()](http://beta.sailsjs.org/#/documentation/reference/res/res.view.html) method.

Assuming we hooked up our route to one of our controller's actions (and our models were set up), we might send down our view like this:

```
// in api/controllers/UserController.js...

  profile: function (req, res) {
    // ...
    return res.view('backOffice/profile', {
      user: theUser,
      corndogs: theUser.corndogCollection
    });
  },
  // ... 
```

<docmeta value="Locals453748" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Locals" name="displayName" class="calibre17"></docmeta>

# Partials

# Partials

Sails uses `ejs-locals` in its view rendering code, so in your views you can do:

```
<%- partial ('foo.ejs') %> 
```

to render a partial located at `/views/foo.ejs`. All of your locals will be sent to the partial automatically.

the paths are relative to the view, that is loading the partial. So if you have a a user view at `/views/users/view.ejs` and want to load `/views/partials/widget.ejs` then you would use:

```
<%- partial ('../../partials/widget.ejs') %> 
```

One thing to note: partials are rendered synchronously, so they will block Sails from serving more requests until they're done loading. It's something to keep in mind while developing your app, especially if you anticipate a large number of connections.

NOTE: When using other templating languages than ejs, their syntax for loading partials or block, etc. will be used. Please refer to their documentation for more information on their syntax and conventions

<docmeta value="Partials610916" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Partials" name="displayName" class="calibre17"></docmeta>

# View Engines

# View Engines

The default view engine in Sails is [EJS](https://github.com/visionmedia/ejs).

##### Swapping out the view engine

To use a different view engine, you should use npm to install it in your project, then set `sails.config.views.engine` (in [`config/views.js`](http://beta.sailsjs.org/#/documentation/anatomy/myApp/config/views.js.html).)

For example, to switch to jade, run `npm install jade --save-dev`, then set `engine: 'jade'` in [`config/views.js`](http://beta.sailsjs.org/#/documentation/anatomy/myApp/config/views.js.html).

##### Supported view engines

*   [atpl](https://github.com/soywiz/atpl.js)
*   [dust](https://github.com/akdubya/dustjs) [(website)](http://akdubya.github.com/dustjs/) (.dust)
*   [eco](https://github.com/sstephenson/eco)
*   [ect](https://github.com/baryshev/ect) [(website)](http://ectjs.com/)
*   [ejs](https://github.com/visionmedia/ejs) (.ejs)
*   [haml](https://github.com/visionmedia/haml.js) [(website)](http://haml-lang.com/)
*   [haml-coffee](https://github.com/9elements/haml-coffee) [(website)](http://haml-lang.com/)
*   [handlebars](https://github.com/wycats/handlebars.js/) [(website)](http://handlebarsjs.com/) (.hbs)
*   [hogan](https://github.com/twitter/hogan.js) [(website)](http://twitter.github.com/hogan.js/)
*   [jade](https://github.com/visionmedia/jade) [(website)](http://jade-lang.com/) (.jade)
*   [jazz](https://github.com/shinetech/jazz)
*   [jqtpl](https://github.com/kof/node-jqtpl) [(website)](http://api.jquery.com/category/plugins/templates/)
*   [JUST](https://github.com/baryshev/just)
*   [liquor](https://github.com/chjj/liquor)
*   [lodash](https://github.com/bestiejs/lodash) [(website)](http://lodash.com/)
*   [mustache](https://github.com/janl/mustache.js)
*   [QEJS](https://github.com/jepso/QEJS)
*   [ractive](https://github.com/Rich-Harris/Ractive)
*   [swig](https://github.com/paularmstrong/swig) [(website)](http://paularmstrong.github.com/swig/)
*   [templayed](http://archan937.github.com/templayed.js/)
*   [toffee](https://github.com/malgorithms/toffee)
*   [underscore](https://github.com/documentcloud/underscore) [(website)](http://documentcloud.github.com/underscore/)
*   [walrus](https://github.com/jeremyruppel/walrus) [(website)](http://documentup.com/jeremyruppel/walrus/)
*   [whiskers](https://github.com/gsf/whiskers.js)

##### Adding new custom view engines

For instructions on adding support for a view engine not listed above, check out the [consolidate project](https://github.com/visionmedia/consolidate.js/blob/master/Readme.md#api) repository.

<docmeta value="ViewEngines339501" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="View Engines" name="displayName" class="calibre17"></docmeta>

# Extending Sails

# Extending Sails

There are currently three types of plugins in Sails:

*   **Generators** - for adding and overriding functionality in the Sails CLI
*   **Adapters** - for integrating Waterline (Sails' ORM) with new data sources, including databases, APIs, or even hardware.
*   **Hooks** - for overriding or injecting new low-level functionality in the Sails runtime

<docmeta value="extendingsails78468" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Extending Sails" name="displayName" class="calibre17"></docmeta>

# Adapters

# Adapters

### Status

##### Stability: [3](http://nodejs.org/api/documentation.html#documentation_stability_index) - Stable

The API has proven satisfactory, but cleanup in the underlying code may cause minor changes. Backwards-compatibility is guaranteed.

### What is an adapter?

Adapters expose **interfaces**, which imply a contract to implement certain functionality. This allows us to guarantee conventional usage patterns across multiple models, developers, apps, and even companies, making app code more maintainable, efficient, and reliable. Adapters are useful for integrating with databases, open APIs, internal/proprietary web services, or even hardware.

### What kind of things can I do in an adapter?

Adapters are mainly focused on providing model-contextualized CRUD methods. CRUD stands for create, read, update, and delete. In Sails/Waterline, we call these methods `create()`, `find()`, `update()`, and `destroy()`.

For example, a `MySQLAdapter` implements a `create()` method which, internally, calls out to a MySQL database using the specified table name and connection informtion and runs an `INSERT ...` SQL query.

In practice, your adapter can really do anything it likes-- any method you write will be exposed on the raw connection objects and any models which use them.

##### Class methods

Below, `class methods` refer to the static, or collection-oriented, functions available on the model itself, e.g. `User.create()` or `Menu.update()`. To add custom class methods to your model (beyond what is provided in the adapters it implements), define them as top-level key/function pairs in the model object.

##### Instance methods

`instance methods` on the other hand, (also known as object, or model, methods) refer to methods available on the individual result models themselves, e.g. `User.findOne(7).done(function (err, user) { user.someInstanceMethod(); });`. To add custom instance methods to your model (beyond what is provided in the adapters it implements), define them as key/function pairs in the `attributes` object of the model's definition.

##### DDL and auto-migrations

`DDL` stands for data-definition language, and is a common fixture of schema-oriented databases. In Sails, auto-migrations are supported out of the box. Since adapters for the most common SQL databases support `alter()`, they also support automatic schema migration! In your own adapter, if you write the `alter()` method, the same behavior will take effect. The feature is configurable using the `migrate` property, which can be set to `safe` (don't touch the schema, period), `drop` (recreate the tables every time the app starts), or `alter` (the default-- merge the schema in the apps' models with what is currently in the database).

<docmeta value="Adapters83669" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Adapters" name="displayName" class="calibre25"></docmeta>

<docmeta value="3" name="stabilityIndex" class="calibre17"></docmeta>

# Adapter List

# List of Available Adapters

This file is meant to be an up to date, comprehensive list of all of the adapters available for the Sails.js framework. If we missed one or you would like to add an adapter you made, just submit a Pull Request to this file, adding to the list.

### Officially Supported Adapters

##### sails-disk

[`github.com/balderdashy/sails-disk/`](https://github.com/balderdashy/sails-disk/)

Write to your computer's hard disk, or a mounted network drive. Not suitable for at-scale production deployments, but great for a small project, and essential for developing in environments where you may not always have a database set up. This adapter is bundled with Sails and works out of the box with zero configuration.

###### Interfaces implemented:

*   Semantic
*   Queryable
*   Streaming

##### sails-memory

[`github.com/balderdashy/sails-memory/`](https://github.com/balderdashy/sails-memory/)

Pretty much like Disk, but doesn't actually write to disk, so it's not persistent. Not suitable for at-scale production deployments, but useful when developing on systems with little or no disk space.

###### Interfaces implemented:

*   Semantic
*   Queryable
*   Streaming

##### sails-mysql

[`github.com/balderdashy/sails-mysql/`](https://github.com/balderdashy/sails-mysql/)

MySQL is the world's most popular relational database. [`en.wikipedia.org/wiki/MySQL`](http://en.wikipedia.org/wiki/MySQL)

###### Interfaces implemented:

*   Semantic
*   Queryable
*   Streaming
*   Migratable

##### sails-postgres

[`github.com/balderdashy/sails-postgresql/`](https://github.com/balderdashy/sails-postgresql/)

[PostgreSQL](http://en.wikipedia.org/wiki/PostgreSQL) is another popular relational database.

###### Interfaces implemented:

*   Semantic
*   Queryable
*   Streaming
*   Migratable

##### sails-mongo

[`github.com/balderdashy/sails-mongo/`](https://github.com/balderdashy/sails-mongo/)

[MongoDB](http://en.wikipedia.org/wiki/MongoDB) is the leading NoSQL database.

###### Interfaces implemented:

*   Semantic
*   Queryable
*   Streaming

##### sails-redis

[`github.com/balderdashy/sails-redis/`](https://github.com/balderdashy/sails-redis/)

[Redis](http://redis.io/) is an open source, BSD licensed, advanced key-value store.

###### Interfaces implemented:

*   Semantic
*   Queryable

### Community Supported Adapters

Have you written a Sails adapter? Submit a PR to this file and add it here!

<docmeta value="adapterList22829" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Available Adapters" name="displayName" class="calibre17"></docmeta>

# Custom Adapters

# Custom Adapters

### Overview

Sails makes it fairly easy to write your own adapter. Check out the [sails-boilerplate-repo](https://github.com/balderdashy/sails-adapter-boilerplate) to learn how

<docmeta value="customAdapters92223" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Custom Adapters" name="displayName" class="calibre17"></docmeta>

# Generators

# Generators

## Status

##### Stability: [2](http://nodejs.org/api/documentation.html#documentation_stability_index) - Unstable

The API is in the process of settling, but has not yet had sufficient real-world testing to be considered stable.

Backwards-compatibility will be maintained if reasonable.

### Purpose

What is my purpose in this world?

### old partial content from when spec was an itty bitty baby

Generators are designed to make it easier to customize the `sails new` and `sails generate` command-line tools, and provide better support for different Gruntfiles, configuration options, view engines, coffeescript, etc.

#### Structure

A generator has either:

(1) a `generate` method, or

(2) a `configure` + `render` method (render may be omitted in the simplest of cases)

Sails

```
 app (appPath + name)
        <- view
        <- folder
        <- jsonfile
        <- file

    api (appPath + name)
        <- controller
        <- model

    controller (appPath + template + name)
        <- file

    model (appPath + template + name)
        <- file

    view (appPath + template + name)
        <- file

    file (destination + name + template + data)

    jsonfile (destination + name + data)

    folder (destination + name) 
```

<docmeta value="Generators82739" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Generators" name="displayName" class="calibre25"></docmeta>

<docmeta value="2" name="stabilityIndex" class="calibre17"></docmeta>

# Custom Generators

# Custom Generators

### Overview

Here is some info on writing custom generators.

<docmeta value="customGenerators22840" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Custom Generators" name="displayName" class="calibre17"></docmeta>

# Generator List

# List of Available Adapters

This file is meant to be an up to date, comprehensive list of all of the generators available for the Sails.js framework. If we missed one or you would like to add a generator you've made, just submit a Pull Request to this file, adding to the list.

### Officially Supported Generators

#### sails-generate-generator

###### Github Repo

[`github.com/balderdashy/sails-generate-generator/`](https://github.com/balderdashy/sails-generate-generator/)

###### On NPM

'npm install sails-generate-generator`

###### Description

Generate the boilerplates to make your own generator.

### Community Supported Generators

<docmeta value="generatorList11719" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Available Generators" name="displayName" class="calibre17"></docmeta>

# Hooks

# Hooks

## Status

> ##### Stability: [2](http://nodejs.org/api/documentation.html#documentation_stability_index) - Unstable

The API is in the process of settling, but has not yet had sufficient real-world testing to be considered stable.

Backwards-compatibility will be maintained if reasonable.

Most of the non-essential Sails core has been pulled into hooks already. These hooks may eventually be pulled out into separate modules, or they may continue to live in the main Sails repo (like Connect middleware).

Custom hooks in userland are functional- specifiable as dependencies (`node_modules`) or by tossing them into a folder in your project. However, this process is not currently well-documented and backwards-compatibility is not guaranteed. Please check out the source for more details.

## Purpose

Hooks were introduced to Sails as part of major refactor designed to make the framework more modular and testable. Their primary purpose for now is to pull all but the most minimal functionality of Sails into independent modules. Eventually, this architecture will allow for built-in hooks to be overridden, and even new hooks to be mixed-in to projects (a proper plugin system).

**Original Proposal:** [`gist.github.com/mikermcneil/5746660`](https://gist.github.com/mikermcneil/5746660)

## Custom Hooks = Plugins?

Sort of! The goal is to make hooks powerful, and simple to work w/ for plugin developers, but also predictable, easy to distribute and install, and documented for end users.

**The hooks API is tentative**, and it is currently going through at least one more set of changes. We are quickly approaching the point where we can call this feature "Stable", prioritize backwards compatibilty, and limit API changes.

That said, you *can* write and distribute a custom hook today. If you're interested in the roadmap for the plugin system, or developing a plugin yourself, consider/check out the following tools at your disposal:

*   [Custom Generators](https://github.com/balderdashy/sails/blob/v0.11/bin/generators/README.md) :: coming in v0.11, useful for extending the Sails command-line interface (Stage 1 - Experimental)
*   [Custom Adapters](https://github.com/balderdashy/sails-docs/blob/0.9/api.adapter-interface.md) :: Since v0.8, useful for adding database support, API integrations, etc. (Stage 2 - Unstable, but approaching Stage 3)
*   [`sails` Core Events](https://gist.github.com/mikermcneil/5898598) :: Since v0.9, the `sails` object is an EventEmitter. (Stage 2 - Unstable, but approaching Stage 3)
*   Custom blueprint middlewares (coming in v0.11: Stage 1 - Experimental)
*   Custom API responses (coming in v0.11: Stage 2 - Unstable)
*   Custom route-level options (since v0.9, but changing in 0.10: Stage 2 - Unstable, but approaching Stage 3)
*   Custom configuration (since v0.7)
*   Custom "shadow routes" (since v0.7, merged in hooks in v0.9)

## FAQ

> If you have a question that isn't covered here, please feel free to send a PR adding it to this section (even if you don't have the answer!)

<docmeta value="Hooks74998" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Hooks" name="displayName" class="calibre25"></docmeta>

<docmeta value="2" name="stabilityIndex" class="calibre17"></docmeta>