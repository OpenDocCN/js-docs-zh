# [](#seajs-flush)seajs-flush

A Sea.js plugin for collecting HTTP requests and sending all at once

## [](#install)Install

Install with spm:

```js
$ spm install seajs/seajs-flush 
```

## [](#usage)Usage

```js
<script src="path/to/sea.js"></script>
<script src="path/to/seajs-combo.js"></script>
<script src="path/to/seajs-flush.js"></script>

<script>
seajs.use(['a', 'b'], function(a, b) {
 // ...
})
 seajs.use(['c', 'd'], function(c, d) {
 // ...
})
 // The combined request is http://test.com/path/to/??a.js,b.js,c.js,d.js
seajs.flush()
</script>
```

For more details please visit [中文文档](https://github.com/seajs/seajs-flush/issues/7)