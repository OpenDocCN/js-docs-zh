# 创建插件

# 创建插件

可以通过添加方法作为 `$.fn` 的属性来写插件：

```
;(function($){
  $.extend($.fn, {
    foo: function(){
      // `this` refers to the current Zepto collection.
      // When possible, return the Zepto collection to allow chaining.
      return this.html('bar')
    }
  })
})(Zepto) 
```

为了更好开始开发插件，先看下[source of Zepto's core module](https://github.com/madrobby/zepto/blob/master/src/zepto.js)，并确认读过[coding style guidelines](https://github.com/madrobby/zepto#code-style-guidelines)