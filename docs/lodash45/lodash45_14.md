# String

# String

# camelCase

## camelCase

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12058 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.camelcase "See the npm package.")

```
_.camelCase([string='']) 
```

转换字符串为 [驼峰写法](https://en.wikipedia.org/wiki/CamelCase)

### 参数

1.  [string=''] (string)

    要转换的字符串

### 返回值 (string)

返回驼峰写法的字符串

### 示例

```
_.camelCase('Foo Bar');
// => 'fooBar'

_.camelCase('--foo-bar');
// => 'fooBar'

_.camelCase('__foo_bar__');
// => 'fooBar' 
```

# capitalize

## capitalize

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12076 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.capitalize "See the npm package.")

```
_.capitalize([string='']) 
```

转换字符串首字母为大写，剩下为小写。

### 参数

1.  [string=''] (string)

    要大写开头的字符串

### 返回值 (string)

返回大写开头的字符串

### 示例

```
_.capitalize('FRED');
// => 'Fred' 
```

# deburr

## deburr

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12093 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.deburr "See the npm package.")

```
_.deburr([string='']) 
```

转换 [latin-1 supplementary letters](https://en.wikipedia.org/wiki/Latin-1_Supplement_(Unicode_block)#Character_table) 为基本拉丁字母，并删除[变音符](https://en.wikipedia.org/wiki/Combining_Diacritical_Marks)。

### 参数

1.  [string=''] (string)

    要处理的字符串

### 返回值 (string)

返回处理后的字符串

### 示例

```
_.deburr('déjà vu');
// => 'deja vu' 
```

# endsWith

## endsWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12119 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.endswith "See the npm package.")

```
_.endsWith([string=''], [target], [position=string.length]) 
```

检查给定的字符是否是字符串的结尾

### 参数

1.  [string=''] (string)

    要检索的字符串

2.  [target] (string)

    要检索字符

3.  [position=string.length] (number)

    检索的位置

### 返回值 (boolean)

如果是结尾返回 `true`，否则返回 `false`

### 示例

```
_.endsWith('abc', 'c');
// => true

_.endsWith('abc', 'b');
// => false

_.endsWith('abc', 'b', 2);
// => true 
```

# escape

## escape

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12160 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.escape "See the npm package.")

```
_.escape([string='']) 
```

转义字符 "&", "<", ">", '"', "'", 以及 "`" 为 HTML 实体字符。

**注意:** 不会转义其他字符，如果需要，可以使用第三方库，例如 [*he*](https://mths.be/he)。

虽然 ">" 是对称转义的，像是 ">" 和 "/" 没有特殊的意义，所以不需要在 HTML 中转义。 除非它们是标签的一部分，或者是不带引号的属性值。 查看 [Mathias Bynens 的文章](https://mathiasbynens.be/notes/ambiguous-ampersands) (under "semi-related fun fact") 了解详情

在 IE < 9 中转义引号，因为会中断属性值或 HTML 注释，查看 [HTML5 安全列表](https://html5sec.org/) 的 [#59](https://html5sec.org/#59), [#102](https://html5sec.org/#102), [#108](https://html5sec.org/#108), 以及 [#133](https://html5sec.org/#133) 了解详情

当解析为 HTML 时应该总是 [引用属性值](http://wonko.com/post/html-escaping) 以减少 XSS 的可能性。

### 参数

1.  [string=''] (string)

    要转义的字符串

### 返回值 (string)

返回转义后的字符串

### 示例

```
_.escape('fred, barney, & pebbles');
// => 'fred, barney, &amp; pebbles' 
```

# escapeRegExp

## escapeRegExp

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12181 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.escaperegexp "See the npm package.")

```
_.escapeRegExp([string='']) 
```

转义`RegExp` 中特殊的字符 "^", "$", "\", ".", "*", "+", "?", "(", ")", "[", "]", "{", "}", 以及 "|"。

### 参数

1.  [string=''] (string)

    要转义的字符串

### 返回值 (string)

返回转义后的字符串

### 示例

```
_.escapeRegExp('[lodash](https://lodash.com/)');
// => '\[lodash\]\(https://lodash\.com/\)' 
```

# kebabCase

## kebabCase

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12207 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.kebabcase "See the npm package.")

```
_.kebabCase([string='']) 
```

转换字符串为 [kebab case](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles)。

### 参数

1.  [string=''] (string)

    要转换的字符串

### 返回值 (string)

返回转换后的字符串

### 示例

```
_.kebabCase('Foo Bar');
// => 'foo-bar'

_.kebabCase('fooBar');
// => 'foo-bar'

_.kebabCase('__foo_bar__');
// => 'foo-bar' 
```

# lowerCase

## lowerCase

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12230 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.lowercase "See the npm package.")

```
_.lowerCase([string='']) 
```

以空格分开单词并转换为小写。

### 参数

1.  [string=''] (string)

    要转换的字符串

### 返回值 (string)

返回小写的字符串

### 示例

```
_.lowerCase('--Foo-Bar');
// => 'foo bar'

_.lowerCase('fooBar');
// => 'foo bar'

_.lowerCase('__FOO_BAR__');
// => 'foo bar' 
```

# lowerFirst

## lowerFirst

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12250 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.lowerfirst "See the npm package.")

