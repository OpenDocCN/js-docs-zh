# 事件处理

# 事件处理

## $.Event

```
$.Event(type, [properties])   => event 
```

创建并初始化一个指定的 DOM 事件。如果给定 properties 对象，使用它来扩展出新的事件对象。默认情况下，事件被设置为冒泡方式；这个可以通过设置`bubbles`为`false`来关闭。

一个事件初始化的函数可以使用 trigger 来触发。

```
$.Event('mylib:change', { bubbles: false }) 
```

## $.proxy v1.0+

```
$.proxy(fn, context)   => function
$.proxy(fn, context, [additionalArguments...])   => function v1.1.4+
$.proxy(context, property)   => function
$.proxy(context, property, [additionalArguments...])   => function v1.1.4+ 
```

接受一个函数，然后返回一个新函数，并且这个新函数始终保持了特定的上下文(context)语境，新函数中`this`指向 context 参数。另外一种形式，原始的 function 是从上下文(context)对象的特定属性读取。

如果传递超过 2 个的额外参数，它们被用于 传递给 fn 参数的函数 引用。

```
var obj = {name: 'Zepto'},
    handler = function(){ console.log("hello from + ", this.name) }

// ensures that the handler will be executed in the context of `obj`:
$(document).on('click', $.proxy(handler, obj)) 
```

## bind

不推荐, 使用 on 代替。

```
bind(type, function(e){ ... })   => self
bind(type, [data], function(e){ ... })   => self v1.1+
bind({ type: handler, type2: handler2, ... })   => self
bind({ type: handler, type2: handler2, ... }, [data])   => self v1.1+ 
```

为一个元素绑定一个处理事件。

## delegate

不推荐, 使用 on 代替。

```
delegate(selector, type, function(e){ ... })   => self
delegate(selector, { type: handler, type2: handler2, ... })   => self 
```

基于一组特定的根元素为所有选择器匹配的元素附加一个处理事件，匹配的元素可能现在或将来才创建。

## die

不推荐, 使用 on 代替。

```
die(type, function(e){ ... })   => self
die({ type: handler, type2: handler2, ... })   => self 
```

删除通过 live 添加的事件。

## event.isDefaultPrevented v1.1+

```
event.isDefaultPrevented()   => boolean 
```

如果`preventDefault()`被该事件的实例调用，那么返回 true。 这可作为跨平台的替代原生的 `defaultPrevented`属性，如果 `defaultPrevented`缺失或在某些浏览器下不可靠的时候。

```
// trigger a custom event and check whether it was cancelled
var event = $.Event('custom')
element.trigger(event)
event.isDefaultPrevented() 
```

## event.isImmediatePropagationStopped v1.1+

```
event.isImmediatePropagationStopped()   => boolean 
```

如果`stopImmediatePropagation()`被该事件的实例调用，那么返回 true。Zepto 在不支持该原生方法的浏览器中实现它， （例如老版本的 Android）。

## event.isPropagationStopped v1.1+

```
event.isPropagationStopped()   => boolean 
```

如果`stopPropagation()`被该事件的实例调用，那么返回 true。

## live

不推荐, 使用 on 代替。

```
live(type, function(e){ ... })   => self
live({ type: handler, type2: handler2, ... })   => self 
```

类似 delegate，添加一个个事件处理器到符合目前选择器的所有元素匹配，匹配的元素可能现在或将来才创建。

## off

```
off(type, [selector], function(e){ ... })   => self
off({ type: handler, type2: handler2, ... }, [selector])   => self
off(type, [selector])   => self
off()   => self 
```

移除通过 on 添加的事件.移除一个特定的事件处理程序， 必须通过用`on()`添加的那个相同的函数。否则，只通过事件类型调用此方法将移除该类型的所有处理程序。如果没有参数，将移出当前元素上*全部*的注册事件。

## on

```
on(type, [selector], function(e){ ... })   => self
on(type, [selector], [data], function(e){ ... })   => self v1.1+
on({ type: handler, type2: handler2, ... }, [selector])   => self
on({ type: handler, type2: handler2, ... }, [selector], [data])   => self v1.1+ 
```

添加事件处理程序到对象集合中得元素上。多个事件可以通过空格的字符串方式添加，或者以事件类型为键、以函数为值的对象 方式。如果给定 css 选择器，当事件在匹配该选择器的元素上发起时，事件才会被触发（愚人码头注：即事件委派，或者说事件代理）。

如果给定`data`参数，这个值将在事件处理程序执行期间被作为有用的 `event.data` 属性

事件处理程序在添加该处理程序的元素、或在给定选择器情况下匹配该选择器的元素的上下文中执行(愚人码头注：this 指向触发事件的元素)。 当一个事件处理程序返回`false`，`preventDefault()` 和 `stopPropagation()`被当前事件调用的情况下， 将防止默认浏览器操作，如链接。

如果`false` 在回调函数的位置上作为参数传递给这个方法， 它相当于传递一个函数，这个函数直接返回`false`。（愚人码头注：即将 `false` 当作 `function(e){ ... }` 的参数，作为 `function(){ return false; }` 的简写形式，例如： `$("a.disabled").on("click", false);`这相当于`$("a.disabled").on("click", function(){ return false; } );`）

```
var elem = $('#content')
// observe all clicks inside #content:
elem.on('click', function(e){ ... })
// observe clicks inside navigation links in #content
elem.on('click', 'nav a', function(e){ ... })
// all clicks inside links in the document
$(document).on('click', 'a', function(e){ ... })
// disable following any navigation link on the page
$(document).on('click', 'nav a', false) 
```

## one

```
one(type, [selector], function(e){ ... })   => self
one(type, [selector], [data], function(e){ ... })   => self v1.1+
one({ type: handler, type2: handler2, ... }, [selector])   => self
one({ type: handler, type2: handler2, ... }, [selector], [data])   => self v1.1+ 
```

添加一个处理事件到元素，当第一次执行事件以后，该事件将自动解除绑定，保证处理函数在每个元素上最多执行一次。`selector` 和 `data` 等参数说明请查看`.on()`。

## trigger

```
trigger(event, [args])   => self 
```

在对象集合的元素上触发指定的事件。事件可以是一个字符串类型，也可以是一个 通过$.Event 定义的事件对象。如果给定 args 参数，它会作为参数传递给事件函数。

```
// add a handler for a custom event
$(document).on('mylib:change', function(e, from, to){
  console.log('change on %o with data %s, %s', e.target, from, to)
})
// trigger the custom event
$(document.body).trigger('mylib:change', ['one', 'two']) 
```

Zepto 仅仅支持在 dom 元素上触发事件。

## triggerHandler

```
triggerHandler(event, [args])   => self 
```

像 trigger，它只在当前元素上触发事件，但不冒泡。

```
 $("input").triggerHandler('focus');
        // 此时 input 上的 focus 事件触发，但是 input 不会获取焦点
        $("input").trigger('focus');
        // 此时 input 上的 focus 事件触发，input 获取焦点 
```

## unbind

Deprecated, use off instead.

```
unbind(type, function(e){ ... })   => self
unbind({ type: handler, type2: handler2, ... })   => self 
```

移除通过 bind 注册的事件。

## undelegate

Deprecated, use off instead.

```
undelegate(selector, type, function(e){ ... })   => self
undelegate(selector, { type: handler, type2: handler2, ... })   => self 
```

移除通过 delegate 注册的事件。