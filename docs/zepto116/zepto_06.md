# 核心方法

## $()

```js
$(selector, [context])   => collection
$(<Zepto collection>)   => same collection
$(<DOM nodes>)   => collection
$(htmlString)   => collection
$(htmlString, attributes)   => collection v1.0+
Zepto(function($){ ... }) 
```

通过执行 css 选择器，包装 dom 节点，或者通过一个 html 字符串创建多个元素 来创建一个 Zepto 集合对象。

Zepto 集合是一个类似数组的对象，它具有链式方法来操作它指向的 DOM 节点，除了$( `Zepto`)对象上的直接方法外(如`$.extend`)，文档对象中的所有方法都是集合方法。

如果选择器中存在 content 参数(css 选择器，dom，或者 Zepto 集合对象)，那么只在所给的节点背景下进行 css 选择器；这个功能和使用`$(context).find(selector)`是一样的。

当给定一个 html 字符串片段来创建一个 dom 节点时。也可以通过给定一组属性映射来创建节点。最快的创建但元素，使用`&lt;div&gt;` 或 `&lt;div/&gt;`形式。

当一个函数附加在 `DOMContentLoaded` 事件的处理流程中。如果页面已经加载完毕，这个方法将会立即被执行。

```js
$('div')  //=> 所有页面中得 div 元素
$('#foo') //=> ID 为 "foo" 的元素

// 创建元素:
$("<p>Hello</p>") //=> 新的 p 元素
// 创建带有属性的元素:
$("<p />", { text:"Hello", id:"greeting", css:{color:'darkblue'} })
//=> <p id=greeting style="color:darkblue">Hello</p>

// 当页面 ready 的时候，执行回调:
Zepto(function($){
  alert('Ready to Zepto!')
}) 
```

