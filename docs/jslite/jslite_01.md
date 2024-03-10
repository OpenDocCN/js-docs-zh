# 插件编写

## $.extend

> 通过源对象扩展目标对象的属性，扩展 `JSLite` 元素集来提供新的方法（通常用来制作插件）

```js
$.extend({
    min: function(a, b) { return a < b ? a : b; },
    max: function(a, b) { return a > b ? a : b; }
});
$.min(2,3);    //? 2
$.max(4,5);    //? 5
// 在$上扩展了几个方法 
//调用方法  $.min(2,3);   //? 2
//调用方法  $.max(4,5);   //? 5 
```

## $.fn.extend

> 扩展 `JSLite` 元素集来提供新的方法（通常用来制作插件）。

```js
$.fn.extend({   //增加两个插件方法。
    check: function() {
        return this.each(function() { this.checked = true; });
    },
    uncheck: function() {
        return this.each(function() { this.checked = false; });
    }
});
$("input[type=checkbox]").check();  //选中
$("input[type=radio]").uncheck();   //取消选中 
```

## $.error

> 当元素遇到错误（没有正确载入）时，发生 `error` 事件。

```js
$.error("2222")
//? 输出错误 Uncaught 2222 
```

* * *