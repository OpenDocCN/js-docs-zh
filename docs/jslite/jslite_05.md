# 测试操作

## $.isDocument

> 判断对象是否为【document】。

```js
$.isDocument(document) //? true 
```

## $.isWindow

> 确定参数是否为一个窗口（window 对象），如果是则返回 true。这在处理 iframe 时非常有用，因为每个 iframe 都有它们自己的 window 对象，使用常规方法 obj==window 校验这些 objects 的时候会失败。

## $.isFunction

> 判断对象是否为函数【function】。

```js
$.isFunction(function(){}) //? true 
```

## $.isObject

> 判断是否为 `Object` 。

```js
$.isObject({})  //? true 
```

## $.isPlainObject

> `$.isPlainObject(object) ? boolean`
> 如果通过 "{}" 或者 "new Object" 创建的则返回 true。判断对象是否是纯粹的对象。

```js
$.isPlainObject({})         // => true
$.isPlainObject(new Object) // => true
$.isPlainObject(new Date)   // => false
$.isPlainObject(window)     // => false 
```

## $.isArray

> 判断是否为【数组】。

```js
$.isArray([1,2,3])  //? true 
```

## $.isJson

> 判断是否为【数组】。

```js
$.isJson({})  //? true 
```

## $.contains

> `$.contains(parent, node) ? boolean` `parent`是否包含`node`节点对象。

```js
$.contains($("#box")[0],$(".boxss")[0]) //? parent 是否包含 node 节点对象 
```

## $.likeArray

> 判断对象是否为数组或者是字符。

```js
$.likeArray([1,2,3])     //? true
$.likeArray("222")  //? true 
```

## $.type

> 获取 JavaScript 对象的类型。可能的类型有： `null` `undefined` `boolean` `number` `string` `function` `array` `date` `regexp` `object` `error` 。

```js
$.type(true)  //? Boolean
$.type("div") //? String 
```

## $.matches

> 如果当前节点能被指定的 css 选择器查找到，则返回`true`，否则返回`false`。
> `$.matches(element,selector) ? boolean`

```js
$.matches($("#box")[0], "#box")//? true 
```

## is

> 判断当前匹配的元素集合中的元素，是否为一个选择器，DOM 元素 is(selector) ? boolean
> is(element) ? boolean

```js
$('#box').is('div');  //? true 
$('#box').is('#box');  //? true 
$('#box').is('#boxsss');  //? false 
$('div').is($('#box')[0]) //? true  节点是否在 $('#box')[0] 是否再集合中 
```

* * *