# lodash 4.5 中文文档

一个 JavaScript 的实用工具库, 表现一致性, [模块化](https://www.npmjs.com/browse/keyword/lodash-modularized), 高性能, 以及 可扩展

### Example

```js
_.assign({ 'a': 1 }, { 'b': 2 }, { 'c': 3 });
// → { 'a': 1, 'b': 2, 'c': 3 }

_.map([1, 2, 3], function(n) { return n * 3; });
// → [3, 6, 9] 
```

## 特点

*   ~100% [代码覆盖率](https://coveralls.io/github/lodash)
*   遵循 [语义化版本控制规范](http://semver.org/)
*   [延迟计算链](http://filimanjaro.com/blog/2014/introducing-lazy-evaluation/)
*   _(…) 支持隐式链
*   _.ary & _.rearg 改变函数的实参个数和顺序
*   _.at 更方便的获取数组或对象的值
*   _.attempt 无需 try-catch 来处理可能会出错的执行函数
*   _.before 与 _.after 互补
*   _.bindKey 实现 [*“懒传参”*](http://michaux.ca/articles/lazy-function-definition-pattern)
*   _.chunk 按给定个数来拆分数组
*   _.clone 支持对 `Date` & `RegExp` 对象的浅拷贝
*   _.cloneDeep 深拷贝数组或对象
*   _.curry & _.curryRight 用于创建 [柯里化](http://hughfdjackson.com/javascript/why-curry-helps/) 函数
*   _.debounce & _.throttle 处理函数防抖和节流
*   _.defaultsDeep 深分配对象的可枚举属性
*   _.fill 指定值填充数组
*   _.findKey 按 keys 查找对象
*   _.flow 与 _.flowRight (即 `_.compose`) 搭配
*   _.forEach 支持提前中断
*   _.forIn 遍历对象所有的可枚举属性
*   _.forOwn 遍历对象的所有属性
*   _.get & _.set 以 path 的方式获取和设置对象属性
*   _.gt, _.gte, _.lt, & _.lte 关系比较方法
*   _.inRange 检测给定的数值是否在指定范围内
*   _.isNative 检测是否是原生函数
*   _.isPlainObject & _.toPlainObject 检测是否是普通对象以及转换为普通对象
*   _.isTypedArray 检测是否是类型数组
*   _.mapKeys 按对象的 key 迭代，并返回新 key 的对象
*   _.matches 支持深匹配对象
*   _.matchesProperty & _.matches & _.property 互补
*   _.merge 相当于递归版 _.extend
*   _.method & _.methodOf 创建一个调用方法的函数
*   _.modArgs 更高级的功能组合
*   _.parseInt 兼容各环境
*   _.pull, _.pullAt, & _.remove 方便调整数组
*   _.random 支持返回浮点数
*   _.restParam & _.spread 应用一个 rest arguments 和 Spread operator 参数传递给函数
*   _.runInContext 无影响的 mixins 且更方便模拟
*   _.slice 支持裁剪类数组
*   _.sortByAll & _.sortByOrder 多个属性排序
*   _.support 标记环境功能
*   _.template 支持 *“imports”* 方式 & [ES 字符串模板](http://people.mozilla.org/%7Ejorendorff/es6-draft.html#sec-template-literal-lexical-components)
*   _.transform 更强大的 _.reduce 代替方法
*   _.unzipWith & _.zipWith 指定如何重组分解后的数组
*   _.valuesIn 获取所有可枚举属性的值
*   _.xor & _.difference, _.intersection, & _.union 互补
*   _.add, _.round, _.sum, 及更多 数学方法
*   _.bind, _.curry, _.partial, & 及更多 支持自定参数占位
*   _.capitalize, _.trim, & 及更多 string 方法
*   _.clone, _.isEqual, & 及更多 接受自定回调函数
*   _.dropWhile, _.takeWhile, & 及更多 互补 _.first, _.initial, _.last, & _.rest
*   _.findLast, _.findLastKey, & 及更多 右结合方法
*   _.includes, _.toArray, & 及更多 接受字符串方式
*   _#commit & _#plant 配合链式队列
*   _#thru 传递链式队列的值

## 关于翻译

*   该文档由 [think2011](https://github.com/think2011/) 翻译，遵循 [MIT 协议](https://github.com/jldec/lodash-doc-src/blob/master/LICENSE)， 定时保持与官方同步，翻译质量可能没法特别好，但会保证尽可能反复细心。
*   如果您有任何建议，或者意见，[欢迎在此讨论，及时更正 ;-)](https://github.com/think2011/lodash-zh/issues)。