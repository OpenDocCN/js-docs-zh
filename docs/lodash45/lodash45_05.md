# Date

# now

## now

*   link
*   [source](https://github.com/lodash/lodash/blob/4.5.0 正式版/lodash.src.js#L8299 "View in source.")
*   [npm](https://www.npmjs.com/package/lodash.now "See the npm package.")

```
_.now() 
```

获得 Unix 纪元(1970 1 月 1 日 00:00:00 UTC) 直到现在的毫秒数。

### 返回值 (number)

返回时间戳

### 示例

```
_.defer(function(stamp) {
  console.log(_.now() - stamp);
}, _.now());
// => 记录延迟函数调用的毫秒数 
```