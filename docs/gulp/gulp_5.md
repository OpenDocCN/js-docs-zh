# gulp 技巧集

# gulp 技巧集

*   整合 streams 来处理错误
*   删除文件和文件夹
*   使用 watchify 加速 browserify 编译
*   增量编译打包，包括处理整所涉及的所有文件
*   将 buffer 变为 stream (内存中的内容)
*   在 gulp 中运行 Mocha 测试
*   仅仅传递更改过的文件
*   从命令行传递参数
*   只重新编译被更改过的文件
*   每个文件夹生成单独一个文件
*   串行方式运行任务
*   拥有实时重载（live-reloading）和 CSS 注入的服务器
*   通过 stream 工厂来共享 stream
*   指定一个新的 cwd (当前工作目录)
*   分离任务到多个文件中
*   使用外部配置文件
*   在一个任务中使用多个文件来源
*   Browserify + Uglify2 和 sourcemaps
*   Browserify + Globs
*   同时输出一个压缩过和一个未压缩版本的文件
*   改变版本号以及创建一个 git tag
*   Swig 以及 YAML front-matter 模板

# 整合 streams 来处理错误

# 整合 streams 来处理错误

默认情况下，在 stream 中发生一个错误的话，它会被直接抛出，除非已经有一个时间监听器监听着 `error` 时间。 这在处理一个比较长的管道操作的时候会显得比较棘手。

