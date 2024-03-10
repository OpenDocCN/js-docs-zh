# 向导

# 支持平台

# 支持的平台

以下的平台是 Electron 目前支持的：

### OS X

对于 OS X 系统仅有 64 位的二进制文档，支持的最低版本是 OS X 10.8。

### Windows

仅支持 Windows 7 及其以后的版本，之前的版本中是不能工作的。

对于 Windows 提供 `x86` 和 `amd64` (x64) 版本的二进制文件。需要注意的是 `ARM` 版本的 Windows 目前尚不支持.

### Linux

预编译的 `ia32`(`i686`) 和 `x64`(`amd64`) 版本 Electron 二进制文件都是在 Ubuntu 12.04 下编译的，`arm` 版的二进制文件是在 ARM v7（硬浮点 ABI 与 Debian Wheezy 版本的 NEON）下完成的。

预编译二进制文件是否能够运行，取决于其中是否包括了编译平台链接的库，所以只有 Ubuntu 12.04 可以保证正常工作，但是以下的平台也被证实可以运行 Electron 的预编译版本：

*   Ubuntu 12.04 及更新
*   Fedora 21
*   Debian 8

# 分发应用

# 应用部署

为了使用 Electron 部署你的应用程序，你存放应用程序的文件夹需要叫做 `app` 并且需要放在 Electron 的 资源文件夹下（在 OS X 中是指 `Electron.app/Contents/Resources/`，在 Linux 和 Windows 中是指 `resources/`） 就像这样：

在 OS X 中:

```js
electron/Electron.app/Contents/Resources/app/
├── package.json
├── main.js
└── index.html 
```

在 Windows 和 Linux 中:

```js
electron/resources/app
├── package.json
├── main.js
└── index.html 
```

然后运行 `Electron.app` （或者 Linux 中的 `electron`，Windows 中的 `electron.exe`）, 接着 Electron 就会以你的应用程序的方式启动。`electron` 文件夹将被部署并可以分发给最终的使用者。

## 将你的应用程序打包成一个文件

