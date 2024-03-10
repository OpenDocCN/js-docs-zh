# [](#seajs-preload)seajs-preload

A Sea.js plugin for preload

## [](#install)Install

Install with spm:

```
$ spm install seajs/seajs-preload 
```

## [](#usage)Usage

```
<script src="path/to/sea.js"></script>
<script src="path/to/seajs-preload.js"></script>

<script>
 seajs.config({
 preload: ['jquery']
})
 seajs.use("path/to/mod")
 </script>
```

## [](#note)Note

This plugin bases on seajs ².3.0