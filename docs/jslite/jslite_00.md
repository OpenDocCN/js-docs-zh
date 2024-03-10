# 核心

## $()

> 选择器使用的是浏览器自带的方法的 `document.querySelectorAll` 接口，支持标准的 CSS 选择器，没有使用 jQuery 作者 John Resig 开发的 DOM 选择器引擎(Dom Selector Engine) `Sizzle` 。 目前 IE8/9 及 Firefox/Chrome/Safari/Opera 的最新版已经支持 `querySelectorAll` 。
> 
> `$(selector)` //? 选择节点
> `$("<DOM nodes>")` //? 生成节点
> `$("htmlString")` //? 生成
> `JSLite(function($){ ... })` //? 相当于 ready

```
$("#box") //? 返回节点数组  //? [<div>?…?</div>?]
$("<div></div>") //? 生成 div 节点
//JSLite(func) 相当于 ready
JSLite(function($){
    console.log("在节点加载完成之后执行")
})
//$(func) 相当于 ready
$(function($){
    console.log("在节点加载完成之后执行")
}) 
```

## JSLite()

> 与`$()`相同。

## noConflict

`noConflict()` 方法让渡变量 $ 的 `JSLite` 控制权，解决俩库之间的$冲突。
该方法释放 `JSLite` 对 `$` 变量的控制。
该方法也可用于为 `JSLite` 变量规定新的自定义名称。

### 常规

```
$.noConflict();
JSLite(document).ready(function($) {
// 使用 JSLite $ 的代码
});
// 使用其他库的 $ 的代码 
```

### 映射回原始的对象

将 `$` 引用的对象映射回原始的对象：

```
JSLite.noConflict();
JSLite("div p").hide(); // 使用 JSLite
$("content").style.display = "none";    // 使用其他库的 $() 
```

### 恢复使用别名

恢复使用别名 `$`，然后创建并执行一个函数，在这个函数的作用域中仍然将 `$` 作为 `JSLite` 的别名来使用。在这个函数中，原来的 `$` 对象是无效的。这个函数对于大多数不依赖于其他库的插件都十分有效：

```
JSLite.noConflict();
(function($) { 
  $(function() {
    // 使用 $ 作为 JSLite 别名的代码
  });
})(JSLite);

... // 其他用 $ 作为别名的库的代码 
```

### 简写

可以将 `JSLite.noConflict()` 与简写的 `ready` 结合，使代码更紧凑

```
JSLite.noConflict()(function(){
    // 使用 JSLite 的代码
    console.log($('div'))
}); 
```

### 创建别名

创建一个新的别名用以在接下来的库中使用 `JSLite` 对象：

```
var j = JSLite.noConflict();
j("#box").hide();  // 基于 JSLite 的代码
$("content").style.display = "none";    // 基于其他库的 $() 代码 
```

### 新的命名空间

完全将 `JSLite` 移到一个新的命名空间：

```
var dom = {};
dom.jslite = JSLite.noConflict(true); 
```

结果:

```
dom.jslite("div p").hide();  // 新 JSLite 的代码
$("content").style.display = "none";    // 另一个库 $() 的代码
JSLite("div > p").hide();   // 另一个版本 JSLite 的代码 
```

* * *