```
_.lowerFirst([string='']) 
```

转换首字母为小写。

### 参数

1.  [string=''] (string)

    要转换的字符串

### 返回值 (string)

返回转换后的字符串

### 示例

```
_.lowerFirst('Fred');
// => 'fred'

_.lowerFirst('FRED');
// => 'fRED' 
```

# pad

## pad

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12292 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.pad "See the npm package.")

```
_.pad([string=''], [length=0], [chars=' ']) 
```

如果字符串长度小于 `length` 则从左到右填充字符。 如果没法平均分配，则截断超出的长度。

### 参数

1.  [string=''] (string)

    要填充的字符串

2.  [length=0] (number)

    填充的长度

3.  [chars=' '] (string)

    填充字符

### 返回值 (string)

返回填充后的字符串

### 示例

```
_.pad('abc', 8);
// => '  abc   '

_.pad('abc', 8, '_-');
// => '_-abc_-_'

_.pad('abc', 3);
// => 'abc' 
```

# padEnd

## padEnd

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12328 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.padend "See the npm package.")

```
_.padEnd([string=''], [length=0], [chars=' ']) 
```

如果字符串长度小于 length 则在右侧填充字符。 如果超出长度则截断超出的部分。

### 参数

1.  [string=''] (string)

    要填充的字符串

2.  [length=0] (number)

    填充的长度

3.  [chars=' '] (string)

    填充字符

### 返回值 (string)

Returns 返回填充后的字符串

### 示例

```
_.padEnd('abc', 6);
// => 'abc   '

_.padEnd('abc', 6, '_-');
// => 'abc_-_'

_.padEnd('abc', 3);
// => 'abc' 
```

# padStart

## padStart

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12354 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.padstart "See the npm package.")

```
_.padStart([string=''], [length=0], [chars=' ']) 
```

如果字符串长度小于 length 则在左侧填充字符。 如果超出长度则截断超出的部分。

### 参数

1.  [string=''] (string)

    要填充的字符串

2.  [length=0] (number)

    填充的长度

3.  [chars=' '] (string)

    填充字符

### 返回值 (string)

Returns 返回填充后的字符串

### 示例

```
_.padStart('abc', 6);
// => '   abc'

_.padStart('abc', 6, '_-');
// => '_-_abc'

_.padStart('abc', 3);
// => 'abc' 
```

# parseInt

## parseInt

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12381 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.parseint "See the npm package.")

```
_.parseInt(string, [radix]) 
```

以指定的基数转换字符串为整数。 如果基数是 `undefined` 或者 0，则基数默认是 10，如果字符串是 16 进制，则基数为 16。

**注意:** 这个方法与 [ES5 implementation](https://es5.github.io/#E) 的 `parseInt` 一致

### 参数

1.  string (string)

    要转换的字符串

2.  [radix] (number)

    基数

### 返回值 (number)

返回转换后的整数

### 示例

```
_.parseInt('08');
// => 8

_.map(['6', '08', '10'], _.parseInt);
// => [6, 8, 10] 
```

# repeat

## repeat

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12413 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.repeat "See the npm package.")

```
_.repeat([string=''], [n=0]) 
```

重复 N 次字符串

### 参数

