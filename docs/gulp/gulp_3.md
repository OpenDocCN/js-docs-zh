# 编写插件

# 编写插件

如果你打算自己写一个 Gulp 插件，为了节约你的时间，你可以先完整地阅读下这个文档。

*   导览 (必读)
*   使用 buffer
*   使用 stream 来处理
*   测试

## 它要做什么？

### 流式处理文件对象（Streaming file objects）

gulp 插件总是返回一个 [object mode](http://nodejs.org/api/stream.html#stream_object_mode) 形式的 stream 来做这些事情：

1.  接收 [vinyl File 对象](http://github.com/wearefractal/vinyl)
2.  输出 [vinyl File 对象](http://github.com/wearefractal/vinyl)

这通常被叫做 [transform streams](http://nodejs.org/api/stream.html#stream_class_stream_transform_1) (有时候也叫做 through streams)。transform streams 是可读又可写的，它会对传给它的对象做一些转换的操作。

### 修改文内容

Vinyl 文件可以通过三种不同形式来访问文件内容：

*   Streams
*   Buffers
*   空 (null) - 对于删除, 清理, 等操作来说，会很有用，因为这时候内容是不需要处理的。

## 有用的资源

*   [File object](https://github.com/wearefractal/gulp-util/#new-fileobj)
*   [PluginError](https://github.com/gulpjs/gulp-util#new-pluginerrorpluginname-message-options)
*   [event-stream](https://github.com/dominictarr/event-stream)
*   [BufferStream](https://github.com/nfroidure/BufferStream)
*   [gulp-util](https://github.com/wearefractal/gulp-util)

## 插件范例

*   [sindresorhus' gulp plugins](https://github.com/search?q=%40sindresorhus+gulp-)
*   [Fractal's gulp plugins](https://github.com/search?q=%40wearefractal+gulp-)
*   [gulp-replace](https://github.com/lazd/gulp-replace)

## 关于 stream

如果你不熟悉 stream，你可以阅读这些来

*   [`github.com/substack/stream-handbook`](https://github.com/substack/stream-handbook) (必读)
*   [`nodejs.org/api/stream.html`](http://nodejs.org/api/stream.html)

其他的一些为 gulp 创建的和使用的，但又并非通过 stream 去处理的库，在 npm 上都会被打上 [gulpfriendly](https://npmjs.org/browse/keyword/gulpfriendly) 标签。

# 指导

# 指导

> 这个指导实际上不是必须的，但是我们强烈建议每一个人来遵守。因为没有人会喜欢用一个不好的插件。这个指导能在某种意义上确保你的插件能很好的适应 gulp，以此来让你的生活变得更将轻松。

编写插件 > 指导

1.  你的插件不应该去做一些现有 node 模块已经能很容易做到的事情

2.  比如：删除一个文件夹并不需要做成一个 gulp 插件，在 task 里使用一个类似 [del](https://github.com/sindresorhus/del) 这样的插件即可。

3.  只是为了封装而封装一些的东西进去，这只会增加很多低质量的插件到生态中，这不符合 gulp 的期望。
4.  gulp 插件都是以文件为基础操作的，如果你发现你正在把一些很复杂的操作塞进 stream 中去，那么，请直接写一个 node 模块就好。
5.  一个好的 gulp 插件例子像是 gulp-coffee，coffee-script 模块并不能直接和 vinyl 做很好的适配，因此，才去封装它来使用相应的功能，并且将一些比较痛苦的操作抽象出来，做成更简单的 gulp 插件来使用。

6.  你的插件应该只做**一件事**，并且做好。

7.  避免使用配置选项，使得你的插件能胜任不同场合的任务。

8.  比如：一个 JS 压缩插件不应该有一个加头部的选项

9.  你的插件不能去做一些其他插件做的事：

10.  不应该去拼接，用 [gulp-concat](https://github.com/wearefractal/gulp-concat) 去做

11.  不应该去增加头部，用 [gulp-header](https://github.com/godaddy/gulp-header) 去做
12.  不应该去增加尾部，用 [gulp-footer](https://github.com/godaddy/gulp-footer) 去做
13.  如果是一个常用的可选的操作，那么，请在文档中注明你的插件通常和其他某个插件一起使用
14.  在你的插件中使用其他的插件，这能大大减少你的代码量，并保证生态系统的稳定。

15.  你的插件必须被**测试过**

16.  测试一个插件很简单，你甚至不需要 gulp 就能测试

17.  参考其他的插件是怎么做的

18.  在 `package.json` 中增加一个名为 `gulpplugin` 的关键字，这可以让它能在我们的搜索中出现

19.  不要再 stream 里面抛出错误

20.  你应该以触发 **error** 事件来代替

21.  如果你在 stream 外面遇到错误，比如在创建 stream 时候发现错误的配置选项等，那么你应该抛出它。

22.  错误需要加上以你插件名字作为前缀

23.  比如： `gulp-replace: Cannot do regexp replace on a stream`

24.  使用 gulp-util 的 [PluginError](https://github.com/gulpjs/gulp-util#new-pluginerrorpluginname-message-options) 类来完成它

25.  `file.contents` 的类型需要总是在输入输出中保持一致

26.  如果 file.contents 为空 (不可读) 请将他忽略，并传过去

27.  如果 file.contents 是一个 stream，但是你不支持，那么请触发一个错误

    *   不要把 stream 硬转成 buffer 来使你的插件支持 stream，这会引发很严重的问题。
28.  在你处理完成之前，不要将 `file` 传到下游去

29.  使用 [`file.clone()`](https://github.com/wearefractal/vinyl#clone) 来复制一个文件或者创建另一个以此为基础的文件
30.  使用我们 模块推荐页 上列举的模块来让你的开发更加轻松
31.  不要把 `gulp` 作为一个依赖

32.  使用 gulp 来测试你的插件的工作流这的确很酷，但请务必确保你将它放到 devDependency 中

33.  在你的插件中依赖 gulp，这意味着安装你的插件的用户将会重新安装一遍 gulp 以及所有它所依赖的东西。
34.  没有任何理由说明你需要将 gulp 写到你的插件代码中去，如果你发现你必须这么做，那么请开一个 issue，我们会帮你解决。

## 为什么这些指导这么严格？

gulp 的目标是为了让用户觉得简单，通过提供一些严格的指导，我们就能提供一致并且高质量的生态系统给大家。不过，这确实给插件作者增加了一些需要考虑的东西，但是也确保了后面的问题会更少。

### 如果我不遵守这些，会发生什么？

npm 对每个人来说是免费的，你可以开发任何你想要开发的东西出来，并且不需要遵守这个规定。我们承诺测试机制将会很快建立起来，并且加入我们的插件搜索中。如果你坚持不遵守插件导览，那么这会反应在我们的打分/排名系统上，人们都会更加喜欢去使用一个 "更加 gulp" 的插件。

### 一个插件大概会是怎么样的？

```
// through2 是一个对 node 的 transform streams 简单封装
var through = require('through2');
var gutil = require('gulp-util');
var PluginError = gutil.PluginError;

// 常量
const PLUGIN_NAME = 'gulp-prefixer';

function prefixStream(prefixText) {
  var stream = through();
  stream.write(prefixText);
  return stream;
}

// 插件级别函数 (处理文件)
function gulpPrefixer(prefixText) {

  if (!prefixText) {
    throw new PluginError(PLUGIN_NAME, 'Missing prefix text!');
  }
  prefixText = new Buffer(prefixText); // 预先分配

  // 创建一个让每个文件通过的 stream 通道
  return through.obj(function(file, enc, cb) {
    if (file.isNull()) {
      // 返回空文件
      cb(null, file);
    }
    if (file.isBuffer()) {
      file.contents = Buffer.concat([prefixText, file.contents]);
    }
    if (file.isStream()) {
      file.contents = file.contents.pipe(prefixStream(prefixText));
    }

    cb(null, file);

  });

};

// 暴露（export）插件主函数
module.exports = gulpPrefixer; 
```

# 使用 buffer

# 使用 buffer

> 这里有些关于如何创建一个使用 buffer 来处理的插件的有用信息。

编写插件 > 使用 buffer

## 使用 buffer

如果你的插件依赖着一个基于 buffer 处理的库，你可能会选择让你的插件以 buffer 的形式来处理 file.contents。让我们来实现一个在文件头部插入额外文本的插件：

```
var through = require('through2');
var gutil = require('gulp-util');
var PluginError = gutil.PluginError;

// 常量
const PLUGIN_NAME = 'gulp-prefixer';

// 插件级别的函数（处理文件）
function gulpPrefixer(prefixText) {
  if (!prefixText) {
    throw new PluginError(PLUGIN_NAME, 'Missing prefix text!');
  }

  prefixText = new Buffer(prefixText); // 提前分配

  // 创建一个 stream 通道，以让每个文件通过
  var stream = through.obj(function(file, enc, cb) {
    if (file.isStream()) {
      this.emit('error', new PluginError(PLUGIN_NAME, 'Streams are not supported!'));
      return cb();
    }

    if (file.isBuffer()) {
      file.contents = Buffer.concat([prefixText, file.contents]);
    }

    // 确保文件进入下一个 gulp 插件
    this.push(file);

    // 告诉 stream 引擎，我们已经处理完了这个文件
    cb();
  });

  // 返回文件 stream
  return stream;
};

// 导出插件主函数
module.exports = gulpPrefixer; 
```

上述的插件可以这样使用：

```
var gulp = require('gulp');
var gulpPrefixer = require('gulp-prefixer');

gulp.src('files/**/*.js')
  .pipe(gulpPrefixer('prepended string'))
  .pipe(gulp.dest('modified-files')); 
```

## 处理 stream

不幸的是，当 gulp.src 如果是以 stream 的形式，而不是 buffer，那么，上面的插件就会报错。如果可以，你也应该让他支持 stream 形式。请查看使用 Stream 处理 获取更多信息。

## 一些基于 buffer 的插件

*   [gulp-coffee](https://github.com/wearefractal/gulp-coffee)
*   [gulp-svgmin](https://github.com/ben-eb/gulp-svgmin)
*   [gulp-marked](https://github.com/lmtm/gulp-marked)
*   [gulp-svg2ttf](https://github.com/nfroidure/gulp-svg2ttf)

# 使用 Stream 处理

# 使用 Stream 处理

> 极力推荐让你所写的插件支持 stream。这里有一些关于让插件支持 stream 的一些有用信息。
> 
> 请确保使用处理错误的最佳实践，并且加入一行代码，使得 gulp 能在转换内容的期间在捕获到第一个错误时候正确报出错误。

编写插件 > 编写以 stream 为基础的插件

## 使用 stream 处理

让我们来实现一个用于在文件头部插入一些文本的插件，这个插件支持 file.contents 所有可能的形式。

```
var through = require('through2');
var gutil = require('gulp-util');
var PluginError = gutil.PluginError;

// 常量
const PLUGIN_NAME = 'gulp-prefixer';

function prefixStream(prefixText) {
  var stream = through();
  stream.write(prefixText);
  return stream;
}

// 插件级别函数 (处理文件)
function gulpPrefixer(prefixText) {
  if (!prefixText) {
    throw new PluginError(PLUGIN_NAME, 'Missing prefix text!');
  }

  prefixText = new Buffer(prefixText); // 预先分配

  // 创建一个让每个文件通过的 stream 通道
  var stream = through.obj(function(file, enc, cb) {
    if (file.isBuffer()) {
      this.emit('error', new PluginError(PLUGIN_NAME, 'Buffers not supported!'));
      return cb();
    }

    if (file.isStream()) {
      // 定义转换内容的 streamer
      var streamer = prefixStream(prefixText);
      // 从 streamer 中捕获错误，并发出一个 gulp 的错误
      streamer.on('error', this.emit.bind(this, 'error'));
      // 开始转换
      file.contents = file.contents.pipe(streamer);
    }

    // 确保文件进去下一个插件
    this.push(file);
    // 告诉 stream 转换工作完成
    cb();
  });

  // 返回文件 stream
  return stream;
}

// 暴露（export）插件的主函数
module.exports = gulpPrefixer; 
```

上面的插件可以像这样使用：

```
var gulp = require('gulp');
var gulpPrefixer = require('gulp-prefixer');

gulp.src('files/**/*.js', { buffer: false })
  .pipe(gulpPrefixer('prepended string'))
  .pipe(gulp.dest('modified-files')); 
```

## 一些使用 stream 的插件

*   [gulp-svgicons2svgfont](https://github.com/nfroidure/gulp-svgiconstosvgfont)

# 测试

# 测试

> 测试是保证你的插件质量的唯一途径。这能使你的用户有信心去使用，且能让你更加轻松。

编写插件 > 测试

## 工具

大多数的插件使用 [mocha](https://github.com/visionmedia/mocha)，[should](https://github.com/visionmedia/should.js) 以及 [event-stream](https://github.com/dominictarr/event-stream) 来做测试。下面的例子也将会使用这些工具。

## 测试插件的流处理（streaming）模式

```
var assert = require('assert');
var es = require('event-stream');
var File = require('vinyl');
var prefixer = require('../');

describe('gulp-prefixer', function() {
  describe('in streaming mode', function() {

    it('should prepend text', function(done) {

      // 创建伪文件
      var fakeFile = new File({
        contents: es.readArray(['stream', 'with', 'those', 'contents'])
      });

      // 创建一个 prefixer 流（stream）
      var myPrefixer = prefixer('prependthis');

      // 将伪文件写入
      myPrefixer.write(fakeFile);

      // 等文件重新出来
      myPrefixer.once('data', function(file) {
        // 确保它以相同的方式出来
        assert(file.isStream());

        // 缓存内容来确保它已经被处理过（加前缀内容）
        file.contents.pipe(es.wait(function(err, data) {
          // 检查内容
          assert.equal(data, 'prependthisstreamwiththosecontents');
          done();
        }));
      });

    });

  });
}); 
```

## 测试插件的 buffer 模式

```
var assert = require('assert');
var es = require('event-stream');
var File = require('vinyl');
var prefixer = require('../');

describe('gulp-prefixer', function() {
  describe('in buffer mode', function() {

    it('should prepend text', function(done) {

      // 创建伪文件
      var fakeFile = new File({
        contents: new Buffer('abufferwiththiscontent')
      });

      // 创建一个 prefixer 流（stream）
      var myPrefixer = prefixer('prependthis');

      // 将伪文件写入
      myPrefixer.write(fakeFile);

      // 等文件重新出来
      myPrefixer.once('data', function(file) {
        // 确保它以相同的方式出来
        assert(file.isBuffer());

        // 检查内容
        assert.equal(file.contents.toString('utf8'), 'prependthisabufferwiththiscontent');
        done();
      });

    });

  });
}); 
```

## 一些拥有高质量的测试用例的插件

*   [gulp-cat](https://github.com/ben-eb/gulp-cat/blob/master/test.js)
*   [gulp-concat](https://github.com/wearefractal/gulp-concat/blob/master/test/main.js)