除了通过拷贝所有的资源文件来分发你的应用程序之外，你可以可以通过打包你的应用程序为一个 [asar](https://github.com/atom/asar) 库文件以避免暴露你的源代码。

为了使用一个 `asar` 库文件代替 `app` 文件夹，你需要修改这个库文件的名字为 `app.asar` ， 然后将其放到 Electron 的资源文件夹下，然后 Electron 就会试图读取这个库文件并从中启动。 如下所示：

在 OS X 中:

```js
electron/Electron.app/Contents/Resources/
└── app.asar 
```

在 Windows 和 Linux 中:

```js
electron/resources/
└── app.asar 
```

更多的细节请见 Application packaging.

## 更换名称与下载二进制文件

在使用 Electron 打包你的应用程序之后，你可能需要在分发给用户之前修改打包的名字。

### Windows

你可以将 `electron.exe` 改成任意你喜欢的名字，然后可以使用像 [rcedit](https://github.com/atom/rcedit) 编辑它的 icon 和其他信息。

### OS X

你可以将 `Electron.app` 改成任意你喜欢的名字，然后你也需要修改这些文件中的 `CFBundleDisplayName`， `CFBundleIdentifier` 以及 `CFBundleName` 字段。 这些文件如下：

*   `Electron.app/Contents/Info.plist`
*   `Electron.app/Contents/Frameworks/Electron Helper.app/Contents/Info.plist`

你也可以重命名帮助应用程序以避免在应用程序监视器中显示 `Electron Helper`， 但是请确保你已经修改了帮助应用的可执行文件的名字。

一个改过名字的应用程序的构造可能是这样的：

```js
MyApp.app/Contents
├── Info.plist
├── MacOS/
│   └── MyApp
└── Frameworks/
    ├── MyApp Helper EH.app
    |   ├── Info.plist
    |   └── MacOS/
    |       └── MyApp Helper EH
    ├── MyApp Helper NP.app
    |   ├── Info.plist
    |   └── MacOS/
    |       └── MyApp Helper NP
    └── MyApp Helper.app
        ├── Info.plist
        └── MacOS/
            └── MyApp Helper 
```

### Linux

你可以将 `electron` 改成任意你喜欢的名字。

## 通过重编译源代码来更换名称

通过修改产品名称并重编译源代码来更换 Electron 的名称也是可行的。 你需要修改 `atom.gyp` 文件并彻底重编译一次。

### grunt 打包脚本

手动检查 Electron 代码并重编译是很复杂晦涩的，因此有一个 Grunt 任务可以自动的处理 这些内容 [grunt-build-atom-shell](https://github.com/paulcbetts/grunt-build-atom-shell).

这个任务会自动的处理编辑 `.gyp` 文件，从源代码进行编译，然后重编译你的应用程序的本地 Node 模块以匹配这个新的可执行文件的名称。

# 提交应用到 Mac App Store

# Mac App Store 应用提交向导

自从 v0.34.0, Electron 就允许提交应用包到 Mac App Store (MAS) . 这个向导提供的信息有 : 如何提交应用和 MAS 构建的限制.

**注意:** 从 v0.36.0，当应用成为沙箱之后，会有一个 bug 阻止 GPU 进程开启 , 所以在这个 bug 修复之前，建议使用 v0.35.x .更多查看 [issue #3871](https://github.com/electron/electron/issues/3871) .

**注意:** 提交应用到 Mac App Store 需要参加 [Apple Developer Program](https://developer.apple.com/support/compare-memberships/) , 这需要花钱.

## 如何提交

下面步骤介绍了一个简单的提交应用到商店方法.然而，这些步骤不能保证你的应用被 Apple 接受；你仍然需要阅读 Apple 的 [Submitting Your App](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/SubmittingYourApp/SubmittingYourApp.html) 关于如何满足 Mac App Store 要求的向导.

### 获得证书

为了提交应用到商店，首先需要从 Apple 获得一个证书.可以遵循 [existing guides](https://github.com/nwjs/nw.js/wiki/Mac-App-Store-%28MAS%29-Submission-Guideline#first-steps).

### App 签名

获得证书之后，你可以使用 Application Distribution 打包你的应用, 然后前往提交你的应用.这个步骤基本上和其他程序一样，但是这 key 一个个的标识 Electron 的每个依赖.

首先，你需要准备 2 个授权文件 .

`child.plist`:

```js
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>com.apple.security.app-sandbox</key>
    <true/>
    <key>com.apple.security.inherit</key>
    <true/>
  </dict>
</plist> 
```

`parent.plist`:

```js
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>com.apple.security.app-sandbox</key>
    <true/>
  </dict>
</plist> 
```

然后使用下面的脚本标识你的应用 :

```js
#!/bin/bash 
# Name of your app.
APP="YourApp"
# The path of you app to sign.
APP_PATH="/path/to/YouApp.app"
# The path to the location you want to put the signed package.
RESULT_PATH="~/Desktop/$APP.pkg"
# The name of certificates you requested.
APP_KEY="3rd Party Mac Developer Application: Company Name (APPIDENTITY)"
INSTALLER_KEY="3rd Party Mac Developer Installer: Company Name (APPIDENTITY)"

FRAMEWORKS_PATH="$APP_PATH/Contents/Frameworks"

codesign --deep -fs "$APP_KEY" --entitlements child.plist "$FRAMEWORKS_PATH/Electron Framework.framework/Versions/A"
codesign --deep -fs "$APP_KEY" --entitlements child.plist "$FRAMEWORKS_PATH/$APP Helper.app/"
codesign --deep -fs "$APP_KEY" --entitlements child.plist "$FRAMEWORKS_PATH/$APP Helper EH.app/"
codesign --deep -fs "$APP_KEY" --entitlements child.plist "$FRAMEWORKS_PATH/$APP Helper NP.app/"
if [ -d "$FRAMEWORKS_PATH/Squirrel.framework/Versions/A" ]; then
  # Signing a non-MAS build.
  codesign --deep -fs "$APP_KEY" --entitlements child.plist "$FRAMEWORKS_PATH/Mantle.framework/Versions/A"
  codesign --deep -fs "$APP_KEY" --entitlements child.plist "$FRAMEWORKS_PATH/ReactiveCocoa.framework/Versions/A"
  codesign --deep -fs "$APP_KEY" --entitlements child.plist "$FRAMEWORKS_PATH/Squirrel.framework/Versions/A"
fi
codesign -fs "$APP_KEY" --entitlements parent.plist "$APP_PATH"

productbuild --component "$APP_PATH" /Applications --sign "$INSTALLER_KEY" "$RESULT_PATH" 
```

如果你是 OS X 下的应用沙箱使用新手，应当仔细阅读 Apple 的 [Enabling App Sandbox](https://developer.apple.com/library/ios/documentation/Miscellaneous/Reference/EntitlementKeyReference/Chapters/EnablingAppSandbox.html) 来有一点基础,然后向授权文件添加你的应用需要的许可 keys .

### 上传你的应用并检查提交

在签名应用之后，可以使用应用 Loader 来上传到 iTunes 链接处理 , 确保在上传之前你已经 [created a record](https://developer.apple.com/library/ios/documentation/LanguagesUtilities/Conceptual/iTunesConnect_Guide/Chapters/CreatingiTunesConnectRecord.html). 然后你能 [submit your app for review](https://developer.apple.com/library/ios/documentation/LanguagesUtilities/Conceptual/iTunesConnect_Guide/Chapters/SubmittingTheApp.html).

## MAS 构建限制

为了让你的应用沙箱满足所有条件，在 MAS 构建的时候，下面的模块被禁用了 :

*   `crashReporter`
*   `autoUpdater`

并且下面的行为也改变了:

*   一些机子的视频采集功能无效.
*   某些特征不可访问.
*   Apps 不可识别 DNS 改变.

也由于应用沙箱的使用方法，应用可以访问的资源被严格限制了 ; 阅读更多信息 [App Sandboxing](https://developer.apple.com/app-sandboxing/) .

## Electron 使用的加密算法

取决于你所在地方的国家和地区 , Mac App Store 或许需要记录你应用的加密算法 , 甚至要求你提交一个 U.S 加密注册(ERN) 许可的复印件.

Electron 使用下列加密算法:

*   AES - [NIST SP 800-38A](http://csrc.nist.gov/publications/nistpubs/800-38a/sp800-38a.pdf), [NIST SP 800-38D](http://csrc.nist.gov/publications/nistpubs/800-38D/SP-800-38D.pdf), [RFC 3394](http://www.ietf.org/rfc/rfc3394.txt)
*   HMAC - [FIPS 198-1](http://csrc.nist.gov/publications/fips/fips198-1/FIPS-198-1_final.pdf)
*   ECDSA - ANS X9.62–2005
*   ECDH - ANS X9.63–2001
*   HKDF - [NIST SP 800-56C](http://csrc.nist.gov/publications/nistpubs/800-56C/SP-800-56C.pdf)
*   PBKDF2 - [RFC 2898](https://tools.ietf.org/html/rfc2898)
*   RSA - [RFC 3447](http://www.ietf.org/rfc/rfc3447)
*   SHA - [FIPS 180-4](http://csrc.nist.gov/publications/fips/fips180-4/fips-180-4.pdf)
*   Blowfish - [`www.schneier.com/cryptography/blowfish/`](https://www.schneier.com/cryptography/blowfish/)
*   CAST - [RFC 2144](https://tools.ietf.org/html/rfc2144), [RFC 2612](https://tools.ietf.org/html/rfc2612)
*   DES - [FIPS 46-3](http://csrc.nist.gov/publications/fips/fips46-3/fips46-3.pdf)
*   DH - [RFC 2631](https://tools.ietf.org/html/rfc2631)
*   DSA - [ANSI X9.30](http://webstore.ansi.org/RecordDetail.aspx?sku=ANSI+X9.30-1%3A1997)
*   EC - [SEC 1](http://www.secg.org/sec1-v2.pdf)
*   IDEA - "On the Design and Security of Block Ciphers" book by X. Lai
*   MD2 - [RFC 1319](http://tools.ietf.org/html/rfc1319)
*   MD4 - [RFC 6150](https://tools.ietf.org/html/rfc6150)
*   MD5 - [RFC 1321](https://tools.ietf.org/html/rfc1321)
*   MDC2 - [ISO/IEC 10118-2](https://www.openssl.org/docs/manmaster/crypto/mdc2.html)
*   RC2 - [RFC 2268](https://tools.ietf.org/html/rfc2268)
*   RC4 - [RFC 4345](https://tools.ietf.org/html/rfc4345)
*   RC5 - [`people.csail.mit.edu/rivest/Rivest-rc5rev.pdf`](http://people.csail.mit.edu/rivest/Rivest-rc5rev.pdf)
*   RIPEMD - [ISO/IEC 10118-3](http://webstore.ansi.org/RecordDetail.aspx?sku=ISO%2FIEC%2010118-3:2004)

如何获取 ERN 许可, 可看这篇文章: [How to legally submit an app to Apple’s App Store when it uses encryption (or how to obtain an ERN)](https://carouselapps.com/2015/12/15/legally-submit-app-apples-app-store-uses-encryption-obtain-ern/).

# 打包应用

# 应用打包

为舒缓 Windows 下路径名过长的问题[issues](https://github.com/joyent/node/issues/6960)， 也略对 `require` 加速以及简单隐匿你的源代码，你可以通过极小的源代码改动将你的应用打包成 [asar](https://github.com/atom/asar)。

## 生成 `asar` 包

[asar](https://github.com/atom/asar) 是一种将多个文件合并成一个文件的类 tar 风格的归档格式。 Electron 可以无需解压，即从其中读取任意文件内容。

参照如下步骤将你的应用打包成 `asar`：

### 1\. 安装 asar

```js
$ npm install -g asar 
```

### 2\. 用 `asar pack` 打包

```js
$ asar pack your-app app.asar 
```

## 使用 `asar` 包

在 Electron 中有两类 APIs：Node.js 提供的 Node API 和 Chromium 提供的 Web API。 这两种 API 都支持从 `asar` 包中读取文件。

### Node API

由于 Electron 中打了特别补丁， Node API 中如 `fs.readFile` 或者 `require` 之类 的方法可以将 `asar` 视之为虚拟文件夹，读取 `asar` 里面的文件就和从真实的文件系统中读取一样。

例如，假设我们在 `/path/to` 文件夹下有个 `example.asar` 包：

```js
$ asar list /path/to/example.asar
/app.js
/file.txt
/dir/module.js
/static/index.html
/static/main.css
/static/jquery.min.js 
```

从 `asar` 包读取一个文件：

```js
const fs = require('fs');
fs.readFileSync('/path/to/example.asar/file.txt'); 
```

列出 `asar` 包中根目录下的所有文件：

```js
const fs = require('fs');
fs.readdirSync('/path/to/example.asar'); 
```

使用 `asar` 包中的一个模块：

```js
require('/path/to/example.asar/dir/module.js'); 
```

你也可以使用 `BrowserWindow` 来显示一个 `asar` 包里的 web 页面：

```js
const BrowserWindow = require('electron').BrowserWindow;
var win = new BrowserWindow({width: 800, height: 600});
win.loadURL('file:///path/to/example.asar/static/index.html'); 
```

### Web API

在 Web 页面里，用 `file:` 协议可以获取 `asar` 包中文件。和 Node API 一样，视 `asar` 包如虚拟文件夹。

例如，用 `$.get` 获取文件:

```js
<script> var $ = require('./jquery.min.js');
$.get('file:///path/to/example.asar/file.txt', function(data) {
  console.log(data);
}); </script> 
```

### 像“文件”那样处理 `asar` 包

有些场景，如：核查 `asar` 包的校验和，我们需要像读取“文件”那样读取 `asar` 包的内容(而不是当成虚拟文件夹)。 你可以使用内置的 `original-fs` （提供和 `fs` 一样的 API）模块来读取 `asar` 包的真实信息。

```js
var originalFs = require('original-fs');
originalFs.readFileSync('/path/to/example.asar'); 
```

## Node API 缺陷

尽管我们已经尽了最大努力使得 `asar` 包在 Node API 下的应用尽可能的趋向于真实的目录结构，但仍有一些底层 Node API 我们无法保证其正常工作。

### `asar` 包是只读的

`asar` 包中的内容不可更改，所以 Node APIs 里那些可以用来修改文件的方法在对待 `asar` 包时都无法正常工作。

### Working Directory 在 `asar` 包中无效

尽管 `asar` 包是虚拟文件夹，但其实并没有真实的目录架构对应在文件系统里，所以你不可能将 working Directory 设置成 `asar` 包里的一个文件夹。将 `asar` 中的文件夹以 `cwd` 形式作为参数传入一些 API 中也会报错。

### API 中的额外“开箱”

大部分 `fs` API 可以无需解压即从 `asar` 包中读取文件或者文件的信息，但是在处理一些依赖真实文件路径的底层 系统方法时，Electron 会将所需文件解压到临时目录下，然后将临时目录下的真实文件路径传给底层系统方法使其正 常工作。 对于这类 API，耗费会略多一些。

以下是一些需要额外解压的 API：

*   `child_process.execFile`
*   `child_process.execFileSync`
*   `fs.open`
*   `fs.openSync`
*   `process.dlopen` - `require`native 模块时用到

### `fs.stat` 获取的 stat 信息不可靠

对 `asar` 包中的文件取 `fs.stat`，返回的 `Stats` 对象不是精确值，因为这些文件不是真实存在于文件系 统里。所以除了文件大小和文件类型以外，你不应该依赖 `Stats` 对象的值。

### 执行 `asar` 包中的程序

Node 中有一些可以执行程序的 API，如 `child_process.exec`，`child_process.spawn` 和 `child_process.execFile` 等， 但只有 `execFile` 可以执行 `asar` 包中的程序。

因为 `exec` 和 `spawn` 允许 `command` 替代 `file` 作为输入，而 `command` 是需要在 shell 下执行的，目前没有 可靠的方法来判断 `command` 中是否在操作一个 `asar` 包中的文件，而且即便可以判断，我们依旧无法保证可以在无任何 副作用的情况下替换 `command` 中的文件路径。

## 打包时排除文件

如上所述，一些 Node API 会在调用时将文件解压到文件系统中，除了效率问题外，也有可能引起杀毒软件的注意！

为解决这个问题，你可以在生成 `asar` 包时使用 `--unpack` 选项来排除一些文件，使其不打包到 `asar` 包中， 下面是如何排除一些用作共享用途的 native 模块的方法：

```js
$ asar pack app app.asar --unpack *.node 
```

经过上述命令后，除了生成的 `app.asar` 包以外，还有一个包含了排除文件的 `app.asar.unpacked` 文件夹， 你需要将这个文件夹一起拷贝，提供给用户。

# 使用 Node 原生模块

# 使用原生模块

Electron 同样也支持原生模块，但由于和官方的 Node 相比使用了不同的 V8 引擎，如果你想编译原生模块，则需要手动设置 Electron 的 headers 的位置。

## 原生 Node 模块的兼容性

当 Node 开始换新的 V8 引擎版本时，原生模块可能“坏”掉。为确保一切工作正常，你需要检查你想要使用的原生模块是否被 Electron 内置的 Node 支持。你可以在[这里](https://github.com/electron/electron/releases)查看 Electron 内置的 Node 版本，或者使用 `process.version` (参考：[快速入门](https://github.com/electron/electron/blob/master/docs/tutorial/quick-start.md))查看。

考虑到 [NAN](https://github.com/nodejs/nan/) 可以使你的开发更容易对多版本 Node 的支持，建议使用它来开发你自己的模块。你也可以使用 [NAN](https://github.com/nodejs/nan/) 来移植旧的模块到新的 Nod e 版本，以使它们可以在新的 Electron 下良好工作。

## 如何安装原生模块

如下三种方法教你安装原生模块：

### 最简单方式

最简单的方式就是通过 [`electron-rebuild`](https://github.com/paulcbetts/electron-rebuild) 包重新编译原生模块，它帮你自动完成了下载 headers、编译原生模块等步骤：

```js
npm install --save-dev electron-rebuild

# 每次运行"npm install"时，也运行这条命令
./node_modules/.bin/electron-rebuild

# 在 windows 下如果上述命令遇到了问题，尝试这个：
.\node_modules\.bin\electron-rebuild.cmd 
```

### 通过 npm 安装

你当然也可以通过 `npm` 安装原生模块。大部分步骤和安装普通模块时一样，除了以下一些系统环境变量你需要自己操作：

```js
export npm_config_disturl=https://atom.io/download/atom-shell
export npm_config_target=0.33.1
export npm_config_arch=x64
export npm_config_runtime=electron
HOME=~/.electron-gyp npm install module-name 
```

### 通过 node-gyp 安装

你需要告诉 `node-gyp` 去哪下载 Electron 的 headers，以及下载什么版本：

```js
$ cd /path-to-module/
$ HOME=~/.electron-gyp node-gyp rebuild --target=0.29.1 --arch=x64 --dist-url=https://atom.io/download/atom-shell 
```

`HOME=~/.electron-gyp` 设置去哪找开发时的 headers。

`--target=0.29.1` 设置了 Electron 的版本

`--dist-url=...` 设置了 Electron 的 headers 的下载地址

`--arch=x64` 设置了该模块为适配 64 位操作系统而编译

# 主进程调试

浏览器窗口的开发工具仅能调试渲染器的进程脚本（比如 web 页面）。为了提供一个可以调试主进程 的方法，Electron 提供了 `--debug` 和 `--debug-brk` 开关。

## 命令行开关

使用如下的命令行开关来调试 Electron 的主进程：

### `--debug=[port]`

当这个开关用于 Electron 时，它将会监听 V8 引擎中有关 `port` 的调试器协议信息。 默认的 `port` 是 `5858`。

### `--debug-brk=[port]`

就像 `--debug` 一样，但是会在第一行暂停脚本运行。

## 使用 node-inspector 来调试

**备注：** Electron 目前对 node-inspector 支持的不是特别好， 如果你通过 node-inspector 的 console 来检查 `process` 对象，主进程就会崩溃。

### 1\. 确认你已经安装了 [node-gyp 所需工具](https://github.com/nodejs/node-gyp#installation)

### 2\. 安装 [node-inspector](https://github.com/node-inspector/node-inspector)

```js
$ npm install node-inspector 
```

### 3\. 安装 `node-pre-gyp` 的一个修订版

```js
$ npm install git+https://git@github.com/enlight/node-pre-gyp.git#detect-electron-runtime-in-find 
```

### 4\. 为 Electron 重新编译 `node-inspector` `v8` 模块（将 target 参数修改为你的 Electron 的版本号）

```js
$ node_modules/.bin/node-pre-gyp --target=0.36.2 --runtime=electron --fallback-to-build --directory node_modules/v8-debug/ --dist-url=https://atom.io/download/atom-shell reinstall
$ node_modules/.bin/node-pre-gyp --target=0.36.2 --runtime=electron --fallback-to-build --directory node_modules/v8-profiler/ --dist-url=https://atom.io/download/atom-shell reinstall 
```

[How to install native modules][how-to-install-native-modules].

### 5\. 打开 Electron 的调试模式

你也可以用调试参数来运行 Electron ：

```js
$ electron --debug=5858 your/app 
```

或者，在第一行暂停你的脚本：

```js
$ electron --debug-brk=5858 your/app 
```

### 6\. 使用 Electron 开启 [node-inspector](https://github.com/node-inspector/node-inspector) 服务

```js
$ ELECTRON_RUN_AS_NODE=true path/to/electron.exe node_modules/node-inspector/bin/inspector.js 
```

### 7\. 加载调试器界面

在 Chrome 中打开 [`127.0.0.1:8080/debug?ws=127.0.0.1:8080&port=5858`](http://127.0.0.1:8080/debug?ws=127.0.0.1:8080&port=5858)

# 使用 Selenium 和 WebDriver

引自[ChromeDriver - WebDriver for Chrome](https://sites.google.com/a/chromium.org/chromedriver/):

> WebDriver 是一款开源的支持多浏览器的自动化测试工具。它提供了操作网页、用户输入、JavaScript 执行等能力。ChromeDriver 是一个实现了 WebDriver 与 Chromium 联接协议的独立服务。它也是由开发了 Chromium 和 WebDriver 的团队开发的。

为了能够使 `chromedriver` 和 Electron 一起正常工作，我们需要告诉它 Electron 在哪，并且让它相信 Electron 就是 Chrome 浏览器。

## 通过 WebDriverJs 配置

[WebDriverJs](https://code.google.com/p/selenium/wiki/WebDriverJs) 是一个可以配合 WebDriver 做测试的 node 模块，我们会用它来做个演示。

### 1\. 启动 ChromeDriver

首先，你要下载 `chromedriver`，然后运行以下命令：

```js
$ ./chromedriver
Starting ChromeDriver (v2.10.291558) on port 9515
Only local connections are allowed. 
```

记住 `9515` 这个端口号，我们后面会用到

### 2\. 安装 WebDriverJS

```js
$ npm install selenium-webdriver 
```

### 3\. 联接到 ChromeDriver

在 Electron 下使用 `selenium-webdriver` 和其平时的用法并没有大的差异，只是你需要手动设置连接 ChromeDriver，以及 Electron 的路径：

```js
const webdriver = require('selenium-webdriver');

var driver = new webdriver.Builder()
  // "9515" 是 ChromeDriver 使用的端口
  .usingServer('http://localhost:9515')
  .withCapabilities({
    chromeOptions: {
      // 这里设置 Electron 的路径
      binary: '/Path-to-Your-App.app/Contents/MacOS/Atom',
    }
  })
  .forBrowser('electron')
  .build();

driver.get('http://www.google.com');
driver.findElement(webdriver.By.name('q')).sendKeys('webdriver');
driver.findElement(webdriver.By.name('btnG')).click();
driver.wait(function() {
 return driver.getTitle().then(function(title) {
   return title === 'webdriver - Google Search';
 });
}, 1000);

driver.quit(); 
```

## 通过 WebdriverIO 配置

[WebdriverIO](http://webdriver.io/) 也是一个配合 WebDriver 用来测试的 node 模块

### 1\. 启动 ChromeDriver

首先，下载 `chromedriver`，然后运行以下命令：

```js
$ chromedriver --url-base=wd/hub --port=9515
Starting ChromeDriver (v2.10.291558) on port 9515
Only local connections are allowed. 
```

记住 `9515` 端口，后面会用到

### 2\. 安装 WebdriverIO

```js
$ npm install webdriverio 
```

### 3\. 连接到 ChromeDriver

```js
const webdriverio = require('webdriverio');
var options = {
    host: "localhost", // 使用 localhost 作为 ChromeDriver 服务器
    port: 9515,        // "9515"是 ChromeDriver 使用的端口
    desiredCapabilities: {
        browserName: 'chrome',
        chromeOptions: {
          binary: '/Path-to-Your-App/electron', // Electron 的路径
          args: [/* cli arguments */]           // 可选参数，类似：'app=' + /path/to/your/app/
        }
    }
};

var client = webdriverio.remote(options);

client
    .init()
    .url('http://google.com')
    .setValue('#q', 'webdriverio')
    .click('#btnG')
    .getTitle().then(function(title) {
        console.log('Title was: ' + title);
    })
    .end(); 
```

## 工作流程

无需重新编译 Electron，只要把 app 的源码放到 [Electron 的资源目录](https://github.com/electron/electron/blob/master/docs/tutorial/application-distribution.md) 里就可直接开始测试了。

当然，你也可以在运行 Electron 时传入参数指定你 app 的所在文件夹。这步可以免去你拷贝－粘贴你的 app 到 Electron 的资源目录。

# 使用开发人员工具扩展

# DevTools 扩展

为了使调试更容易，Electron 原生支持 [Chrome DevTools Extension](https://developer.chrome.com/extensions/devtools)。

对于大多数 DevTools 的扩展，你可以直接下载源码，然后通过 `BrowserWindow.addDevToolsExtension` API 加载它们。Electron 会记住已经加载了哪些扩展，所以你不需要每次创建一个新 window 时都调用 `BrowserWindow.addDevToolsExtension` API。

**注：React DevTools 目前不能直接工作，详情留意 [`github.com/electron/electron/issues/915`](https://github.com/electron/electron/issues/915)**

例如，要用[React DevTools Extension](https://github.com/facebook/react-devtools)，你得先下载他的源码：

```js
$ cd /some-directory
$ git clone --recursive https://github.com/facebook/react-devtools.git 
```

参考 [`react-devtools/shells/chrome/Readme.md`](https://github.com/facebook/react-devtools/blob/master/shells/chrome/Readme.md) 来编译这个扩展源码。

然后你就可以在任意页面的 DevTools 里加载 React DevTools 了，通过控制台输入如下命令加载扩展：

```js
const BrowserWindow = require('electron').remote.BrowserWindow;
BrowserWindow.addDevToolsExtension('/some-directory/react-devtools/shells/chrome'); 
```

要卸载扩展，可以调用 `BrowserWindow.removeDevToolsExtension` API (扩展名作为参数传入)，该扩展在下次打开 DevTools 时就不会加载了：

```js
BrowserWindow.removeDevToolsExtension('React Developer Tools'); 
```

## DevTools 扩展的格式

理论上，Electron 可以加载所有为 chrome 浏览器编写的 DevTools 扩展，但它们必须存放在文件夹里。那些以 `crx` 形式发布的扩展是不能被加载的，除非你把它们解压到一个文件夹里。

## 后台运行(background pages)

Electron 目前并不支持 chrome 扩展里的后台运行(background pages)功能，所以那些依赖此特性的 DevTools 扩展在 Electron 里可能无法正常工作。

## `chrome.*` APIs

有些 chrome 扩展使用了 `chrome.*`APIs，而且这些扩展在 Electron 中需要额外实现一些代码才能使用，所以并不是所有的这类扩展都已经在 Electron 中实现完毕了。

考虑到并非所有的 `chrome.*`APIs 都实现完毕，如果 DevTools 正在使用除了 `chrome.devtools.*` 之外的其它 APIs，这个扩展很可能无法正常工作。你可以通过报告这个扩展的异常信息，这样做方便我们对该扩展的支持。

# 使用 Pepper Flash 插件

Electron 现在支持 Pepper Flash 插件。要在 Electron 里面使用 Pepper Flash 插件，你需 要手动设置 Pepper Flash 的路径和在你的应用里启用 Pepper Flash。

## 保留一份 Flash 插件的副本

在 OS X 和 Linux 上，你可以在 Chrome 浏览器的 `chrome://plugins` 页面上找到 Pepper Flash 的插件信息。插件的路径和版本会对 Election 对其的支持有帮助。你也可以把插件 复制到另一个路径以保留一份副本。

## 添加插件在 Electron 里的开关

你可以直接在命令行中用 `--ppapi-flash-path` 和 `ppapi-flash-version` 或者 在 app 的准备事件前调用 `app.commandLine.appendSwitch` 这个 method。同时， 添加 `browser-window` 的插件开关。 例如：

```js
// Specify flash path. 设置 flash 路径
// On Windows, it might be /path/to/pepflashplayer.dll
// On OS X, /path/to/PepperFlashPlayer.plugin
// On Linux, /path/to/libpepflashplayer.so
app.commandLine.appendSwitch('ppapi-flash-path', '/path/to/libpepflashplayer.so');

// Specify flash version, for example, v17.0.0.169 设置版本号
app.commandLine.appendSwitch('ppapi-flash-version', '17.0.0.169');

app.on('ready', function() {
  mainWindow = new BrowserWindow({
    'width': 800,
    'height': 600,
    'web-preferences': {
      'plugins': true
    }
  });
  mainWindow.loadURL('file://' + __dirname + '/index.html');
  // Something else
}); 
```

## 使用 `<webview>` 标签启用插件

在 `<webview>` 标签里添加 `plugins` 属性。

```js
<webview src="http://www.adobe.com/software/flash/about/" plugins></webview> 
```

# 使用 Widevine CDM 插件

在 Electron ，你可以使用 Widevine CDM 插件装载 Chrome 浏览器 .

## 获取插件

Electron 没有为 Widevine CDM 插件 配制许可 reasons, 为了获得它，首先需要安装官方的 chrome 浏览器，这匹配了体系架构和 Electron 构建使用的 chrome 版本 .

**注意:** Chrome 浏览器的主要版本必须和 Electron 使用的版本一样，否则插件不会有效，虽然 `navigator.plugins` 会显示你已经安装了它 .

### Windows & OS X

在 Chrome 浏览器中打开 `chrome://components/` ，找到 `WidevineCdm` 并且确定它更新到最新版本，然后你可以从 `APP_DATA/Google/Chrome/WidevineCDM/VERSION/_platform_specific/PLATFORM_ARCH/` 路径找到所有的插件二进制文件 .

`APP_DATA` 是系统存放数据的地方，在 Windows 上它是 `%LOCALAPPDATA%`, 在 OS X 上它是 `~/Library/Application Support`. `VERSION` 是 Widevine CDM 插件的版本字符串, 类似 `1.4.8.866`. `PLATFORM` 是 `mac` 或 `win`. `ARCH` 是 `x86` 或 `x64`.

在 Windows，必要的二进制文件是 `widevinecdm.dll` and `widevinecdmadapter.dll`, 在 OS X ，它们是 `libwidevinecdm.dylib` 和 `widevinecdmadapter.plugin`. 你可以将它们复制到任何你喜欢的地方，但是它们必须要放在一起.

### Linux

在 Linux ，Chrome 浏览器将插件的二进制文件装载在一起 , 你可以在 `/opt/google/chrome` 下找到,文件名是 `libwidevinecdm.so` 和 `libwidevinecdmadapter.so`.

## 使用插件

在获得了插件文件后，你可以使用 `--widevine-cdm-path` 命令行开关来将 `widevinecdmadapter` 的路径传递给 Electron , 插件版本使用 `--widevine-cdm-version` 开关.

**注意:** 虽然只有 `widevinecdmadapter` 的二进制文件传递给了 Electron, `widevinecdm` 二进制文件应当放在它的旁边.

必须在 `app` 模块的 `ready` 事件触发之前使用命令行开关，并且 page 使用的插件必须激活.

示例代码 :

```js
// You have to pass the filename of `widevinecdmadapter` here, it is
// * `widevinecdmadapter.plugin` on OS X,
// * `libwidevinecdmadapter.so` on Linux,
// * `widevinecdmadapter.dll` on Windows.
app.commandLine.appendSwitch('widevine-cdm-path', '/path/to/widevinecdmadapter.plugin');
// The version of plugin can be got from `chrome://plugins` page in Chrome.
app.commandLine.appendSwitch('widevine-cdm-version', '1.4.8.866');

var mainWindow = null;
app.on('ready', function() {
  mainWindow = new BrowserWindow({
    webPreferences: {
      // The `plugins` have to be enabled.
      plugins: true
    }
  })
}); 
```

## 验证插件

为了验证插件是否工作，你可以使用下面的方法 :

*   打开开发者工具查看是否 `navigator.plugins` 包含了 Widevine CDM 插件.
*   打开 `https://shaka-player-demo.appspot.com/` 加载一个使用 `Widevine` 的 manifest.
*   打开 [`www.dash-player.com/demo/drm-test-area/`](http://www.dash-player.com/demo/drm-test-area/), 检查是否界面输出 `bitdash uses Widevine in your browser`, 然后播放 video.