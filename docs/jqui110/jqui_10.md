# Utilities

## Easings

Easing 函数指定动画在不同点上的行进速度。

Also in: [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## Widget Factory

使用与所有 jQuery UI 小部件相同的抽象化来创建有状态的 jQuery 插件。

Also in: [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## Widget Plugin Bridge

jQuery.widget.bridge() 方法是 jQuery 部件库（Widget Factory）的一部分。它扮演着由 $.widget() 创建的对象和 jQuery API 之间的中介。

Also in: [Interactions](http://www.css88.com/jquery-ui-api/category/interactions/ "View all posts in Interactions")

## Mouse Interaction

基本交互层。

Also in: [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods")

## .position()

相对另一个元素定位一个元素。

# Widget Factory

Categories: [Utilities](http://www.css88.com/jquery-ui-api/category/utilities/ "View all posts in Utilities") | [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

*   [jQuery.widget( name [, base ], prototype )](#jQuery-widget1)
    *   [jQuery.widget( name [, base ], prototype )](#jQuery-widget-name-base-prototype)
*   jQuery.Widget

## jQuery.widget( name [, base ], prototype )

**Description:** 使用与所有 jQuery UI 小部件相同的抽象化来创建有状态的 jQuery 插件。

*   #### [jQuery.widget( name [, base ], prototype )](#jQuery-widget-name-base-prototype)

    *   **name**Type: [String](http://api.jquery.com/Types/#String)要创建的小部件名称，包括命名空间。
    *   **base**Type: [Function](http://api.jquery.com/Types/#Function)()要继承的基础小部件。必须是一个可以使用 `new` 关键词实例化的构造函数。默认为 `jQuery.Widget`。
    *   **prototype**Type: [PlainObject](http://api.jquery.com/Types/#PlainObject)要作为小部件原型使用的对象。

您可以使用 `$.Widget` 对象作为要继承的基础，或者可以明确地从现有的 jQuery UI 或第三方控件，从头开始创建新的小部件。定义一个带有相同名称的小部件来继承基础部件，甚至允许您适当地扩展小部件。

jQuery UI 中包含许多保持状态的小部件，因此比典型的 jQuery 插件稍有不同的使用模式。所有的 jQuery UI 小部件使用相同的模式，这是由部件库（Widget Factory）定义的。所以，只要您学会使用其中一个，您就知道如何使用其他的小部件（Widget）。

寻找有关小部件工厂的教程？查看[jQuery 学习中心的文章](http://learn.jquery.com/jquery-ui/widget-factory/)。

注意：本章节使用 进度条部件（Progressbar Widget） 演示实例，但是语法适用于每个小部件。

### 初始化

为了跟踪小部件的状态，我们必须引入小部件的全生命周期。小部件初始化时生命周期开始。要初始化一个小部件，我们只需要简单地在一个或多个元素上调用插件。

```
$( "#elem" ).progressbar(); 
```

这将初始化 jQuery 对象中的每个元素。上面实例中元素 id 为 `"elem"`。

### 选项

由于 `progressbar()` 调用时不带参数，小部件是使用默认选项进行初始化的。我们可以在初始化时传递一组选项来覆盖默认选项：

```
$( "#elem" ).progressbar({ value: 20 }); 
```

我们可以根据需要传递选项的个数，任何我们未传递的选项都使用它们的默认值。

您可以传递多个选项参数，这些参数将会被合并为一个对象（类似于 `$.extend( true, target, object1, objectN )`）。这在为所有实例覆盖一些设置，实例间共享选项时很有用：

```
var options = { modal: true, show: "slow" };
$( "#dialog1" ).dialog( options );
$( "#dialog2" ).dialog( options, { autoOpen: false }); 
```

所有在初始化时传递的选项都是深拷贝的，确保后续在不影响小部件的情况下修改对象。数组是唯一的例外，它们是按原样引用的。这个例外是为了适当地支持数据绑定，其中数据源必须作为引用。

默认值保存在小部件的属性中，因此我们可以覆盖 jQuery UI 设置的值。例如，在下面的设置后，所有将来的进度条实例将默认为值 80：

```
$.ui.progressbar.prototype.options.value = 80; 
```

选项是小部件状态的组成部分，所以我们也可以在初始化后设置选项。我们会在后续看到 option 方法。

### 方法

现在小部件已经初始化，我们可以查询它的状态，或者在小部件上执行动作。所有初始化后的动作都是以方法调用方式执行。为了在小部件上调用一个方法，我们向 jQuery 插件传递方法的名称。例如，在进度条部件（Progressbar Widget）上调用 `value()` 方法，我们可以使用：

```
$( "#elem" ).progressbar( "value" ); 
```

如果方法接受参数，我们可以在方法名称后传递参数。例如，要传递参数 `40` 到 `value()` 方法，我们可以使用：

```
$( "#elem" ).progressbar( "value", 40 ); 
```

就像 jQuery 中的其他方法，大多数的小部件方法返回 jQuery 对象：

```
$( "#elem" )
  .progressbar( "value", 90 )
  .addClass( "almost-done" ); 
```

每个小部件都有自己的方法设置，这些设置是基于小部件提供的功能。但是，有一些方法是存在于所有的小部件上，这会在下面进行详细讲解。

### 事件

所有的小部件都有与它们各种行为相关的事件，以便在状态改变的时候通知您。对于大多数的小部件，当事件被触发时，名称以小部件名称的小写字母形式作为前缀。例如，我们可以绑定进度条的 `change` 事件，该事件在值改变时触发。

```
$( "#elem" ).bind( "progressbarchange", function() {
  alert( "The value has changed!" );
}); 
```

每个事件都有一个对应的回调，这会作为选项。如果需要，我们可以抓住进度条的 `change` 回调，而不用绑定 `progressbarchange` 事件。

```
$( "#elem" ).progressbar({
  change: function() {
    alert( "The value has changed!" );
  }
}); 
```

所有的小部件都有一个 `change` 事件，该事件在实例化时触发。

### 实例化

小部件的实例是使用带有小部件全称作为键的 `jQuery.data()` 存储的。因此，您可以使用下面代码从元素检索进度条部件（Progressbar Widget）的实例对象。

```
$( "#elem" ).data( "ui-progressbar" ); 
```

元素是否绑定了给定小部件，可以使用 `:data` 选择器来检测。

```
$( "#elem" ).is( ":data( 'ui-progressbar' )" ); // true
$( "#elem" ).is( ":data( 'ui-draggable' )" ); // false 
```

您也可以使用 `:data` 来获得作为给定小部件实例的所有元素的列表。

```
$( ":data( 'ui-progressbar' )" ); 
```

### 属性

所有的小部件都有下面的属性：

*   **defaultElement**：当构造小部件实例未提供元素时要使用的元素。例如，由于进度条的 `defaultElement` 是 `"&lt;div&gt;`"，`$.ui.progressbar({ value: 50 })` 在一个新建的 `&lt;div&gt;` 上实例化进度条小部件实例。
*   **document**：其内包含小部件元素的 `document`。如果需要在框架内与小部件进行交互时很有用。
*   **element**：一个 jQuery 对象，包含用于实例化小部件的 元素。如果您选择多个元素并调用 `.myWidget()`，将为每个元素创建一个单独的小部件实例。因此，该属性总是包含一个元素。
*   **namespace**：小部件原型存储的全局 jQuery 对象的位置。例如，`"ui"` 的 `namespace` 表示小部件原型存储在 `$.ui`。
*   **options**：一个包含小部件当前使用选项的对象。在实例化时，用户提供的任何选项将会自动与 `$.myNamespace.myWidget.prototype.options` 中定义的默认值合并。用户指定的选项会覆盖默认值。
*   **uuid**：一个表示控件标识符的唯一整数。
*   **version**：小部件的字符串版本。对于 jQuery UI 小部件，该属性会被设置为小部件使用的 jQuery UI 的版本。插件开发者必须在他们的原型中明确设置该属性。
*   **widgetEventPrefix**：添加到小部件事件名称的前缀。例如，可拖拽小部件（Draggable Widget） 的 `widgetEventPrefix` 是 `"drag"`，因此当创建一个 draggable 时，事件的名称是 `"dragcreate"`。默认情况下，小部件的 `widgetEventPrefix` 是它的名称。*注意：该属性已被废弃，将在以后的版本中非常。事件名称将被改为 widgetName:eventName （例如 `"draggable:create"`）。*
*   **widgetFullName**：包含命名空间的小部件全称。对于 `$.widget( "myNamespace.myWidget", {} )`， `widgetFullName` 将是 `"myNamespace-myWidget"`。
*   **widgetName**：小部件的名称。对于 `$.widget( "myNamespace.myWidget", {} )`，`widgetName` 将是 `"myWidget"`。
*   **window**：其内包含小部件元素的 `window`。如果需要在框架内与小部件进行交互时很有用。

**Description:** 部件库（Widget Factory）使用的基础小部件。

## QuickNav

### Options

*   disabled
*   hide
*   show

### Methods

*   _create
*   _delay
*   _destroy
*   _focusable
*   _getCreateEventData
*   _getCreateOptions
*   _hide
*   _hoverable
*   _init
*   _off
*   _on
*   _setOption
*   _setOptions
*   _show
*   _super
*   _superApply
*   _trigger
*   destroy
*   disable
*   enable
*   option
*   widget

### Events

*   create

## Options

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为 `true`，则禁用该小部件。**Code examples:**

初始化带有指定 `disabled` 选项的小部件：

```
$( ".selector" ).widget({ disabled: true }); 
```

在初始化后，获取或设置`disabled` 选项：

```
// getter
var disabled = $( ".selector" ).widget( "option", "disabled" );

// setter
$( ".selector" ).widget( "option", "disabled", true ); 
```

### hide**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String) or [Object](http://api.jquery.com/Types/#Object)

**Default:** `null`是否使用动画隐藏元素，以及如何动画隐藏元素。**支持多个类型：**

*   **Boolean**：当设置为 `false` 时，则不使用动画，元素会立即隐藏。当设置为 `true` 时，元素会使用默认的持续时间和默认的 easing 淡出。
*   **Number**：元素将使用指定的持续时间和默认的 easing 淡出。
*   **String**：元素将使用指定的特效隐藏。该值可以是一个内建的 jQuery 动画方法名称，比如 `"slideUp"`，也可以是一个 jQuery UI 特效 的名称，比如`"fold"`。以上两种情况的特效将使用默认的持续时间和默认的 easing。
*   **Object**：如果值是一个对象，则 `effect`、`delay`、`duration` 和 `easing` 属性会被提供。如果 `effect` 属性包含 jQuery 方法的名称，则使用该方法，否则，它被认为是一个 jQuery UI 特效的名称。当使用一个支持额外设置的 jQuery UI 特效时，您可以在对象中包含这些设置，且它们会被传递给特效。如果 `duration` 或 `easing` 被省略，则使用默认值。如果 `effect` 被省略，则使用 `"fadeOut"`。如果 `delay` 被省略，则不使用延迟。

**Code examples:**

初始化带有指定 `hide` 选项的小部件：

```
$( ".selector" ).widget({ hide: { effect: "explode", duration: 1000 } }); 
```

在初始化后，获取或设置`hide` 选项：

```
// getter
var hide = $( ".selector" ).widget( "option", "hide" );

// setter
$( ".selector" ).widget( "option", "hide", { effect: "explode", duration: 1000 } ); 
```

### show**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String) or [Object](http://api.jquery.com/Types/#Object)

**Default:** `null`是否使用动画显示元素，以及如何动画显示元素。**支持多个类型：**

*   **Boolean**：当设置为 `false` 时，则不使用动画，元素会立即显示。当设置为 `true` 时，元素会使用默认的持续时间和默认的 easing 淡入。
*   **Number**：元素将使用指定的持续时间和默认的 easing 淡入。
*   **String**：元素将使用指定的特效显示。该值可以是一个内建的 jQuery 动画方法名称，比如 `"slideDown"`，也可以是一个 jQuery UI 特效 的名称，比如`"fold"`。以上两种情况的特效将使用默认的持续时间和默认的 easing。
*   **Object**：如果值是一个对象，则 `effect`、`delay`、`duration` 和 `easing` 属性会被提供。如果 `effect` 属性包含 jQuery 方法的名称，则使用该方法，否则，它被认为是一个 jQuery UI 特效的名称。当使用一个支持额外设置的 jQuery UI 特效时，您可以在对象中包含这些设置，且它们会被传递给特效。如果 `duration` 或 `easing` 被省略，则使用默认值。如果 `effect` 被省略，则使用 `"fadeIn"`。如果 `delay` 被省略，则不使用延迟。

**Code examples:**

初始化带有指定 `show` 选项的小部件：

```
$( ".selector" ).widget({ show: { effect: "blind", duration: 800 } }); 
```

在初始化后，获取或设置`show` 选项：

```
// getter
var show = $( ".selector" ).widget( "option", "show" );

// setter
$( ".selector" ).widget( "option", "show", { effect: "blind", duration: 800 } ); 
```

## Methods

### _create()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

`_create()` 方法是小部件的构造函数。没有参数，但是 `this.element` 和 `this.options` 已经设置。

*   该方法不接受任何参数。

**Code examples:**

基于一个选项设置小部件元素的背景颜色。

```
_create: function() {
  this.element.css( "background-color", this.options.color );
} 
```

### _delay( fn [, delay ] )Returns: [Number](http://api.jquery.com/Types/#Number)

在指定延迟后调用提供的函数。保持 `this` 上下文正确。本质上是 `setTimeout()`。

使用 `clearTimeout()` 返回超时 ID。

*   **fn**Type: [Function](http://api.jquery.com/Types/#Function)() or [String](http://api.jquery.com/Types/#String)要调用的函数。也可以是小部件上方法的名称。
*   **delay**Type: [Number](http://api.jquery.com/Types/#Number)调用函数前等待的毫秒数，默认为 `0`。

**Code examples:**

100 毫秒后在小部件上调用 `_foo()` 方法。

```
this._delay( this._foo, 100 ); 
```

### _destroy()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

公共的 `destroy()` 方法清除所有的公共数据、事件等等。代表了定制、指定小部件、清理的 `_destroy()`。

*   该方法不接受任何参数。

**Code examples:**

当小部件被销毁时，从小部件的元素移除一个 class。

```
_destroy: function() {
  this.element.removeClass( "my-widget" );
} 
```

### _focusable( element )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

建立聚焦在元素上时要应用 `ui-state-focus` 的 `element`。

事件处理程序在销毁时自动清理。

*   **element**Type: [jQuery](http://api.jquery.com/Types/#jQuery)要应用 focusable 行为的元素。

**Code examples:**

向小部件内的一组元素应用 focusable 样式：

```
this._focusable( this.element.find( ".my-items" ) ); 
```

### _getCreateEventData()Returns: [Object](http://api.jquery.com/Types/#Object)

所有的小部件触发 `create` 事件。默认情况下，事件中不提供任何的数据，但是该方法会返回一个对象，作为 `create` 事件的数据被传递。

*   该方法不接受任何参数。

**Code examples:**

向 `create` 事件处理程序传递小部件的选项，作为参数。

```
_getCreateEventData: function() {
  return this.options;
} 
```

### _getCreateOptions()Returns: [Object](http://api.jquery.com/Types/#Object)

该方法允许小部件在初始化期间为定义选项定义一个自定义的方法。用户提供的选项会覆盖该方法返回的选项，即会覆盖默认的选项。

*   该方法不接受任何参数。

**Code examples:**

让小部件元素的 id 属性作为选项可用。

```
_getCreateOptions: function() {
  return { id: this.element.attr( "id" ) };
} 
```

### _hide( element, option [, callback ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

使用内置的动画方法或使用自定义的特效隐藏一个元素。如需了解可能的 `option` 值，请查看 hide。

*   **element**Type: [jQuery](http://api.jquery.com/Types/#jQuery)要隐藏的元素。
*   **option**Type: [Object](http://api.jquery.com/Types/#Object)定义如何隐藏元素的设置。
*   **callback**Type: [Function](http://api.jquery.com/Types/#Function)()元素完全隐藏后要调用的回调。

**Code examples:**

为自定义动画传递 `hide` 选项。

```
this._hide( this.element, this.options.hide, function() {

  // Remove the element from the DOM when it's fully hidden.
  $( this ).remove();
}); 
```

### _hoverable( element )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

建立悬浮在元素上时要应用 `ui-state-hover` class 的 `element`。

事件处理程序在销毁时自动清理。

*   **element**Type: [jQuery](http://api.jquery.com/Types/#jQuery)要应用 hoverable 行为的元素。

**Code examples:**

当悬浮在元素上时，向元素内所有的 `&lt;div&gt;` 应用 hoverable 样式。

```
this._hoverable( this.element.find( "div" ) ); 
```

### _init()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

小部件初始化的理念与创建不同。任何时候不带参数的调用插件或者只带一个选项哈希的调用插件，初始化小部件。当小部件被创建时会包含这个方法。

*注意：如果存在不带参数成功调用小部件时要执行的逻辑动作，初始化只能在这时处理。*

*   该方法不接受任何参数。

**Code examples:**

如果设置了 `autoOpen` 选项，则调用 `open()` 方法。

```
_init: function() {
  if ( this.options.autoOpen ) {
    this.open();
  }
} 
```

### _off( element, eventName )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

从指定的元素取消绑定事件处理程序。

*   **element**Type: [jQuery](http://api.jquery.com/Types/#jQuery)要取消绑定事件处理程序的元素。不像 `_on()` 方法，`_off()` 方法中元素是必需的。
*   **eventName**Type: [String](http://api.jquery.com/Types/#String)一个或多个空格分隔的事件类型。

**Code examples:**

从小部件的元素上取消绑定所有 click 事件。

```
this._off( this.element, "click" ); 
```

### _on( [suppressDisabledCheck ] [, element ], handlers )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

授权通过事件名称内的选择器被支持，例如 "`click .foo`"。`_on()` 方法提供了一些直接事件绑定的好处：

*   保持处理程序内适当的 `this` 上下文。
*   自动处理禁用的部件：如果小部件被禁用或事件发生在带有 `ui-state-disabled` class 的元素上，则不调用事件处理程序。可以被 `suppressDisabledCheck` 参数重写。
*   事件处理程序会自动添加命名空间，在销毁时会自自动清理。

*   **suppressDisabledCheck** (default: `false`)Type: [Boolean](http://api.jquery.com/Types/#Boolean)是否要绕过禁用的检查。

*   **element**Type: [jQuery](http://api.jquery.com/Types/#jQuery)要绑定事件处理程序的元素。如果未提供元素，`this.element` 用于未授权的事件， widget 元素 用于授权的事件。
*   **handlers**Type: [Object](http://api.jquery.com/Types/#Object)一个 map，其中字符串键代表事件类型，可选的选择器用于授权，值代表事件调用的处理函数。

**Code examples:**

放置小部件元素内所有被点击的链接的默认行为。

```
this._on( this.element, {
  "click a": function( event ) {
    event.preventDefault();
  }
}); 
```

### _setOption( key, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

为每个独立的选项调用 `_setOptions()` 方法。小部件状态随着改变而更新。

*   **key**Type: [String](http://api.jquery.com/Types/#String)要设置的选项名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)为选项设置的值。

**Code examples:**

当小部件的 `height` 或 `width` 选项改变时，更新小部件的元素。

```
_setOption: function( key, value ) {
  if ( key === "width" ) {
    this.element.width( value );
  }
  if ( key === "height" ) {
    this.element.height( value );
  }
  this._super( key, value );
} 
```

### _setOptions( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

当调用 `option()` 方法时调用，无论以什么形式调用 `option()`。

如果您要根据多个选项的改变而改变处理器密集型，重载该方法是很有用的。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的选项-值对。

**Code examples:**

如果小部件的 `height` 或 `width` 选项改变，调用 `resize()` 方法。

```
_setOptions: function( options ) {
  var that = this,
    resize = false;

  $.each( options, function( key, value ) {
    that._setOption( key, value );
    if ( key === "height" || key === "width" ) {
      resize = true;
    }
  });

  if ( resize ) {
    this.resize();
  }
} 
```

### _show( element, option [, callback ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

使用内置的动画方法或使用自定义的特效显示一个元素。如需了解可能的 `option` 值，请查看 show。

*   **element**Type: [jQuery](http://api.jquery.com/Types/#jQuery)要显示的元素。
*   **option**Type: [Object](http://api.jquery.com/Types/#Object)定义如何显示元素的设置。
*   **callback**Type: [Function](http://api.jquery.com/Types/#Function)()元素完全显示后要调用的回调。

**Code examples:**

为自定义动画传递 `show` 选项。

```
this._show( this.element, this.options.show, function() {

  // Focus the element when it's fully visible.
  this.focus();
} 
```

### _super( [arg ] [, ... ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

从父部件中调用相同名称的方法，带有任意指定的参数。本质上是`.call()`。

*   **arg**Type: [Object](http://api.jquery.com/Types/#Object)要传递给父部件的方法的零到多个参数。

**Code examples:**

处理 `title` 选项更新，并调用付部件的 `_setOption()` 来更新选项的内部存储。

```
_setOption: function( key, value ) {
  if ( key === "title" ) {
    this.element.find( "h3" ).text( value );
  }
  this._super( key, value );
} 
```

### _superApply( arguments )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

从父部件中调用相同名称的方法，带有参数的数组。本质上是 `.apply()`。

*   **arguments**Type: [Array](http://api.jquery.com/Types/#Array)要传递给父部件的方法的参数数组。

**Code examples:**

处理 `title` 选项更新，并调用付部件的 `_setOption()` 来更新选项的内部存储。

```
_setOption: function( key, value ) {
  if ( key === "title" ) {
    this.element.find( "h3" ).text( value );
  }
  this._superApply( arguments );
} 
```

### _trigger( type [, event ] [, data ] )Returns: [Boolean](http://api.jquery.com/Types/#Boolean)

触发一个事件及其相关的回调。

带有该名称的选项与作为回调被调用的类型相等。

事件名称是小部件名称和类型的小写字母串。

*注意: 当提供数据时，您必须提供所有三个参数。如果没有传递事件，则传递 `null`。*

如果默认行为是阻止的，则返回 `false`，否则返回 `true`。当处理程序返回 `false` 时或调用 `event.preventDefault()` 时，则阻止默认行为发生。

*   **type**Type: [String](http://api.jquery.com/Types/#String)The `type` 应该匹配回调选项的名称。完整的事件类型会自动生成。
*   **event**Type: [Event](http://api.jquery.com/Types/#Event)导致该事件发生的原始事件，想听众提供上下文时很有用。
*   **data**Type: [Object](http://api.jquery.com/Types/#Object)一个与事件相关的数据哈希。

**Code examples:**

当按下一个键时，触发 `search` 事件。

```
this._on( this.element, {
  keydown: function( event ) {

    // Pass the original event so that the custom search event has
    // useful information, such as keyCode
    this._trigger( "search", event, {

      // Pass additional information unique to this event
      value: this.element.val()
    });
  }
}); 
```

### destroy()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

完全移除小部件功能。这会把元素返回到它的预初始化状态。

*   该方法不接受任何参数。

**Code examples:**

当点击小部件的任意锚点时销毁小部件。

```
this._on( this.element, {
  "click a": function( event ) {
    event.preventDefault();
    this.destroy();
  }
}); 
```

### disable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

禁用小部件。

*   该方法不接受任何参数。

**Code examples:**

当点击小部件的任意锚点时禁用小部件。

```
this._on( this.element, {
  "click a": function( event ) {
    event.preventDefault();
    this.disable();
  }
}); 
```

### enable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

启用小部件。

*   该方法不接受任何参数。

**Code examples:**

当点击小部件的任意锚点时启用小部件。

```
this._on( this.element, {
  "click a": function( event ) {
    event.preventDefault();
    this.enable();
  }
}); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取当前与指定的 `optionName` 关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取的选项的名称。

**Code examples:**

获得 `width` 选项的值。

```
this.option( "width" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含键/值对的对象，键/值对表示当前小部件选项哈希。

*   该方法不接受任何参数。

**Code examples:**

Log the key and value of each of the widget's options for debugging.

```
var options = this.option();
for ( var key in options ) {
  console.log( key, options[ key ] );
} 
```

### option( optionName, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置与指定的 `optionName` 关联的小部件选项的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的值。

**Code examples:**

设置 `width` 选项为 `500`。

```
this.option( "width", 500 ); 
```

### option( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

为小部件设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的 option-value 对。

**Code examples:**

设置 `height` 和 `width` 选项为 `500`。

```
this.option({
  width: 500,
  height: 500
}); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个包含原始元素或其他相关的生成元素的 `jQuery` 对象。

*   该方法不接受任何参数。

**Code examples:**

当创建小部件时，在小部件的原始元素周围放置一个红色的边框。

```
_create: function() {
  this.widget().css( "border", "2px solid red" );
} 
```

## Events

### create( event, ui )Type: `widgetcreate`

当小部件被创建时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*Note: `ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 create 回调的小部件：

```
$( ".selector" ).widget({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 widgetcreate 事件：

```
$( ".selector" ).on( "widgetcreate", function( event, ui ) {} ); 
```

# Widget Plugin Bridge

Categories: [Utilities](http://www.css88.com/jquery-ui-api/category/utilities/ "View all posts in Utilities") | [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## jQuery.widget.bridge( name, constructor )

**Description:** `jQuery.widget.bridge()` 方法是 jQuery 部件库（Widget Factory） 的一部分。它扮演着由 `$.widget()` 创建的对象和 jQuery API 之间的中介。

*   #### jQuery.widget.bridge( name, constructor )

    *   **name**Type: [String](http://api.jquery.com/Types/#String)要创建的插件名称。
    *   **constructor**Type: [Function](http://api.jquery.com/Types/#Function)()当插件被调用时要实例化的对象。

`$.widget.bridge()` 做如下事情：

*   连接一个常规的 JavaScript 构造函数到 jQuery API。
*   自动创建对象实例，并存储在元素的 `$.data` 缓存内。
*   允许调用公有方法。
*   防止调用私有方法。
*   防止在未初始化的对象上调用方法。
*   防止多个初始化。

jQuery UI 小部件使用 `$.widget( "foo.bar", {} );` 语法定义一个对象来创建。给出一个带有五个 `.foo`，`$( ".foo" ).bar();` 的 DOM 结构将创建 "bar" 对象的五个实例。`$.widget.bridge()` 基于 "bar" 对象和一个公共的 API 在库内工作。因此，您可以通过编写 `$( ".foo" ).bar()` 来创建实例，通过编写 `$( ".foo" ).bar( "baz" )` 来调用方法。

如果您只想一次性初始化并调用方法，那么您所传递给 `jQuery.widget.bridge()` 的对象可以很小：

```
var Highlighter = function( options, element ) {
  this.options = options;
  this.element = $( element );
  this._set( 800 );
};
Highlighter.prototype = {
  toggle: function() {
    this._set( this.element.css( "font-weight") === 400 ? 800 : 400 );
  },
  _set: function(value) {
    this.element.css( "font-weight", value );
  }
}; 
```

在这里，您需要的只是一个构造函数，接收两个参数：

*   `options`：一个配置选项的对象
*   `element`：该实例在其上创建的 DOM 元素

然后您可以使用桥（bridge）把该对象作为一个 jQuery 插件，且可以在任意的 jQuery 对象上使用它：

```
// Hook up the plugin
$.widget.bridge( "colorToggle", Highlighter );

// Initialize it on divs
$( "div" ).colorToggle().click(function() {
  // Call the public method on click
  $( this ).colorToggle( "toggle" );
}); 
```

为了使用桥（bridge）的所有特性，您的对象原型需要有一个 `_init()` 方法。该方法在调用插件且实例已存在时调用。在这种情况下，您还需要有一个 `option()` 方法。该方法将会以选项作为第一个参数被调用。如果没有选项，则参数为一个空对象。如需了解 `option` 方法的使用，请查看 `$.Widget`。

桥（bridge）有一个可选的属性，如果存在：如果对象原型有一个 `widgetFullName` 属性，则该属性将被作为存储和检索实例的键。否则，将使用 name 参数。