通过使用 [stream-combiner2](https://github.com/substack/stream-combiner2)，你可以将一系列的 stream 合并成一个，这意味着，你只需要在你的代码中一个地方添加监听器监听 `error` 时间就可以了。

这里是一个在 gulpfile 中使用它的例子：

```
var combiner = require('stream-combiner2');
var uglify = require('gulp-uglify');
var gulp = require('gulp');

gulp.task('test', function() {
  var combined = combiner.obj([
    gulp.src('bootstrap/js/*.js'),
    uglify(),
    gulp.dest('public/bootstrap')
  ]);

  // 任何在上面的 stream 中发生的错误，都不会抛出，
  // 而是会被监听器捕获
  combined.on('error', console.error.bind(console));

  return combined;
}); 
```

# 删除文件和文件夹

# 删除文件和文件夹

你也许会想要在编译文件之前删除一些文件。由于删除文件和文件内容并没有太大关系，所以，我们没必要去用一个 gulp 插件。最好的一个选择就是使用一个原生的 node 模块。

因为 [`del`](https://github.com/sindresorhus/del) 模块支持多个文件以及 [globbing](https://github.com/sindresorhus/multimatch#globbing-patterns)，因此，在这个例子中，我们将使用它来删除文件：

```
$ npm install --save-dev gulp del 
```

假想有如下的文件结构：

```
.
├── dist
│   ├── report.csv
│   ├── desktop
│   └── mobile
│       ├── app.js
│       ├── deploy.json
│       └── index.html
└── src 
```

在 gulpfile 中，我们希望在运行我们的编译任务之前，将 `mobile` 文件的内容先清理掉：

```
var gulp = require('gulp');
var del = require('del');

gulp.task('clean:mobile', function (cb) {
  del([
    'dist/report.csv',
    // 这里我们使用一个通配模式来匹配 `mobile` 文件夹中的所有东西
    'dist/mobile/**/*',
    // 我们不希望删掉这个文件，所以我们取反这个匹配模式
    '!dist/mobile/deploy.json'
  ], cb);
});

gulp.task('default', ['clean:mobile']); 
```

## 在管道中删除文件

你可能需要在管道中将一些处理过的文件删除掉。

我们使用 [vinyl-paths](https://github.com/sindresorhus/vinyl-paths) 模块来简单地获取 stream 中每个文件的路径，然后传给 `del` 方法。

```
$ npm install --save-dev gulp del vinyl-paths 
```

假想有如下的文件结构：

```
.
├── tmp
│   ├── rainbow.js
│   └── unicorn.js
└── dist 
```

```
var gulp = require('gulp');
var stripDebug = require('gulp-strip-debug'); // 仅用于本例做演示
var del = require('del');
var vinylPaths = require('vinyl-paths');

gulp.task('clean:tmp', function () {
  return gulp.src('tmp/*')
    .pipe(stripDebug())
    .pipe(gulp.dest('dist'))
    .pipe(vinylPaths(del));
});

gulp.task('default', ['clean:tmp']); 
```

只有在已经使用了其他的插件之后才需要这样做，否则，请直接使用 `gulp.src` 来代替。

# 使用 watchify 加速 browserify 编译

# 使用 watchify 加速 browserify 编译

当一个 [browserify](http://github.com/substack/node-browserify) 项目开始变大的时候，编译打包的时间也会慢慢变得长起来。虽然开始的时候可能只需花 1 秒，然后当你的项目需要建立在一些流行的大型项目的基础上时，它很有可能就变成 30 秒了。

这就是为什么 [substack](http://github.com/substack) 写了 [watchify](http://github.com/substack/watchify) 的原因，一个持续监视文件的改动，并且 *只重新打包必要的文件* 的 browserify 打包工具。用这种方法，第一次打包的时候可能会还是会花 30 秒，但是后续的编译打包工作将一直保持在 100 毫秒以下 —— 这是一个极大的提升。

watchify 并没有一个相应的 gulp 插件，并且也不需要有：你可以使用 [vinyl-source-stream](http://github.com/hughsk/vinyl-source-stream) 来把你的用于打包的 stream 连接到 gulp 管道中。

```
'use strict';

var watchify = require('watchify');
var browserify = require('browserify');
var gulp = require('gulp');
var source = require('vinyl-source-stream');
var buffer = require('vinyl-buffer');
var gutil = require('gulp-util');
var sourcemaps = require('gulp-sourcemaps');
var assign = require('lodash.assign');

// 在这里添加自定义 browserify 选项
var customOpts = {
  entries: ['./src/index.js'],
  debug: true
};
var opts = assign({}, watchify.args, customOpts);
var b = watchify(browserify(opts));

// 在这里加入变换操作
// 比如： b.transform(coffeeify);

gulp.task('js', bundle); // 这样你就可以运行 `gulp js` 来编译文件了
b.on('update', bundle); // 当任何依赖发生改变的时候，运行打包工具
b.on('log', gutil.log); // 输出编译日志到终端

function bundle() {
  return b.bundle()
    // 如果有错误发生，记录这些错误
    .on('error', gutil.log.bind(gutil, 'Browserify Error'))
    .pipe(source('bundle.js'))
    // 可选项，如果你不需要缓存文件内容，就删除
    .pipe(buffer())
    // 可选项，如果你不需要 sourcemaps，就删除
    .pipe(sourcemaps.init({loadMaps: true})) // 从 browserify 文件载入 map
       // 在这里将变换操作加入管道
    .pipe(sourcemaps.write('./')) // 写入 .map 文件
    .pipe(gulp.dest('./dist'));
} 
```

# 增量编译打包，包括处理整所涉及的所有文件

# 增量编译打包，包括处理整所涉及的所有文件

在做增量编译打包的时候，有一个比较麻烦的事情，那就是你常常希望操作的是 *所有* 处理过的文件，而不仅仅是单个的文件。举个例子，你想要只对更改的文件做代码 lint 操作，以及一些模块封装的操作，然后将他们与其他已经 lint 过的，以及已经进行过模块封装的文件合并到一起。如果不用到临时文件的话，这将会非常困难。

使用 [gulp-cached](https://github.com/wearefractal/gulp-cached) 以及 [gulp-remember](https://github.com/ahaurw01/gulp-remember) 来解决这个问题。

```
var gulp = require('gulp');
var header = require('gulp-header');
var footer = require('gulp-footer');
var concat = require('gulp-concat');
var jshint = require('gulp-jshint');
var cached = require('gulp-cached');
var remember = require('gulp-remember');

var scriptsGlob = 'src/**/*.js';

gulp.task('scripts', function() {
  return gulp.src(scriptsGlob)
      .pipe(cached('scripts'))        // 只传递更改过的文件
      .pipe(jshint())                 // 对这些更改过的文件做一些特殊的处理...
      .pipe(header('(function () {')) // 比如 jshinting ^^^
      .pipe(footer('})();'))          // 增加一些类似模块封装的东西
      .pipe(remember('scripts'))      // 把所有的文件放回 stream
      .pipe(concat('app.js'))         // 做一些需要所有文件的操作
      .pipe(gulp.dest('public/'));
});

gulp.task('watch', function () {
  var watcher = gulp.watch(scriptsGlob, ['scripts']); // 监视与 scripts 任务中同样的文件
  watcher.on('change', function (event) {
    if (event.type === 'deleted') {                   // 如果一个文件被删除了，则将其忘记
      delete cached.caches.scripts[event.path];       // gulp-cached 的删除 api
      remember.forget('scripts', event.path);         // gulp-remember 的删除 api
    }
  });
}); 
```

# 将 buffer 变为 stream (内存中的内容)

# 将 buffer 变为 stream (内存中的内容)

有时候，你会需要这样一个 stream，它们的内容保存在一个变量中，而不是在一个实际的文件中。换言之，怎么不使用 `gulp.src()` 而创建一个 'gulp' stream。

我们来举一个例子，我们拥有一个包含 js 库文件的目录，以及一个包含一些模块的不同版本文件的目录。编译的目标是为每个版本创建一个 js 文件，其中包含所有库文件以及相应版本的模块文件拼接后的结果。

逻辑上我们将把这个拆分为如下步骤：

*   载入库文件
*   拼接库文件的内容
*   载入不同版本的文件
*   对于每个版本的文件，将其和库文件的内容拼接
*   对于每个版本的文件，将结果输出到一个文件

想象如下的文件结构：

```
├── libs
│   ├── lib1.js
│   └── lib2.js
└── versions
    ├── version.1.js
    └── version.2.js 
```

你应该要得到这样的结果：

```
└── output
    ├── version.1.complete.js # lib1.js + lib2.js + version.1.js
    └── version.2.complete.js # lib1.js + lib2.js + version.2.js 
```

一个简单的模块化处理方式将会像下面这样：

```
var gulp = require('gulp');
var runSequence = require('run-sequence');
var source = require('vinyl-source-stream');
var vinylBuffer = require('vinyl-buffer');
var tap = require('gulp-tap');
var concat = require('gulp-concat');
var size = require('gulp-size');
var path = require('path');
var es = require('event-stream');

var memory = {}; // 我们会将 assets 保存到内存中

// 载入内存中文件内容的任务
gulp.task('load-lib-files', function() {
  // 从磁盘中读取库文件
  return gulp.src('src/libs/*.js')
  // 将所有库文件拼接到一起
  .pipe(concat('libs.concat.js'))
  // 接入 stream 来获取每个文件的数据
  .pipe(tap(function(file) {
    // 保存文件的内容到内存
    memory[path.basename(file.path)] = file.contents.toString();
  }));
});

gulp.task('load-versions', function() {
  memory.versions = {};
  // 从磁盘中读取文件
  return gulp.src('src/versions/version.*.js')
  // 接入 stream 来获取每个文件的数据
  .pipe( tap(function(file) {
    // 在 assets 中保存文件的内容
    memory.versions[path.basename(file.path)] = file.contents.toString();
  }));
});

gulp.task('write-versions', function() {
  // 我们将不容版本的文件的名字保存到一个数组中
  var availableVersions = Object.keys(memory.versions);
  // 我们创建一个数组来保存所有的 stream 的 promise
  var streams = [];

  availableVersions.forEach(function(v) {
    // 以一个假文件名创建一个新的 stream
    var stream = source('final.' + v);
    // 从拼接后的文件中读取数据
    var fileContents = memory['libs.concat.js'] +
      // 增加版本文件的数据
      '\n' + memory.versions[v];

    streams.push(stream);

    // 将文件的内容写入 stream
    stream.write(fileContents);

    process.nextTick(function() {
      // 在下一次处理循环中结束 stream
      stream.end();
    });

    stream
    // 转换原始数据到 stream 中去，到一个 vinyl 对象/文件
    .pipe(vinylBuffer())
    //.pipe(tap(function(file) { /* 这里可以做一些对文件内容的处理操作 */ }))
    .pipe(gulp.dest('output'));
  });

  return es.merge.apply(this, streams);
});

//============================================ 我们的主任务
gulp.task('default', function(taskDone) {
  runSequence(
    ['load-lib-files', 'load-versions'],  // 并行载入文件
    'write-versions',  // 一旦所有资源进入内存便可以做写入操作了
    taskDone           // 完成
  );
});

//============================================ 我们的监控任务
// 只在运行完 'default' 任务后运行，
// 这样所有的资源都已经在内存中了
gulp.task('watch', ['default'], function() {
  gulp.watch('./src/libs/*.js', function() {
    runSequence(
      'load-lib-files',  // 我们只需要载入更改过的文件
      'write-versions'
    );
  });

  gulp.watch('./src/versions/*.js', function() {
    runSequence(
      'load-versions',  // 我们只需要载入更改过的文件
      'write-versions'
    );
  });
}); 
```

# 在 gulp 中运行 Mocha 测试

# 在 gulp 中运行 Mocha 测试

### 运行所有的测试用例

```
// npm install gulp gulp-mocha

var gulp = require('gulp');
var mocha = require('gulp-mocha');

gulp.task('default', function() {
  return gulp.src(['test/test-*.js'], { read: false })
    .pipe(mocha({
      reporter: 'spec',
      globals: {
        should: require('should')
      }
    }));
}); 
```

### 在文件改动时候运行 mocha 测试用例

```
// npm install gulp gulp-mocha gulp-util

var gulp = require('gulp');
var mocha = require('gulp-mocha');
var gutil = require('gulp-util');

gulp.task('mocha', function() {
    return gulp.src(['test/*.js'], { read: false })
        .pipe(mocha({ reporter: 'list' }))
        .on('error', gutil.log);
});

gulp.task('watch-mocha', function() {
    gulp.watch(['lib/**', 'test/**'], ['mocha']);
}); 
```

# 仅仅传递更改过的文件

# 仅仅传递更改过的文件

默认情况下，每次运行时候所有的文件都会传递并通过整个管道。通过使用 [gulp-changed](https://github.com/sindresorhus/gulp-changed) 可以只让更改过的文件传递过管道。这可以大大加快连续多次的运行。

```
// npm install --save-dev gulp gulp-changed gulp-jscs gulp-uglify

var gulp = require('gulp');
var changed = require('gulp-changed');
var jscs = require('gulp-jscs');
var uglify = require('gulp-uglify');

// 我们在这里定义一些常量以供使用
var SRC = 'src/*.js';
var DEST = 'dist';

gulp.task('default', function() {
    return gulp.src(SRC)
        // `changed` 任务需要提前知道目标目录位置
        // 才能找出哪些文件是被修改过的
        .pipe(changed(DEST))
        // 只有被更改过的文件才会通过这里
        .pipe(jscs())
        .pipe(uglify())
        .pipe(gulp.dest(DEST));
}); 
```

# 从命令行传递参数

# 从命令行传递参数

```
// npm install --save-dev gulp gulp-if gulp-uglify minimist

var gulp = require('gulp');
var gulpif = require('gulp-if');
var uglify = require('gulp-uglify');

var minimist = require('minimist');

var knownOptions = {
  string: 'env',
  default: { env: process.env.NODE_ENV || 'production' }
};

var options = minimist(process.argv.slice(2), knownOptions);

gulp.task('scripts', function() {
  return gulp.src('**/*.js')
    .pipe(gulpif(options.env === 'production', uglify())) // 仅在生产环境时候进行压缩
    .pipe(gulp.dest('dist'));
}); 
```

然后，通过如下命令运行 gulp：

```
$ gulp scripts --env development 
```

# 只重新编译被更改过的文件

# 只重新编译被更改过的文件

通过使用 [`gulp-watch`](https://github.com/floatdrop/gulp-watch):

```
var gulp = require('gulp');
var sass = require('gulp-sass');
var watch = require('gulp-watch');

gulp.task('default', function() {
  return gulp.src('sass/*.scss')
    .pipe(watch('sass/*.scss'))
    .pipe(sass())
    .pipe(gulp.dest('dist'));
}); 
```

# 每个文件夹生成单独一个文件

# 每个文件夹生成单独一个文件

如果你有一整套的文件目录，并且希望执行相应的一套任务，比如...

```
/scripts
/scripts/jquery/*.js
/scripts/angularjs/*.js 
```

...然后希望完成如下的结果 h...

```
/scripts
/scripts/jquery.min.js
/scripts/angularjs.min.js 
```

...你将会需要像下面所示的东西...

```
var fs = require('fs');
var path = require('path');
var merge = require('merge-stream');
var gulp = require('gulp');
var concat = require('gulp-concat');
var rename = require('gulp-rename');
var uglify = require('gulp-uglify');

var scriptsPath = 'src/scripts';

function getFolders(dir) {
    return fs.readdirSync(dir)
      .filter(function(file) {
        return fs.statSync(path.join(dir, file)).isDirectory();
      });
}

gulp.task('scripts', function() {
   var folders = getFolders(scriptsPath);

   var tasks = folders.map(function(folder) {
      // 拼接成 foldername.js
      // 写入输出
      // 压缩
      // 重命名为 folder.min.js
      // 再一次写入输出
      return gulp.src(path.join(scriptsPath, folder, '/*.js'))
        .pipe(concat(folder + '.js'))
        .pipe(gulp.dest(scriptsPath))
        .pipe(uglify())
        .pipe(rename(folder + '.min.js'))
        .pipe(gulp.dest(scriptsPath));
   });

   return merge(tasks);
}); 
```

注：

*   `folders.map` - 在每一个文件夹中分别执行一次函数，并且返回异步 stream
*   `merge` - 汇总 stream，并且在所有的 stream 都完成后完成

# 串行方式运行任务，亦即，任务依赖

# 串行方式运行任务，亦即，任务依赖

默认情况下，任务会以最大的并发数同时运行 -- 也就是说，它会不做任何等待地将所有的任务同时开起来。如果你希望创建一个有特定顺序的串行的任务链，你需要做两件事：

*   给它一个提示，用以告知任务在什么时候完成，
*   而后，再给一个提示，用以告知某任务需要依赖另一个任务的完成。

举个例子，我们假设你有两个任务，"one" 和 "two"，并且你明确的希望他们就以这样的顺序运行：

1.  在任务 "one" 中，你添加的一个提示，来告知何时它会完成。你可以传入一个回调函数，然后在完成后执行回调函数，也可以通过返回一个 promise 或者 stream 来让引擎等待它们分别地被解决掉。

2.  在任务 "two" 中，你添加一个提示，来告知引擎它需要依赖第一个任务的完成。

因此，这个例子将会是像这样：

```
var gulp = require('gulp');

// 传入一个回调函数，因此引擎可以知道何时它会被完成
gulp.task('one', function(cb) {
    // 做一些事 -- 异步的或者其他任何的事
    cb(err); // 如果 err 不是 null 和 undefined，流程会被结束掉，'two' 不会被执行
});

// 标注一个依赖，依赖的任务必须在这个任务开始之前被完成
gulp.task('two', ['one'], function() {
    // 现在任务 'one' 已经完成了
});

gulp.task('default', ['one', 'two']);
// 也可以这么写：gulp.task('default', ['two']); 
```

另一个例子，通过返回一个 stream 来取代使用回调函数的方法：

```
var gulp = require('gulp');
var del = require('del'); // rm -rf

gulp.task('clean', function(cb) {
    del(['output'], cb);
});

gulp.task('templates', ['clean'], function() {
    var stream = gulp.src(['src/templates/*.hbs'])
        // 执行拼接，压缩，等。
        .pipe(gulp.dest('output/templates/'));
    return stream; // 返回一个 stream 来表示它已经被完成

});

gulp.task('styles', ['clean'], function() {
    var stream = gulp.src(['src/styles/app.less'])
        // 执行一些代码检查，压缩，等
        .pipe(gulp.dest('output/css/app.css'));
    return stream;
});

gulp.task('build', ['templates', 'styles']);

// templates 和 styles 将会并行处理
// clean 将会保证在任一个任务开始之前完成
// clean 并不会被执行两次，尽管它被作为依赖调用了两次

gulp.task('default', ['build']); 
```

# 拥有实时重载（live-reloading）和 CSS 注入的服务器

# 拥有实时重载（live-reloading）和 CSS 注入的服务器

使用 [BrowserSync](http://browsersync.io) 和 gulp，你可以轻松地创建一个开发服务器，然后同一个 WiFi 中的任何设备都可以方便地访问到。BrowserSync 同时集成了 live-reload 所以不需要另外做配置了。

首先安装模块：

```
$ npm install --save-dev browser-sync 
```

然后，考虑拥有如下的目录结构...

```
gulpfile.js
app/
  styles/
    main.css
  scripts/
    main.js
  index.html 
```

... 通过如下的 `gulpfile.js`，你可以轻松地将 `app` 目录中的文件加到服务器中，并且所有的浏览器都会在文件发生改变之后自动刷新：

```
var gulp = require('gulp');
var browserSync = require('browser-sync');
var reload = browserSync.reload;

// 监视文件改动并重新载入
gulp.task('serve', function() {
  browserSync({
    server: {
      baseDir: 'app'
    }
  });

  gulp.watch(['*.html', 'styles/**/*.css', 'scripts/**/*.js'], {cwd: 'app'}, reload);
}); 
```

在 `index.html` 中引入 CSS：

```
<html>
  <head>
    ...
    <link rel="stylesheet" href="styles/main.css">
    ... 
```

通过如下命令启动服务，并且打开一个浏览器，访问默认的 URL ([`localhost:3000)：`](http://localhost:3000)：)

```
gulp serve 
```

## + CSS 预处理器

一个常见的使用案例是当 CSS 文件文件预处理之后重载它们。以 sass 为例，这便是你如何指示浏览器无需刷新整个页面而只是重载 CSS。

考虑有如下的文件目录结构...

```
gulpfile.js
app/
  scss/
    main.scss
  scripts/
    main.js
  index.html 
```

... 通过如下的 `gulpfile.js`，你可以轻松地监视 `scss` 目录中的文件，并且所有的浏览器都会在文件发生改变之后自动刷新：

```
var gulp = require('gulp');
var sass = require('gulp-ruby-sass');
var browserSync = require('browser-sync');
var reload = browserSync.reload;

gulp.task('sass', function() {
  return sass('scss/styles.scss')
    .pipe(gulp.dest('app/css'))
    .pipe(reload({ stream:true }));
});

// 监视 Sass 文件的改动，如果发生变更，运行 'sass' 任务，并且重载文件
gulp.task('serve', ['sass'], function() {
  browserSync({
    server: {
      baseDir: 'app'
    }
  });

  gulp.watch('app/scss/*.scss', ['sass']);
}); 
```

在 `index.html` 文件中引入预处理后的 CSS 文件：

```
<html>
  <head>
    ...
    <link rel="stylesheet" href="css/main.css">
    ... 
```

通过如下命令启动服务，并且打开一个浏览器，访问默认的 URL ([`localhost:3000)：`](http://localhost:3000)：)

```
gulp serve 
```

## 附注：

*   实时重载（Live reload），CSS 注入以及同步滚动可以在 [BrowserStack](http://www.browserstack.com/) 虚拟机里无缝执行。
*   设置 `tunnel: true` 来使用一个公开的 URL 来访问你本地的站点 (支持所有 BrowserSync 功能)。

# 通过 stream 工厂来共享 stream

# 通过 stream 工厂来共享 stream

如果你在多个任务中使用了相同的插件，你可能发现你很想把这些东西以 DRY 的原则去处理。这个方法可以创建一些工厂来把你经常使用的 stream 链分离出来。

我们将使用 [lazypipe](https://github.com/OverZealous/lazypipe) 来完成这件事。

这是我们的例子：

```
var gulp = require('gulp');
var uglify = require('gulp-uglify');
var coffee = require('gulp-coffee');
var jshint = require('gulp-jshint');
var stylish = require('jshint-stylish');

gulp.task('bootstrap', function() {
  return gulp.src('bootstrap/js/*.js')
    .pipe(jshint())
    .pipe(jshint.reporter(stylish))
    .pipe(uglify())
    .pipe(gulp.dest('public/bootstrap'));
});

gulp.task('coffee', function() {
  return gulp.src('lib/js/*.coffee')
    .pipe(coffee())
    .pipe(jshint())
    .pipe(jshint.reporter(stylish))
    .pipe(uglify())
    .pipe(gulp.dest('public/js'));
}); 
```

然后，使用了 lazypipe 之后，将会是这样：

```
var gulp = require('gulp');
var uglify = require('gulp-uglify');
var coffee = require('gulp-coffee');
var jshint = require('gulp-jshint');
var stylish = require('jshint-stylish');
var lazypipe = require('lazypipe');

// 赋给 lazypipe
var jsTransform = lazypipe()
  .pipe(jshint)
  .pipe(jshint.reporter, stylish)
  .pipe(uglify);

gulp.task('bootstrap', function() {
  return gulp.src('bootstrap/js/*.js')
    .pipe(jsTransform())
    .pipe(gulp.dest('public/bootstrap'));
});

gulp.task('coffee', function() {
  return gulp.src('lib/js/*.coffee')
    .pipe(coffee())
    .pipe(jsTransform())
    .pipe(gulp.dest('public/js'));
}); 
```

你可以看到，我们把多个任务中都在使用的 JavaScript 管道（JSHint + Uglify）分离到了一个工厂。工厂可以在任意多的任务中重用。你也可以嵌套这些工厂，或者把它们连接起来，已达到更好的效果。分离出每个共享的管道，也可以让你能够集中地管理，当你的工作流程更改后，你只需要修改一个地方即可。

# 指定一个新的 cwd (当前工作目录)

# 指定一个新的 cwd (当前工作目录)

在一个多层嵌套的项目中，这是非常有用的，比如：

```
/project
  /layer1
  /layer2 
```

你可以使用 gulp 的 CLI 参数 `--cwd`.

在 `project/` 目中中：

```
gulp --cwd layer1 
```

如果你需要对特定的匹配指定一个 cwd，你可以使用 [glob-stream](https://github.com/wearefractal/glob-stream) 的 `cwd` 选项：

```
gulp.src('./some/dir/**/*.js', { cwd: 'public' }); 
```

# 分离任务到多个文件中

# 分离任务到多个文件中

如果你的 `gulpfile.js` 开始变得很大，你可以通过使用 [require-dir](https://github.com/aseemk/requireDir) 模块将任务分离到多个文件

想象如下的文件结构：

```
gulpfile.js
tasks/
├── dev.js
├── release.js
└── test.js 
```

安装 `require-dir` 模块：

```
npm install --save-dev require-dir 
```

在 `gulpfile.js` 中增加如下几行代码：

```
var requireDir = require('require-dir');
var dir = requireDir('./tasks'); 
```

# 使用外部配置文件

# 使用外部配置文件

这有很多好处，因为它能让任务更加符合 DRY 原则，并且 config.json 可以被其他的任务运行器使用，比如 `grunt`。

###### `config.json`

```
{
  "desktop" : {
    "src" : [
      "dev/desktop/js/**/*.js",
      "!dev/desktop/js/vendor/**"
    ],
    "dest" : "build/desktop/js" },
  "mobile" : {
    "src" : [
      "dev/mobile/js/**/*.js",
      "!dev/mobile/js/vendor/**"
    ],
    "dest" : "build/mobile/js" } } 
```

###### `gulpfile.js`

```
// npm install --save-dev gulp gulp-uglify
var gulp = require('gulp');
var uglify = require('gulp-uglify');
var config = require('./config.json');

function doStuff(cfg) {
  return gulp.src(cfg.src)
    .pipe(uglify())
    .pipe(gulp.dest(cfg.dest));
}

gulp.task('dry', function() {
  doStuff(config.desktop);
  doStuff(config.mobile);
}); 
```

# 在一个任务中使用多个文件来源

# 在一个任务中使用多个文件来源

```
// npm install --save-dev gulp merge-stream

var gulp = require('gulp');
var merge = require('merge-stream');

gulp.task('test', function() {
  var bootstrap = gulp.src('bootstrap/js/*.js')
    .pipe(gulp.dest('public/bootstrap'));

  var jquery = gulp.src('jquery.cookie/jquery.cookie.js')
    .pipe(gulp.dest('public/jquery'));

  return merge(bootstrap, jquery);
}); 
```

`gulp.src` 会以文件被添加的顺序来 emit：

```
// npm install gulp gulp-concat

var gulp = require('gulp');
var concat = require('gulp-concat');

gulp.task('default', function() {
  return gulp.src(['foo/*', 'bar/*'])
    .pipe(concat('result.txt'))
    .pipe(gulp.dest('build'));
}); 
```

# Browserify + Uglify2 和 sourcemaps

# Browserify + Uglify2 和 sourcemaps

[Browserify](http://github.com/substack/node-browserify) 现在已经成为了一个不可或缺的重要工具了，然后要让它能完美的和 gulp 一起协作，还得需要做一些封装处理。先面便是一个使用 Browserify 并且增加一个完整的 sourcemap 来对应到单独的每个源文件。

同时请看: [组合 Streams 来处理错误](https://github.com/gulpjs/gulp/blob/master/docs/recipes/combining-streams-to-handle-errors.md) 范例来查看如何处理你的 stream 中 browserify 或者 uglify 的错误。

```
'use strict';

var browserify = require('browserify');
var gulp = require('gulp');
var source = require('vinyl-source-stream');
var buffer = require('vinyl-buffer');
var uglify = require('gulp-uglify');
var sourcemaps = require('gulp-sourcemaps');
var gutil = require('gulp-util');

gulp.task('javascript', function () {
  // 在一个基础的 task 中创建一个 browserify 实例
  var b = browserify({
    entries: './entry.js',
    debug: true
  });

  return b.bundle()
    .pipe(source('app.js'))
    .pipe(buffer())
    .pipe(sourcemaps.init({loadMaps: true}))
        // 在这里将转换任务加入管道
        .pipe(uglify())
        .on('error', gutil.log)
    .pipe(sourcemaps.write('./'))
    .pipe(gulp.dest('./dist/js/'));
}); 
```

# Browserify + Globs

# Browserify + Globs

[Browserify + Uglify2](https://github.com/gulpjs/gulp/blob/master/docs/recipes/browserify-uglify-sourcemap.md) 展示了如何设置一个基础的 gulp 任务来把一个 JavaScript 文件以及它的依赖打包，并且使用 UglifyJS 压缩并且保留 source map。 然而这还不够，这里还将会展示如何使用 gulp 和 Browserify 将多个文件打包到一起。

同时请看: [组合 Streams 来处理错误](https://github.com/gulpjs/gulp/blob/master/docs/recipes/combining-streams-to-handle-errors.md) 范例来查看如何处理你的 stream 中 browserify 或者 uglify 的错误。

```
'use strict';

var browserify = require('browserify');
var gulp = require('gulp');
var source = require('vinyl-source-stream');
var buffer = require('vinyl-buffer');
var globby = require('globby');
var through = require('through2');
var gutil = require('gulp-util');
var uglify = require('gulp-uglify');
var sourcemaps = require('gulp-sourcemaps');
var reactify = require('reactify');

gulp.task('javascript', function () {
  // gulp 希望任务能返回一个 stream，因此我们在这里创建一个
  var bundledStream = through();

  bundledStream
    // 将输出的 stream 转化成为一个包含 gulp 插件所期许的一些属性的 stream
    .pipe(source('app.js'))
    // 剩下的部分，和你往常缩写的一样。
    // 这里我们直接拷贝 Browserify + Uglify2 范例的代码。
    .pipe(buffer())
    .pipe(sourcemaps.init({loadMaps: true}))
      // 在这里将相应 gulp 插件加入管道
      .pipe(uglify())
      .on('error', gutil.log)
    .pipe(sourcemaps.write('./'))
    .pipe(gulp.dest('./dist/js/'));

  // "globby" 替换了往常的 "gulp.src" 为 Browserify
  // 创建的可读 stream。
  globby(['./entries/*.js'], function(err, entries) {
    // 确保任何从 globby 发生的错误都被捕获到
    if (err) {
      bundledStream.emit('error', err);
      return;
    }

    // 创建 Browserify 实例
    var b = browserify({
      entries: entries,
      debug: true,
      transform: [reactify]
    });

    // 将 Browserify stream 接入到我们之前创建的 stream 中去
    // 这里是 gulp 式管道正式开始的地方
    b.bundle().pipe(bundledStream);
  });

  // 最后，我们返回这个 stream，这样 gulp 会知道什么时候这个任务会完成
  return bundledStream;
}); 
```

# 同时输出一个压缩过和一个未压缩版本的文件

# 同时输出一个压缩过和一个未压缩版本的文件

同时输出压缩过的和未压缩版本的文件可以通过使用 `gulp-rename` 然后 pipe 到 `dest` 两次来实现 (一次是压缩之前的，一次是压缩后的)：

```
'use strict';

var gulp = require('gulp');
var rename = require('gulp-rename');
var uglify = require('gulp-uglify');

var DEST = 'build/';

gulp.task('default', function() {
  return gulp.src('foo.js')
    // 这会输出一个未压缩过的版本
    .pipe(gulp.dest(DEST))
    // 这会输出一个压缩过的并且重命名未 foo.min.js 的文件
    .pipe(uglify())
    .pipe(rename({ extname: '.min.js' }))
    .pipe(gulp.dest(DEST));
}); 
```

# 改变版本号以及创建一个 git tag

# 改变版本号以及创建一个 git tag

如果你的项目遵循语义化版本，那么，把那些发布新版本的时候需要做的事情通过自动化的手段去完成将会是个很不错的主意。 下面有一个简单的范例展示了如何改变项目的版本号，将更新提交到 git，以及创建一个 tag。

```
 var gulp = require('gulp');
var runSequence = require('run-sequence');
var bump = require('gulp-bump');
var gutil = require('gulp-util');
var git = require('gulp-git');
var fs = require('fs');

gulp.task('bump-version', function () {
// 注意：这里我硬编码了更新类型为 'patch'，但是更好的做法是用
//      minimist (https://www.npmjs.com/package/minimist) 通过检测一个命令行参数来判断你正在做的更新是
//      一个 'major'， 'minor' 还是一个 'patch'。
  return gulp.src(['./bower.json', './package.json'])
    .pipe(bump({type: "patch"}).on('error', gutil.log))
    .pipe(gulp.dest('./'));
});

gulp.task('commit-changes', function () {
  return gulp.src('.')
    .pipe(git.commit('[Prerelease] Bumped version number', {args: '-a'}));
});

gulp.task('push-changes', function (cb) {
  git.push('origin', 'master', cb);
});

gulp.task('create-new-tag', function (cb) {
  var version = getPackageJsonVersion();
  git.tag(version, 'Created Tag for version: ' + version, function (error) {
    if (error) {
      return cb(error);
    }
    git.push('origin', 'master', {args: '--tags'}, cb);
  });

  function getPackageJsonVersion () {
    // 这里我们直接解析 json 文件而不是使用 require，这是因为 require 会缓存多次调用，这会导致版本号不会被更新掉
    return JSON.parse(fs.readFileSync('./package.json', 'utf8')).version;
  };
});

gulp.task('release', function (callback) {
  runSequence(
    'bump-version',
    'commit-changes',
    'push-changes',
    'create-new-tag',
    function (error) {
      if (error) {
        console.log(error.message);
      } else {
        console.log('RELEASE FINISHED SUCCESSFULLY');
      }
      callback(error);
    });
}); 
```

# Swig 以及 YAML front-matter 模板

# Swig 以及 YAML front-matter 模板

模板可以使用 `gulp-swig` 和 `gulp-front-matter` 来设置：

##### `page.html`

```
---
title: Things to do
todos:
    - First todo
    - Another todo item
    - A third todo item
---
<html>
    <head>
        <title>{{ title }}</title>
    </head>
    <body>
        <h1>{{ title }}</h1>
        <ul>{% for todo in todos %}
          <li>{{ todo }}</li>
        {% endfor %}</ul>
    </body>
</html> 
```

##### `gulpfile.js`

```
var gulp = require('gulp');
var swig = require('gulp-swig');
var frontMatter = require('gulp-front-matter');

gulp.task('compile-page', function() {
  gulp.src('page.html')
      .pipe(frontMatter({ property: 'data' }))
      .pipe(swig())
      .pipe(gulp.dest('build'));
});

gulp.task('default', ['compile-page']); 
```