1.  [string=''] (string)

    要重复的字符串

2.  [n=0] (number)

    重复的次数

### 返回值 (string)

返回重复的字符串

### 示例

```
_.repeat('*', 3);
// => '***'

_.repeat('abc', 2);
// => 'abcabc'

_.repeat('abc', 0);
// => '' 
```

# replace

## replace

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12451 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.replace "See the npm package.")

```
_.replace([string=''], pattern, 要替换的内容) 
```

替换字符串中匹配的内容为给定的内容

**注意:** 这个方法基于 [`String#replace`](https://mdn.io/String/replace)

### 参数

1.  [string=''] (string)

    待替换的字符串

2.  pattern (RegExp|string)

    要匹配的内容

3.  要替换的内容 (Function|string)

### 返回值 (string)

返回替换完成的字符串

### 示例

```
_.replace('Hi Fred', 'Fred', 'Barney');
// => 'Hi Barney' 
```

# snakeCase

## snakeCase

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12477 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.snakecase "See the npm package.")

```
_.snakeCase([string='']) 
```

转换字符串为 [snake case](https://en.wikipedia.org/wiki/Snake_case)

### 参数

1.  [string=''] (string)

    要转换的字符串

### 返回值 (string)

返回转换后的字符串

### 示例

```
_.snakeCase('Foo Bar');
// => 'foo_bar'

_.snakeCase('fooBar');
// => 'foo_bar'

_.snakeCase('--foo-bar');
// => 'foo_bar' 
```

# split

## split

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12498 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.split "See the npm package.")

```
_.split([string=''], [separator], [limit]) 
```

以 `separator` 拆分字符串

**注意:** 这个方法基于 [`String#split`](https://mdn.io/String/split)

### 参数

1.  [string=''] (string)

    要拆分的字符串

2.  [separator] (RegExp|string)

    拆分的分隔符

3.  [limit] (number)

    限制的数量

### 返回值 (Array)

返回拆分部分的字符串的数组

### 示例

```
_.split('a-b-c', '-', 2);
// => ['a', 'b'] 
```

# startCase

## startCase

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12521 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.startcase "See the npm package.")

```
_.startCase([string='']) 
```

转换字符串为 [start case](https://en.wikipedia.org/wiki/Letter_case#Stylistic_or_specialised_usage)

### 参数

1.  [string=''] (string)

    要转换的字符串

### 返回值 (string)

返回转换后的字符串

### 示例

```
_.startCase('--foo-bar');
// => 'Foo Bar'

_.startCase('fooBar');
// => 'Foo Bar'

_.startCase('__foo_bar__');
// => 'Foo Bar' 
```

# startsWith

## startsWith

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12546 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.startswith "See the npm package.")

```
_.startsWith([string=''], [target], [position=0]) 
```

检查字符串是否以 `target` 开头。

### 参数

1.  [string=''] (string)

    要检索的字符串

2.  [target] (string)

    要检查的字符串

3.  [position=0] (number)

    检索的位置

### 返回值 (boolean)

如果符合条件返回`true`，否则返回 `false`

### 示例

```
_.startsWith('abc', 'a');
// => true

_.startsWith('abc', 'b');
// => false

_.startsWith('abc', 'b', 1);
// => true 
```

# template

## template

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12648 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.template "See the npm package.")

```
_.template([string=''], [options]) 
```

创建一个预编译模板方法，可以插入数据到模板中 "interpolate" 分隔符相应的位置。 HTML 会在 "escape" 分隔符中转换为相应实体。 在 "evaluate" 分隔符中允许执行 JavaScript 代码。 在模板中可以自由访问变量。 如果设置了选项对象，则会优先覆盖 `_.templateSettings` 的值。

