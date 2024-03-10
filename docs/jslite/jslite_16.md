# 事件处理

> `blur` `focus` `focusin` `focusout` `load` `resize` `scroll` `unload` `click` `dblclick` `mousedown` `mouseup` `mousemove` `mouseover` `mouseout` `mouseenter` `mouseleave` `change` `select` `submit` `keydown` `keypress` `keyup` `error` 对象上直接添加事件。

```js
$("#box").click(function(){
    console.log("绑定点击事件")
}); 
```

## ready

> ready(function($){ ... }) ? self
> 添加一个事件侦听器，当页面 `dom` 加载完毕 `DOMContentLoaded` 事件触发时触发。加载完毕执行，建议使用 `$(func)` 来代替这种用法。

```js
$(document).ready(function(){
    alert("当页面 dom 加载完毕执行");
    console.log($("#box"));
}) 
```

## $(func)

> 加载完毕执行。与 `ready` 方法相同

```js
//或者使用下面方法代替 ready
$(function(){
    console.log("当页面 dom 加载完毕执行");
}) 
```

## bind

> 为每个匹配元素的特定事件绑定事件处理函数。可以绑定这些事件 `blur` `focus` `focusin` `focusout` `load` `resize` `scroll` `unload` `click` `dblclick` `mousedown` `mouseup` `mousemove` `mouseover` `mouseout` `mouseenter` `mouseleave` `change` `select` `submit` `keydown` `keypress` `keyup` `error` `paste` `drop` `dragover` 。

```js
$("#box").bind("click", function(){
    console.log("绑定点击事件")
}); 
```

## unbind

> 解除绑定事件，从每一个匹配的节点对象中删除绑定的事件。

```js
var f1=function(){alert('41');}
$("#box").bind("click",f1)   //? 绑定事件
$("#box").unbind("click",f1) //? 解除绑定事件

$("#box").bind("click",function(){alert('41');})   //? 绑定事件
$("#box").unbind("click",function(){alert('41');}) //? 解除绑定事件 
```

## on

> on(type, [selector], function(e){ ... }) ? self
> on({ type: handler, type2: handler2, ... }, [selector]) ? self
> 为每个匹配元素的特定事件绑定事件处理函数。可以绑定这些事件 `blur` `focus` `focusin` `focusout` `load` `resize` `scroll` `unload` `click` `dblclick` `mousedown` `mouseup` `mousemove` `mouseover` `mouseout` `mouseenter` `mouseleave` `change` `select` `submit` `keydown` `keypress` `keyup` `error` `paste` `drop` `dragover` 。

```js
$("#box").on("click", function(){
    console.log("绑定点击事件")
});

$("#box").on('click mouseover',function(evn){
    console.log('2'+evn)
}) //? self  绑定两个事件

$("#box").on('click','p',function(){
    console.log("被点击了")
})//? self  返回“#box”节点

$("#box").on("click",{val:1},function(){//传参数
    console.log("dddd","event.data.val = " + event.data.val)
})

$( "#box" ).on({ //绑定多个事件
    click: function() {
        $( this ).css("background","red");
    }, 
    mouseover: function() {
        $( this ).css("background","yellow")
    },
    mousedown: function() {
        $( this ).css("background","green")
    }
}); 
```

## off

> 解除绑定事件，从每一个匹配的节点对象中删除绑定的事件。

```js
var f1=function(){alert('41');}
$("#box").on("click",f1)   //? 绑定事件
$("#box").off("click",f1) //? 解除绑定事件

$("#box").on("click",function(){alert('41');})   //? 绑定事件
$("#box").off("click",function(){alert('41');}) //? 解除绑定事件 
```

## trigger

> trigger(event, [args]) ? self
> 匹配到的节点集合的元素上触发指定的事件。如果给定 args 参数，它会作为参数传递给事件函数。

```js
$("#box").on('abc:click',function(evn,a,c){
    console.log('2'+a+c)
}) //? self  绑定一个事件
$("#box").trigger('abc:click',['wwww']) //? self 触发并传一个参数进去 
```

* * *