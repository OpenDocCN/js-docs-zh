# 插入节点方法

## prepend

> 插入到标签开始标记之后（里面的第一个）。
> `prepend(content) ? self` `prepend(Function) ? self`

```js
$("#box").prepend("dd") //? self
$("#box").prepend(function(){
    return "asdfasdf"
}) //? self 
```

## prependTo

> 将生成的内容插入到匹配的节点标签开始标记之后。这有点像 prepend，但是是相反的方式。
> `prependTo(selector) ? self`

```js
$('<div>test</div>').prependTo('#box') 
```

## append

> 插入到标签结束标记前（里面的结尾）。
> `append(content) ? self` `append(Function) ? self`

```js
$("#box").append("dd") //? self

$("#box").append(function(){
    return "asdfasdf"
}) //? self 
```

## appendTo

> 将生成的内容插入到匹配的元素标签结束标记前（里面的最后）。这个有点像 append，但是插入的目标与其相反。 `appendTo(selector) ? self`

```js
$('<div>test</div>').appendTo('#box') 
```

## after

> 插入到标签结束标记后。（兄弟节点的下面）
> `after(content) ? self` `after(Function) ? self`

```js
$("#box").after("dd") //? self
$("#box").after(function(){
    return "asdfasdf"
}) //? self 
```

## insertAfter

> 插入的对象集合中的元素到指定的每个元素后面的 dom 中。这个有点像 `after` ，但是使用方式相反。
> `insertAfter(selector) ? self`

```js
$('<p>test</p>').insertAfter('#box') //? self
$('#input').insertAfter('#box')        //? self  $('#input') 
```

## before

> 插入到标签开始前。
> `after(content) ? self` `after(Function) ? self`

```js
$("#box").before($('input')) //? self
$("#box").before(function(){
    return "asdfasdf"
}) //? self 
```

## insertBefore

> 将生成的内容插入 `selector` 匹配的节点标签开始前。这个有点像 `before`，但是使用方式相反。 `insertBefore(selector) ? self`

```js
$('<p>test</p>').insertBefore('#box') 
```

## unwrap

> 移除集合中每个元素的直接父节点，并把他们的子元素保留在原来的位置。 基本上，这种方法删除上一的祖先元素，同时保持 DOM 中的当前元素。 `replaceWith(content|fn)`

```js
$("p").unwrap() // ? self 
```

## replaceWith

> 将所有匹配的元素替换成指定的 HTML 或 DOM 元素。
> `replaceWith(content|fn)`

```js
$("p").replaceWith("<b>段落。</b>"); 
```

用第一段替换第三段，你可以发现他是移动到目标位置来替换，而不是复制一份来替换。

```js
<div class="container">
  <div class="inner first">Hello</div>
  <div class="inner second">And</div>
  <div class="inner third">Goodbye</div>
</div>
<script type="text/javascript"> $('.third').replaceWith($('.first'));  // ? 返回 “.third” 节点 </script> 
```

上面的结果

```js
<div class="container">
  <div class="inner second">And</div>
  <div class="inner first">Hello</div>
</div> 
```

## clone

> clone() ? collection
> 通过深度克隆来复制集合中的所有元素。(通过原生 `cloneNode` 方法深度克隆来复制集合中的所有元素。此方法不会有数据和事件处理程序复制到新的元素。这点和 jquery 中利用一个参数来确定是否复制数据和事件处理不相同。)

```js
$('body').append($("#box").clone()) 
```

* * *