**注意:** 在开发过程中可以使用 [sourceURLs](http://www.html5rocks.com/en/tutorials/developertools/sourcemaps/#toc-sourceurl) 便于调试。

了解更多预编译模板的信息查看 [lodash 的自定义构建文档](https://lodash.com/custom-builds)

了解更多 Chrome 沙箱扩展的信息查看 [Chrome 的扩展文档](https://developer.chrome.com/extensions/sandboxingEval)

### 参数

1.  [string=''] (string)

    模板字符串

2.  [options] (Object)

    选项对象

3.  [options.escape] (RegExp)

    "escape" 分隔符

4.  [options.evaluate] (RegExp)

    "evaluate" 分隔符

5.  [options.imports] (Object)

    导入对象到模板中作为自由变量

6.  [options.interpolate] (RegExp)

    "interpolate" 分隔符

7.  [options.sourceURL] (string)

    模板编译的来源 URL

8.  [options.variable] (string)

    数据对象的变量名

### 返回值 (Function)

返回编译模板函数

### 示例

```
// 使用 "interpolate" 分隔符创建编译模板
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'

// 使用 HTML "escape" 转义数据的值
var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'

// 使用 "evaluate" 分隔符执行 JavaScript 和 生成 HTML 代码
var compiled = _.template('<% _.forEach(users, function(user) { %><li><%- user %></li><% }); %>');
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'

// 在 "evaluate" 分隔符中使用内部的 `print` 函数
var compiled = _.template('<% print("hello " + user); %>!');
compiled({ 'user': 'barney' });
// => 'hello barney!'

// 使用 ES 分隔符代替默认的 "interpolate" 分隔符
var compiled = _.template('hello ${ user }!');
compiled({ 'user': 'pebbles' });
// => 'hello pebbles!'

// 使用自定义的模板分隔符
_.templateSettings.interpolate = /{{([\s\S]+?)}}/g;
var compiled = _.template('hello {{ user }}!');
compiled({ 'user': 'mustache' });
// => 'hello mustache!'

// 使用反斜杠符号作为纯文本处理
var compiled = _.template('<%= "\\<%- value %\\>" %>');
compiled({ 'value': 'ignored' });
// => '<%- value %>'

// 使用 `imports` 选项导入 `jq` 作为 `jQuery` 的别名
var text = '<% jq.each(users, function(user) { %><li><%- user %></li><% }); %>';
var compiled = _.template(text, { 'imports': { 'jq': jQuery } });
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'

// 使用 `sourceURL` 选项指定模板的来源 URL
var compiled = _.template('hello <%= user %>!', { 'sourceURL': '/basic/greeting.jst' });
compiled(data);
// => 在开发工具的 Sources 选项卡 或 Resources 面板中找到 "greeting.jst"

// 使用 `variable` 选项确保在编译模板中不声明变量
var compiled = _.template('hi <%= data.user %>!', { 'variable': 'data' });
compiled.source;
// => function(data) {
//   var __t, __p = '';
//   __p += 'hi ' + ((__t = ( data.user )) == null ? '' : __t) + '!';
//   return __p;
// }

// 使用 `source` 特性内联编译模板
// 便以查看行号、错误信息、堆栈
fs.writeFileSync(path.join(cwd, 'jst.js'), '\
  var JST = {\
    "main": ' + _.template(mainText).source + '\
  };\
'); 
```

# toLower

## toLower

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12773 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.tolower "See the npm package.")

```
_.toLower([string='']) 
```

转换整体的字符串为小写

### 参数

1.  [string=''] (string)

    要转换的字符串

### 返回值 (string)

返回小写的字符串

### 示例

```
_.toLower('--Foo-Bar');
// => '--foo-bar'

_.toLower('fooBar');
// => 'foobar'

_.toLower('__FOO_BAR__');
// => '__foo_bar__' 
```

# toUpper

## toUpper

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12796 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.toupper "See the npm package.")

```
_.toUpper([string='']) 
```

转换整体的字符串为大写

### 参数

1.  [string=''] (string)

    要转换的字符串

### 返回值 (string)

返回大写的字符串

### 示例

```
_.toUpper('--foo-bar');
// => '--FOO-BAR'

_.toUpper('fooBar');
// => 'FOOBAR'

_.toUpper('__foo_bar__');
// => '__FOO_BAR__' 
```

# trim

## trim

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12821 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.trim "See the npm package.")

```
_.trim([string=''], [chars=whitespace]) 
```

从字符串中移除前面和后面的空白 或 指定的字符。

### 参数

1.  [string=''] (string)

    要处理的字符串

2.  [chars=whitespace] (string)

    要处理的字符

### 返回值 (string)

返回处理后的字符串

### 示例

