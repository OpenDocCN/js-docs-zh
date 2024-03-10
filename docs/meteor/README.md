# Meteor 中文文档

> 来源：[Meteor 中文文档](http://docs.meteorhub.org/#/basic/)

***Meteor 是一个用于构建现代应用的超简单的开发环境。之前用最好的工具，都需要花费数周时间的事情，现在用 Meteor，只需数小时。***

Web 最初被设计成和 70 年代大型机工作方式相同。服务器渲染完成一个页面并通过网络发送到终端。无论用户做了什么，服务端都会重新渲染整个页面。 这种模式在 Web 上持续了十多年。从而产生了 LAMP，Rails，Django，PHP。

但是现在，一个非常牛的团队，他们有着充足的预算和长远的规划，使我们可以构建运行在客户端的 javascript 应用。这些应用拥有出色的界面。 无需刷新网页，而是实时响应：任何一个客户端产生变化都会立即反映到所有人的屏幕。

他们经过一番努力推出了 Meteor。Meteor 使构建现代应用变得简单而有趣。用一个周末的时间或是在黑客马拉松上，你就可以构建一个完整的应用。 你无需再准备服务器资源，或是部署 API 到云端，不用管理数据库或是纠缠于 ORM 层，不用再在 javascript 和 Ruby 之间来回切换，也不用再广播无效数据给客户端。

# 快速开始!

## 快速开始!

Meteor 支持 [OS X, Windows, and Linux](https://github.com/meteor/meteor/wiki/Supported-Platforms).

用 Windows? [下载官方安装包](https://install.meteor.com/windows).

用 OS X 或是 Linux? 通过命令行安装 Meteor 官方最新版：

```
$ curl https://install.meteor.com/ | sh 
```

Windows 安装包支持 Windows 7, Windows 8.1, Windows Server 2008, 和 Windows Server 2012。命令行安装，支持 Mac OS X 10.7 (Lion) 及其以上版本, Linux x86 和 x86_64 架构.

安装完成之后，创建一个项目：

```
$ meteor create myapp 
```

在本地运行：

```
$ cd myapp
$ meteor
# Meteor server running on: http://localhost:3000/ 
```

然后，打开一个命令行窗口，发布到线上（我们提供的一个免费服务器）

```
$ meteor deploy myapp.meteor.com 
```

# Meteor 的理念

## Meteor 的理念

*   *Data on the Wire*. Meteor 不在网络上发送 HTML。服务器发送数据，让客户端来渲染它。

*   *One Language.* Meteor 使你可以用 javascript 来实现应用的客户端和服务端

*   *Database Everywhere*. 在客户端和服务端，你可以使用相同的方法来使用数据库。

*   *Latency Compensation*. 在客户端，Meteor 预加载数据以及本地模拟的模式使它看起来就像是服务端方法调用立即返回了一样。

*   *Full Stack Reactivity*. 在 Meteor 中，默认是实时性的。所有层面，从数据库到模板，都会在需要的时候自动更新。

*   *Embrace the Ecosystem*. Meteor 是开源的，并且集成了现有的开源工具和框架。

*   *Simplicity Equals Productivity*. 让事情看起来简单最好的方式就是让它真的成为简单地事。Meteor 的主要功能点的 API 非常干净、经典漂亮。

# 学习资源

## 学习资源

有很多社区资源可以帮助你开发应用。如果你对 Meteor 感兴趣，希望你能参与其中！

教程

快速开始[Meteor 官方教程](https://www.meteor.com/install)!

Stack Overflow

对于技术问题，提问、寻找答案最好的去处就是 [Stack Overflow](http://stackoverflow.com/questions/tagged/meteor). 确保给你的问题添加 `meteor` 标签。

论坛

访问 [Meteor discussion forums](https://forums.meteor.com)宣布项目，寻求帮助，讨论社区或是讨论核心模块的变动。

GitHub

核心代码在[GitHub](http://github.com/meteor/meteor)上. 如果你会写代码或是提 issue，我们很想得到你的帮助。 对于如何开始，请先阅读[Contributing to Meteor](https://github.com/meteor/meteor/wiki/Contributing-to-Meteor)

# 命令行工具

## 命令行工具

#### `meteor help`

获取 `meteor` 命令行使用帮助。运行 `meteor help` 会列出`meteor`所有命令。运行`meteor help &lt;command&gt;`会打印出关于`meteor &lt;command&gt;`的详细帮助。

#### `meteor create &lt;name&gt;`

创建一个名为`&lt;name&gt;`的子目录，并在里面新建一个 Meteor 应用。

#### `meteor run`

使用 Meteor 本地开发服务器运行当前应用，地址为：[`localhost:3000`](http://localhost:3000)

#### `meteor debug`

附带着 Node Inspector 运行项目，这样你就可以一步一步跟踪服务端代码。更多信息查看`meteor debug`

#### `meteor deploy &lt;site&gt;`

打包你的应用，并发布到`&lt;site&gt;`。如果你发布到`&lt;your app&gt;.meteor.com`，Meteor 提供免费的主机，只要`&lt;your app&gt;`的名字还未被其他人使用。

#### `meteor update`

升级 Meteor 到最新发布版，然后（如果`meteor update`是在一个应用目录中执行的）升级当前项目使用的包到最新兼容版。

#### `meteor add`

添加一个包（或多个）到 Meteor 项目中。要查询可用的包，使用`meteor search`命令。

#### `meteor remove`

移除之前添加到项目中的包。查看项目使用的包列表，用`meteor list` 命令。

#### `meteor mongo`

打开一个 MongoDB shell 来查看、操作数据库中的集合。注意：你必须先运行当前应用(在另外的命令行)，`meteor mongo`才能连接到应用的数据库

#### `meteor reset`

重置当前项目为初始状态。移除所有本地数据。

如果你经常使用`meteor reset` ，但是又不想丢失一些初始数据，考虑使用`Meteor.startup` 在服务第一次启动时重建这些数据。

```
if (Meteor.isServer) {
  Meteor.startup(function () {
    if (Rooms.find().count() === 0) {
      Rooms.insert({name: "Initial room"});
    }
  });
} 
```

# 文件结构

## 文件结构

对于该如何组织应用的文件结构，Meteor 是非常灵活的。它会自动加载所有文件，所以不需要再用`&lt;script&gt;` 或 `&lt;link&gt;`标签来引入 javascript 和 CSS。

### 文件的默认加载

如果某个文件在下面提到的特殊文件夹之外，Meteor 会做如下处理：

1.  HTML 模板编译完成后发送到客户端。详细信息参见 the templates section。
2.  CSS 文件发送到客户端。在生产模式下，会自动合并、压缩。
3.  Javascript 被加载到客户端和服务端。可以使用`Meteor.isClient` 和 `Meteor.isServer` 来控制特定代码的运行位置。

如果你想更好的控制哪些 javascript 代码加载到客户端或是服务端，可以使用下面列出的特殊文件夹。

### 特殊文件夹

#### `/client`

`/client`文件夹中所有文件都只发送到客户端。用来放置 HTML，CSS 和 UI 相关的 javascript 代码。

#### `/server`

`/server`文件夹中所有文件都只提供给服务端使用，不会发送到客户端。用来放置不应该被客户端看到的敏感逻辑和数据。

#### `/public`

`/public`文件夹中的文件会原样发送到客户端。用来放置资源，例如：图片。假设有张图片`/public/background.png`， 在 HTML 中用 `&lt;img src='/background.png'/&gt;`引用或是在 CSS 中用 `background-image: url(/background.png)` 引用。 注意图片 URL 中不包含`/public`。

#### `/private`

`/private`文件夹中的文件只能由服务端代码通过`Assets` API 来获取，客户端无法获取。

更多关于文件加载顺序和特殊文件夹的说明参见 Structuring Your App section

# 开发手机应用

## 开发手机应用

当你用 Meteor 开发完成 web app 之后，只需几个命令，就可以轻松地构建一个 native 包装，并发布到 Google Play Store 或是 iOS App Store。 我们用了很大精力，使相同的包和 API 在桌面端和移动端都能工作，所以你无须担心大量的移动应用开发相关的边界情况。

### 安装手机 SDKs

安装 Android 或 ios 开发工具：

```
meteor install-sdk android     # for Android
meteor install-sdk ios         # for iOS 
```

### 添加平台

添加相关平台到你的应用：

```
meteor add-platform android    # for Android
meteor add-platform ios        # for iOS 
```

### 运行模拟器

```
meteor run android             # for Android
meteor run ios                 # for iOS 
```

### 在设备上运行

```
meteor run android-device      # for Android
meteor run ios-device          # for iOS 
```

### 配置 APP 图标和 metadata

可以用特殊的文件`mobile-config.js`配置 APP 的图标、标题、版本号、启动画面以及其他 metadata。

更多关于 Meteor 对移动端的支持参见[GitHub wiki page](https://github.com/meteor/meteor/wiki/Meteor-Cordova-Phonegap-integration)。