不支持[jQuery CSS 扩展](http://api.jquery.com/category/selectors/jquery-selector-extensions/)， 然而，可选的“selector”模块有限提供了支持几个最常用的伪选择器，而且可以被丢弃，与现有的代码或插件的兼容执行。

如果`$`变量尚未定义，Zepto 只设置了全局变量`$`指向它本身。允许您同时使用的 Zepto 和有用的遗留代码，例如，prototype.js。只要首先加载 Prototype，Zepto 将不会覆盖 Prototype 的 `$` 函数。Zepto 将始终设置全局变量`Zepto`指向它本身。

## $.camelCase v1.0+

```js
$.camelCase(string)   => string 
```

将一组字符串变成“骆驼”命名法的新字符串，如果该字符已经是“骆驼”命名法，则不变化。

```js
$.camelCase('hello-there') //=> "helloThere"
$.camelCase('helloThere')  //=> "helloThere" 
```

## $.contains v1.0+

```js
$.contains(parent, node)   => boolean 
```

检查父节点是否包含给定的 dom 节点，如果两者是相同的节点，则返回 `false`。

## $.each

```js
$.each(collection, function(index, item){ ... })   => collection 
```

遍历数组元素或以 key-value 值对方式遍历对象。回调函数返回 `false` 时停止遍历。

```js
$.each(['a', 'b', 'c'], function(index, item){
  console.log('item %d is: %s', index, item)
})

var hash = { name: 'zepto.js', size: 'micro' }
$.each(hash, function(key, value){
  console.log('%s: %s', key, value)
}) 
```

## $.extend

```js
$.extend(target, [source, [source2, ...]])   => target
$.extend(true, target, [source, ...])   => target v1.0+ 
```

通过源对象扩展目标对象的属性，源对象属性将覆盖目标对象属性。

默认情况下为，复制为浅拷贝（浅复制）。如果第一个参数为 true 表示深度拷贝（深度复制）。

```js
var target = { one: 'patridge' },
    source = { two: 'turtle doves' }

$.extend(target, source)
//=> { one: 'patridge',
//     two: 'turtle doves' } 
```

## $.fn

`Zepto.fn`是一个对象，它拥有 Zepto 对象上所有可用的方法，如 `addClass()`， `attr()`，和其它方法。在这个对象添加一个方法，所有的 Zepto 对象上都能用到该方法。

这里有一个实现 Zepto 的 `empty()` 方法的例子：

```js
$.fn.empty = function(){
  return this.each(function(){ this.innerHTML = '' })
} 
```

## $.grep v1.0+

```js
$.grep(items, function(item){ ... })   => array 
```

获取一个新数组，新数组只包含回调函数中返回 ture 的数组项。

```js
$.grep([1,2,3],function(item){
    return item > 1
});//=>[2,3] 
```

## $.inArray v1.0+

```js
$.inArray(element, array, [fromIndex])   => number 
```

返回数组中指定元素的索引值（愚人码头注：以 0 为基数），如果没有找到该元素则返回`-1`。

愚人码头注：`[fromIndex]` 参数可选，表示从哪个索引值开始向后查找。

```js
$.inArray("abc",["bcd","abc","edf","aaa"]);//=>1

$.inArray("abc",["bcd","abc","edf","aaa"],1);//=>1

$.inArray("abc",["bcd","abc","edf","aaa"],2);//=>-1 
```

## $.isArray

```js
$.isArray(object)   => boolean 
```

如果 object 是 array，则返回 ture。

## $.isFunction

```js
$.isFunction(object)   => boolean 
```

如果 object 是 function，则返回 ture。

## $.isPlainObject v1.0+

```js
$.isPlainObject(object)   => boolean 
```

测试对象是否是“纯粹”的对象，这个对象是通过 对象常量（"{}"） 或者 `new Object` 创建的，如果是，则返回 true。

```js
$.isPlainObject({})         // => true
$.isPlainObject(new Object) // => true
$.isPlainObject(new Date)   // => false
$.isPlainObject(window)     // => false 
```

## $.isWindow v1.0+

```js
$.isWindow(object)   => boolean 
```

如果 object 参数是否为一个 window 对象，那么返回 true。这在处理 iframe 时非常有用，因为每个 iframe 都有它们自己的 window 对象，使用常规方法`obj === window`校验这些 objects 的时候会失败。

## $.map

```js
$.map(collection, function(item, index){ ... })   => collection 
```

通过遍历集合中的元素，返回通过迭代函数的全部结果，（愚人码头注：一个新数组）`null` 和 `undefined` 将被过滤掉。

```js
$.map([1,2,3,4,5],function(item,index){
        if(item>1){return item*item;}
}); 
// =>[4, 9, 16, 25]

$.map({"yao":1,"tai":2,"yang":3},function(item,index){
    if(item>1){return item*item;}
}); 
// =>[4, 9] 
```

## $.parseJSON v1.0+

```js
$.parseJSON(string)  ? object 
```

原生`JSON.parse`方法的别名。（愚人码头注：接受一个标准格式的 JSON 字符串，并返回解析后的 JavaScript 对象。）

## $.trim v1.0+

```js
$.trim(string)   => string 
```

删除字符串首尾的空白符。类似 String.prototype.trim()。

## $.type v1.0+

```js
$.type(object)   => string 
```

获取 JavaScript 对象的类型。可能的类型有： `null` `undefined` `boolean` `number` `string` `function` `array` `date` `regexp` `object` `error`。

对于其它对象，它只是简单报告为“object”，如果你想知道一个对象是否是一个 javascript 普通对象，使用 isPlainObject。

## add

```js
add(selector, [context])   => self 
```

添加元素到当前匹配的元素集合中。如果给定 content 参数，将只在 content 元素中进行查找，否则在整个 document 中查找。

```js
<ul>
    <li>list item 1</li>
    <li>list item 2</li>
    <li>list item 3</li>
</ul>
<p>a paragraph</p>

<script type="text/javascript">
    $('li').add('p').css('background-color', 'red');
</script> 
```

## addClass

```js
addClass(name)   => self
addClass(function(index, oldClassName){ ... })   => self 
```

为每个匹配的元素添加指定的 class 类名。多个 class 类名使用空格分隔。

## after

```js
after(content)   => self 
```

在每个匹配的元素后插入内容（愚人码头注：外部插入）。内容可以为 html 字符串，dom 节点，或者节点组成的数组。

```js
$('form label').after('<p>A note below the label</p>') 
```

## append

```js
append(content)   => self 
```

在每个匹配的元素末尾插入内容（愚人码头注：内部插入）。内容可以为 html 字符串，dom 节点，或者节点组成的数组。

```js
$('ul').append('<li>new list item</li>') 
```

## appendTo

```js
appendTo(target)   => self 
```

将匹配的元素插入到目标元素的末尾（愚人码头注：内部插入）。这个有点像 append，但是插入的目标与其相反。

```js
$('<li>new list item</li>').appendTo('ul') 
```

## attr

```js
attr(name)   => string
attr(name, value)   => self
attr(name, function(index, oldValue){ ... })   => self
attr({ name: value, name2: value2, ... })   => self 
```

读取或设置 dom 的属性。如果没有给定 value 参数，则读取对象集合中第一个元素的属性值。当给定了 value 参数。则设置对象集合中所有元素的该属性的值。当 value 参数为`null`，那么这个属性将被移除(类似 removeAttr)，多个属性可以通过对象键值对的方式进行设置。

要读取 DOM 的属性如 `checked`和`selected`, 使用 prop。

```js
var form = $('form')
form.attr('action')             //=> 读取值
form.attr('action', '/create')  //=> 设置值
form.attr('action', null)       //=> 移除属性

// 多个属性:
form.attr({
  action: '/create',
  method: 'post'
}) 
```

## before

```js
before(content)   => self 
```

在匹配每个元素的前面插入内容（愚人码头注：外部插入）。内容可以为 html 字符串，dom 节点，或者节点组成的数组。

```js
$('table').before('<p>See the following table:</p>') 
```

## children

```js
children([selector])   => collection 
```

获得每个匹配元素集合元素的直接子元素，如果给定 selector，那么返回的结果中只包含符合 css 选择器的元素。

```js
$('ol').children('*:nth-child(2n)')
//=> every other list item from every ordered list 
```

## clone v1.0+

```js
clone()   => collection 
```

通过深度克隆来复制集合中的所有元素。

此方法不会将数据和事件处理程序复制到新的元素。这点和 jquery 中利用一个参数来确定是否复制数据和事件处理不相同。

## closest

```js
closest(selector, [context])   => collection
closest(collection)   => collection v1.0+
closest(element)   => collection v1.0+ 
```

从元素本身开始，逐级向上级元素匹配，并返回最先匹配 selector 的元素。如果给定 context 节点参数，那么只匹配该节点的后代元素。这个方法与 `parents(selector)`有点相像，但它只返回最先匹配的祖先元素。

如果参数是一个 Zepto 对象集合或者一个元素，结果必须匹配给定的元素而不是选择器。

```js
var input = $('input[type=text]')
input.closest('form') 
```

## concat

```js
concat(nodes, [node2, ...])   => self 
```

添加元素到一个 Zepto 对象集合形成一个新数组。如果参数是一个数组，那么这个数组中的元素将会合并到 Zepto 对象集合中。

这是一个 Zepto 提供的方法，不是 jquey 的 API 。

## contents v1.0+

```js
contents()   => collection 
```

获得每个匹配元素集合元素的子元素，包括文字和注释节点。（愚人码头注：.contents()和.children()方法类似，只不过前者包括文本节点以及 jQuery 对象中产生的 HTML 元素。）

## css

```js
css(property)   => value
css([property1, property2, ...])   => object v1.1+
css(property, value)   => self
css({ property: value, property2: value2, ... })   => self 
```

读取或设置 DOM 元素的 css 属性。当 value 参数不存在的时候，返回对象集合中第一个元素的 css 属性。当 value 参数存在时，设置对象集合中每一个元素的对应 css 属性。

多个属性可以通过传递一个属性名组成的数组一次性获取。多个属性可以利用对象键值对的方式进行设置。

当 value 为空(空字符串，`null` 或 `undefined`)，那个 css 属性将会被移出。当 value 参数为一个无单位的数字，如果该 css 属性需要单位，“px”将会自动添加到该属性上。

```js
var elem = $('h1')
elem.css('background-color')          // read property
elem.css('background-color', '#369')  // set property
elem.css('background-color', '')      // remove property

// set multiple properties:
elem.css({ backgroundColor: '#8EE', fontSize: 28 })

// read multiple properties:
elem.css(['backgroundColor', 'fontSize'])['fontSize'] 
```

## data

```js
data(name)   => value
data(name, value)   => self 
```

读取或写入 dom 的 `data-*` 属性。行为有点像 attr ，但是属性名称前面加上 `data-`。

当读取属性值时，会有下列转换：v1.0+

*   “true”, “false”, and “null” 被转换为相应的类型；
*   数字值转换为实际的数字类型；
*   JSON 值将会被解析，如果它是有效的 JSON；
*   其它的一切作为字符串返回。

    Zepto 基本实现`data()`只能存储字符串。如果你要存储任意对象，请引入可选的“data”模块到你构建的 Zepto 中。

## each

```js
each(function(index, item){ ... })   => self 
```

遍历一个对象集合每个元素。在迭代函数中，`this`关键字指向当前项(作为函数的第二个参数传递)。如果迭代函数返回 `false`，遍历结束。

```js
$('form input').each(function(index){
  console.log('input %d is: %o', index, this)
}) 
```

## empty

```js
empty()   => self 
```

清空对象集合中每个元素的 DOM 内容。

## eq

```js
eq(index)   => collection 
```

从当前对象集合中获取给定索引值（愚人码头注：以 0 为基数）的元素。

```js
$('li').eq(0)   //=> only the first list item
$('li').eq(-1)  //=> only the last list item 
```

## filter

```js
filter(selector)   => collection
filter(function(index){ ... })   => collection v1.0+ 
```

过滤对象集合，返回对象集合中满足 css 选择器的项。如果参数为一个函数，函数返回有实际值得时候，元素才会被返回。在函数中， `this` 关键字指向当前的元素。

与此相反的功能，查看 not.

## find

```js
find(selector)   => collection
find(collection)   => collection v1.0+
find(element)   => collection v1.0+ 
```

在当对象前集合内查找符合 CSS 选择器的每个元素的后代元素。

如果给定 Zepto 对象集合或者元素，过滤它们，只有当它们在当前 Zepto 集合对象中时，才回被返回。

```js
var form = $('#myform')
form.find('input, select') 
```

## first

```js
first()   => collection 
```

获取当前对象集合中的第一个元素。

```js
$('form').first() 
```

## forEach

```js
forEach(function(item, index, array){ ... }, [context]) 
```

遍历对象集合中每个元素，有点类似 each，但是遍历函数的参数不一样，当函数返回 `false` 的时候，遍历不会停止。

这是一个 Zepto 提供的方法，不是 jquery 的 API。

## get

```js
get()   => array
get(index)   => DOM node 
```

从当前对象集合中获取所有元素或单个元素。当 index 参数不存在的时，以普通数组的方式返回所有的元素。当指定 index 时，只返回该置的元素。这点与 eq 不同，该方法返回的是 DOM 节点，不是 Zepto 对象集合。

```js
var elements = $('h2')
elements.get()   //=> get all headings as an array
elements.get(0)  //=> get first heading node 
```

## has v1.0+

```js
has(selector)   => collection
has(node)   => collection 
```

判断当前对象集合的子元素是否有符合选择器的元素，或者是否包含指定的 DOM 节点，如果有，则返回新的对象集合，该对象过滤掉不含有选择器匹配元素或者不含有指定 DOM 节点的对象。

```js
$('ol > li').has('a[href]')
//=> get only LI elements that contain links 
```

## hasClass

```js
hasClass(name)   => boolean 
```

检查对象集合中是否有元素含有指定的 class。

```js
<ul>
    <li>list item 1</li>
    <li class="yaotaiyang">list item 2</li>
    <li>list item 3</li>
</ul>
<p>a paragraph</p>

<script type="text/javascript">
    $("li").hasClass("yaotaiyang");
 //=> true
</script> 
```

## height

```js
height()   => number
height(value)   => self
height(function(index, oldHeight){ ... })   => self 
```

获取对象集合中第一个元素的高度；或者设置对象集合中所有元素的高度。

```js
$('#foo').height()   // => 123
$(window).height()   // => 838 (viewport height)
$(document).height() // => 22302 
```

## hide

```js
hide()   => self 
```

Hide elements in this collection by setting their `display` CSS property to `none`.

通过设置 css 的属性`display` 为 `none`来将对象集合中的元素隐藏。

## html

```js
html()   => string
html(content)   => self
html(function(index, oldHtml){ ... })   => self 
```

获取或设置对象集合中元素的 HTML 内容。当没有给定 content 参数时，返回对象集合中第一个元素的 innerHtml。当给定 content 参数时，用其替换对象集合中每个元素的内容。content 可以是 append 中描述的所有类型。

```js
// autolink everything that looks like a Twitter username
$('.comment p').html(function(idx, oldHtml){
  return oldHtml.replace(/(^|\W)@(\w{1,15})/g,
    '$1@<a href="http://twitter.com/$2">$2</a>')
}) 
```

## index

```js
index([element])   => number 
```

获取一个元素的索引值（愚人码头注：从 0 开始计数）。当 elemen 参数没有给出时，返回当前元素在兄弟节点中的位置。当 element 参数给出时，返回它在当前对象集合中的位置。如果没有找到该元素，则返回`-1`。

```js
$('li:nth-child(2)').index()  //=> 1 
```

## indexOf

```js
indexOf(element, [fromIndex])   => number 
```

Get the position of an element in the current collection. If fromIndex number is given, search only from that position onwards. Returns the 0-based position when found and `-1` if not found. Use of index is recommended over this method.

在当前对象集合中获取一个元素的索引值（愚人码头注：从 0 开始计数）。如果给定 formindex 参数，从该位置开始往后查找，返回基于 0 的索引值，如果没找到，则返回`-1`。index 方法是基于这个方法实现的。

这是一个 Zepto 的方法，不是 jquer 的 api。

## insertAfter

```js
insertAfter(target)   => self 
```

将集合中的元素插入到指定的目标元素后面（愚人码头注：外部插入）。这个有点像 after，但是使用方式相反。

```js
$('<p>Emphasis mine.</p>').insertAfter('blockquote') 
```

## insertBefore

```js
insertBefore(target)   => self 
```

将集合中的元素插入到指定的目标元素前面（愚人码头注：外部插入）。这个有点像 before，但是使用方式相反。

```js
$('<p>See the following table:</p>').insertBefore('table') 
```

## is

```js
is(selector)   => boolean 
```

判断当前元素集合中的第一个元素是否符 css 选择器。对于基础支持 jquery 的非标准选择器类似： `:visible`包含在可选的“selector”模块中。

[jQuery CSS extensions](http://api.jquery.com/category/selectors/jquery-selector-extensions/) 不被支持。 选择“selector”模块仅仅能支持有限几个最常用的方式。

## last

```js
last()   => collection 
```

获取对象集合中最后一个元素。

```js
$('li').last() 
```

## map

```js
map(function(index, item){ ... })   => collection 
```

遍历对象集合中的所有元素。通过遍历函数返回值形成一个新的集合对象。在遍历函数中`this`关键之指向当前循环的项（遍历函数中的第二个参数）。

遍历中返回 `null`和`undefined`，遍历将结束。

```js
// get text contents of all elements in collection
elements.map(function(){ return $(this).text() }).get().join(', ') 
```

## next

```js
next()   => collection
next(selector)   => collection v1.0+ 
```

Get the next sibling–optionally filtered by selector–of each element in the collection.

获取对象集合中每一个元素的下一个兄弟节点(可以选择性的带上过滤选择器)。

```js
$('dl dt').next()   //=> the DD elements 
```

## not

```js
not(selector)   => collection
not(collection)   => collection
not(function(index){ ... })   => collection 
```

过滤当前对象集合，获取一个新的对象集合，它里面的元素不能匹配 css 选择器。如果另一个参数为 Zepto 对象集合，那么返回的新 Zepto 对象中的元素都不包含在该参数对象中。如果参数是一个函数。仅仅包含函数执行为 false 值得时候的元素，函数的 `this` 关键字指向当前循环元素。

与它相反的功能，查看 filter.

## offset

```js
offset()   => object
offset(coordinates)   => self v1.0+
offset(function(index, oldOffset){ ... })   => self v1.0+ 
```

获得当前元素相对于 document 的位置。返回一个对象含有： `top`, `left`, `width`和`height`

当给定一个含有`left`和`top`属性对象时，使用这些值来对集合中每一个元素进行相对于 document 的定位。

## offsetParent v1.0+

```js
offsetParent()   => collection 
```

找到第一个定位过的祖先元素，意味着它的 css 中的`position` 属性值为“relative”, “absolute” or “fixed”

## parent

```js
parent([selector])   => collection 
```

获取对象集合中每个元素的直接父元素。如果 css 选择器参数给出。过滤出符合条件的元素。

## parents

```js
parents([selector])   => collection 
```

获取对象集合每个元素所有的祖先元素。如果 css 选择器参数给出，过滤出符合条件的元素。

如果想获取直接父级元素，使用 parent。如果只想获取到第一个符合 css 选择器的元素，使用 closest。

```js
$('h1').parents()   //=> [<div#container>, <body>, <html>] 
```

## pluck

```js
pluck(property)   => array 
```

获取对象集合中每一个元素的属性值。返回值为 `null`或`undefined`值得过滤掉。

```js
$('body > *').pluck('nodeName') // => ["DIV", "SCRIPT"]

// implementation of Zepto's `next` method
$.fn.next = function(){
  return $(this.pluck('nextElementSibling'))
} 
```

这是一个 Zepto 的方法，不是 jquery 的 api

## position v1.0+

```js
position()   => object 
```

获取对象集合中第一个元素的位置。相对于 offsetParent。当绝对定位的一个元素靠近另一个元素的时候，这个方法是有用的。

Returns an object with properties: `top`, `left`.

```js
var pos = element.position()

// position a tooltip relative to the element
$('#tooltip').css({
  position: 'absolute',
  top: pos.top - 30,
  left: pos.left
}) 
```

## prepend

```js
prepend(content)   => self 
```

将参数内容插入到每个匹配元素的前面（愚人码头注：元素内部插入）。插入 d 的元素可以试 html 字符串片段，一个 dom 节点，或者一个节点的数组。

```js
$('ul').prepend('<li>first list item</li>') 
```

## prependTo

```js
prependTo(target)   => self 
```

将所有元素插入到目标前面（愚人码头注：元素内部插入）。这有点像 prepend，但是是相反的方式。

```js
$('<li>first list item</li>').prependTo('ul') 
```

## prev

```js
prev()   => collection
prev(selector)   => collection v1.0+ 
```

获取对象集合中每一个元素的前一个兄弟节点，通过选择器来进行过滤。

## prop v1.0+

```js
prop(name)   => value
prop(name, value)   => self
prop(name, function(index, oldValue){ ... })   => self 
```

读取或设置 dom 元素的属性值。它在读取属性值的情况下优先于 attr，因为这些属性值会因为用户的交互发生改变，如`checked` 和 `selected`。

简写或小写名称，比如`for`, `class`, `readonly`及类似的属性，将被映射到实际的属性上，比如`htmlFor`, `className`, `readOnly`, 等等。

## push

```js
push(element, [element2, ...])   => self 
```

Add elements to the end of the current collection.

添加元素到当前对象集合的最后。

这是一个 zepto 的方法，不是 jquery 的 api

## ready

```js
ready(function($){ ... })   => self 
```

添加一个事件侦听器，当页面 DOM 加载完毕 “DOMContentLoaded” 事件触发时触发。建议使用 $())来代替这种用法。

## reduce

```js
reduce(function(memo, item, index, array){ ... }, [initial])   => value 
```

与 [Array.reduce](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array/Reduce)有相同的用法，遍历当前对象集合。memo 是函数上次的返回值。迭代进行遍历。

这是一个 zepto 的方法，不是 jquery 的 api

## remove

```js
remove()   => self 
```

从其父节点中删除当前集合中的元素，有效的从 dom 中移除。

## removeAttr

```js
removeAttr(name)   => self 
```

移除当前对象集合中所有元素的指定属性。

## removeClass

```js
removeClass([name])   => self
removeClass(function(index, oldClassName){ ... })   => self 
```

移除当前对象集合中所有元素的指定 class。如果没有指定 name 参数，将移出所有的 class。多个 class 参数名称可以利用空格分隔。下例移除了两个 class。

```js
<input class="taiyang yueliang" id="check1" type="checkbox" checked="checked">
<input class="yaotaiyang" id="check2" type="checkbox">

<script type="text/javascript">
    $("#check1").removeClass("taiyang yueliang")
    //=>[<input class id="check1" type="checkbox" checked="checked">]
</script> 
```

## replaceWith

```js
replaceWith(content)   => self 
```

用给定的内容替换所有匹配的元素。(包含元素本身)。content 参数可以为 before 中描述的类型。

## scrollLeft v1.1+

```js
scrollLeft()   => number
scrollLeft(value)   => self 
```

获取或设置页面上的滚动元素或者整个窗口向右滚动的像素值。

## scrollTop v1.0+

```js
scrollTop()   => number
scrollTop(value)   => self v1.1+ 
```

获取或设置页面上的滚动元素或者整个窗口向下滚动的像素值。

## show

```js
show()   => self 
```

恢复对象集合中每个元素默认的“display”值。如果你用 hide 将元素隐藏，用该属性可以将其显示。相当于去掉了`display：none`。

## siblings

```js
siblings([selector])   => collection 
```

获取对象集合中所有元素的兄弟节点。如果给定 CSS 选择器参数，过滤出符合选择器的元素。

## size

```js
size()   => number 
```

获取对象集合中元素的数量。

## slice

```js
slice(start, [end])   => array 
```

提取这个数组`array`的子集，从`start`开始，如果给定`end`，提取从从`start`开始到`end`结束的元素，但是不包含`end`位置的元素。

## text

```js
text()   => string
text(content)   => self
text(function(index, oldText){ ... })   => self v1.1.4+ 
```

获取或者设置所有对象集合中元素的文本内容。当没有给定 content 参数时，返回当前对象集合中第一个元素的文本内容（包含子节点中的文本内容）。当给定 content 参数时，使用它替换对象集合中所有元素的文本内容。它有待点似 html，与它不同的是它不能用来获取或设置 HTML。

## toggle

```js
toggle([setting])   => self 
```

显示或隐藏匹配元素。如果 `setting`为 true，相当于 show 法。如果`setting`为 false。相当于 hide 方法。

```js
var input = $('input[type=text]')
$('#too_long').toggle(input.val().length > 140) 
```

## toggleClass

```js
toggleClass(names, [setting])   => self
toggleClass(function(index, oldClassNames){ ... }, [setting])   => self 
```

在匹配的元素集合中的每个元素上添加或删除一个或多个样式类。如果 class 的名称存在则删除它，如果不存在，就添加它。如果 `setting`的值为真，这个功能类似于 addClass，如果为假，这个功能类似与 removeClass。

## unwrap

```js
unwrap()   => self 
```

移除集合中每个元素的直接父节点，并把他们的子元素保留在原来的位置。 基本上，这种方法删除上一的祖先元素，同时保持 DOM 中的当前元素。

```js
$(document.body).append('<div id=wrapper><p>Content</p></div>')
$('#wrapper p').unwrap().parents()  //=> [<body>, <html>] 
```

## val

```js
val()   => string
val(value)   => self
val(function(index, oldValue){ ... })   => self 
```

获取或设置匹配元素的值。当没有给定 value 参数，返回第一个元素的值。如果是`&lt;select multiple&gt;`标签，则返回一个数组。当给定 value 参数，那么将设置所有元素的值。

## width

```js
width()   => number
width(value)   => self
width(function(index, oldWidth){ ... })   => self 
```

获取对象集合中第一个元素的宽；或者设置对象集合中所有元素的宽。

```js
$('#foo').width()   // => 123
$(window).width()   // => 768 (viewport width)
$(document).width() // => 768 
```

## wrap

```js
wrap(structure)   => self
wrap(function(index){ ... })   => self v1.0+ 
```

在每个匹配的元素外层包上一个 html 元素。structure 参数可以是一个单独的元素或者一些嵌套的元素。也可以是一个 html 字符串片段或者 dom 节点。还可以是一个生成用来包元素的回调函数，这个函数返回前两种类型的包裹片段。

**需要提醒的是：**该方法对于 dom 中的节点有着很好的支持。如果将`wrap()` 用在一个新的元素上，然后再将结果插入到 document 中，此时该方法无效。

```js
// wrap each button in a separate span:
$('.buttons a').wrap('<span>')

// wrap each code block in a div and pre:
$('code').wrap('<div class=highlight><pre /></div>')

// wrap all form inputs in a span with classname
// corresponding to input type:
$('input').wrap(function(index){
  return '<span class=' + this.type + 'field />'
})
//=> <span class=textfield><input type=text /></span>,
//   <span class=searchfield><input type=search /></span>

// WARNING: will not work as expected!
$('<em>broken</em>').wrap('<li>').appendTo(document.body)
// do this instead:
$('<em>better</em>').appendTo(document.body).wrap('<li>') 
```

## wrapAll

```js
wrapAll(structure)   => self 
```

在所有匹配元素外面包一个单独的结构。结构可以是单个元素或 几个嵌套的元素，并且可以通过在作为 HTML 字符串或 DOM 节点。

```js
// wrap all buttons in a single div:
$('a.button').wrapAll('<div id=buttons />') 
```

## wrapInner

```js
wrapInner(structure)   => self
wrapInner(function(index){ ... })   => self v1.0+ 
```

将每个元素中的*内容*包裹在一个单独的结构中。结构可以是单个元件或多个嵌套元件，并且可以通过在作为 HTML 字符串或 DOM 节点，或者是一个生成用来包元素的回调函数，这个函数返回前两种类型的包裹片段。

```js
// wrap the contents of each navigation link in a span:
$('nav a').wrapInner('<span>')

// wrap the contents of each list item in a paragraph and emphasis:
$('ol li').wrapInner('<p><em /></p>') 
```