```
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'

_.map(['  foo  ', '  bar  '], _.trim);
// => ['foo', 'bar'] 
```

# trimEnd

## trimEnd

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12857 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.trimend "See the npm package.")

```
_.trimEnd([string=''], [chars=whitespace]) 
```

移除字符串后面的空白 或 指定的字符。

### 参数

1.  [string=''] (string)

    要处理的字符串

2.  [chars=whitespace] (string)

    要处理的字符

### 返回值 (string)

返回处理后的字符串

### 示例

```
_.trimEnd('  abc  ');
// => '  abc'

_.trimEnd('-_-abc-_-', '_-');
// => '-_-abc' 
```

# trimStart

## trimStart

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12891 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.trimstart "See the npm package.")

```
_.trimStart([string=''], [chars=whitespace]) 
```

移除字符串中前面的空白 或 指定的字符。

### 参数

1.  [string=''] (string)

    要处理的字符串

2.  [chars=whitespace] (string)

    要处理的字符

### 返回值 (string)

返回处理后的字符串

### 示例

```
_.trimStart('  abc  ');
// => 'abc  '

_.trimStart('-_-abc-_-', '_-');
// => 'abc-_-' 
```

# truncate

## truncate

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12942 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.truncate "See the npm package.")

```
_.truncate([string=''], [options]) 
```

截断字符串，如果字符串超出了限定的最大值。 被截断的字符串后面会以 `omission` 代替，`omission` 默认是 "..."。

### 参数

1.  [string=''] (string)

    要截断的字符串

2.  [options] (Object)

    选项对象

3.  [options.length=30] (number)

    允许的最大长度

4.  [options.omission='...'] (string)

    超出后的代替字符

5.  [options.separator] (RegExp|string)

    截断点

### 返回值 (string)

返回截断后的字符串

### 示例

```
_.truncate('hi-diddly-ho there, neighborino');
// => 'hi-diddly-ho there, neighbo...'

_.truncate('hi-diddly-ho there, neighborino', {
  'length': 24,
  'separator': ' '
});
// => 'hi-diddly-ho there,...'

_.truncate('hi-diddly-ho there, neighborino', {
  'length': 24,
  'separator': /,? +/
});
// => 'hi-diddly-ho there...'

_.truncate('hi-diddly-ho there, neighborino', {
  'omission': ' [...]'
});
// => 'hi-diddly-ho there, neig [...]' 
```

# unescape

## unescape

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13015 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.unescape "See the npm package.")

```
_.unescape([string='']) 
```

反向版 `_.escape`。 这个方法转换 HTML 实体 `&amp;`, `&lt;`, `&gt;`, `&quot;`, `&#39;`, 以及 `&#96;` 为对应的字符。

**注意:** 不会转换其他的 HTML 实体，需要转换可以使用类似 [*he*](https://mths.be/he) 的第三方库。

### 参数

1.  [string=''] (string)

    要转换的字符串

### 返回值 (string)

返回转换后的字符串

### 示例

```
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles' 
```

# upperCase

## upperCase

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13041 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.uppercase "See the npm package.")

```
_.upperCase([string='']) 
```

转换字符串为空格分割的大写单词

### 参数

1.  [string=''] (string)

    要转换的字符串

### 返回值 (string)

返回大写单词

### 示例

```
_.upperCase('--foo-bar');
// => 'FOO BAR'

_.upperCase('fooBar');
// => 'FOO BAR'

_.upperCase('__foo_bar__');
// => 'FOO BAR' 
```

# upperFirst

## upperFirst

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L12268 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.upperfirst "See the npm package.")

```
_.upperFirst([string='']) 
```

转换首字母为大写。

### 参数

1.  [string=''] (string)

    要转换的字符串

### 返回值 (string)

返回转换后的字符串

### 示例

```
_.upperFirst('fred');
// => 'Fred'

_.upperFirst('FRED');
// => 'FRED' 
```

# words

## words

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L13063 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.words "See the npm package.")

```
_.words([string=''], [pattern]) 
```

拆分字符串中的词为数组

### 参数

1.  [string=''] (string)

    要处理的字符串

2.  [pattern] (RegExp|string)

    匹配模式

### 返回值 (Array)

然后拆分后的数组

### 示例

```
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']

_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles'] 
```