# Interactions

jQuery UI 提供了一套基于鼠标的交互。

## Draggable Widget

允许使用鼠标移动元素。

## Droppable Widget

为可拖拽小部件创建目标。

Also in: [Utilities](http://www.css88.com/jquery-ui-api/category/utilities/ "View all posts in Utilities")

## Mouse Interaction

基本交互层。

## Resizable Widget

使用鼠标改变元素的尺寸。

## Selectable Widget

使用鼠标选择单个元素或一组元素。

## Sortable Widget

使用鼠标调整列表中或者网格中元素的排序。

# Draggable Widget

Categories: [Interactions](http://www.css88.com/jquery-ui-api/category/interactions/ "View all posts in Interactions")

## version added: 1.0

**Description:** 该组件可以让你使用鼠标拖动所有元素。

## QuickNavExamples

### Options

*   addClasses
*   appendTo
*   axis
*   cancel
*   connectToSortable
*   containment
*   cursor
*   cursorAt
*   delay
*   disabled
*   distance
*   grid
*   handle
*   helper
*   iframeFix
*   opacity
*   refreshPositions
*   revert
*   revertDuration
*   scope
*   scroll
*   scrollSensitivity
*   scrollSpeed
*   snap
*   snapMode
*   snapTolerance
*   stack
*   zIndex

### Methods

*   destroy
*   disable
*   enable
*   option
*   widget

### Events

*   create
*   drag
*   start
*   stop

让被选择元素可以被鼠标拖动。如果你想把元素拖放到另一个元素内部，查看 jQuery UI Droppable plugin,该组件为被拖动元素提供了一个目标容器。

### Dependencies（依赖性）

*   UI Core
*   Widget Factory
*   Mouse Interaction

## Options

### addClasses**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `true`如果值设置为`false`, `ui-draggable`样式类将不能被添加引用。当在大量元素上调用`.draggable()`时，你可能会想要这样设置，作为一个性能优化。**Code examples:**

使用`addClasses`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ addClasses: false }); 
```

在组件初始化之后，读取或设置`addClasses`选项

```
// getter
var addClasses = $( ".selector" ).draggable( "option", "addClasses" );

// setter
$( ".selector" ).draggable( "option", "addClasses", false ); 
```

### appendTo**Type:** [jQuery](http://api.jquery.com/Types/#jQuery) or [Element](http://api.jquery.com/Types/#Element) or [Selector](http://api.jquery.com/Types/#Selector) or [String](http://api.jquery.com/Types/#String)

**Default:** `"parent"`当进行拖动时，拖动组件助手应该被添加到的元素。**支持多种类型:**

*   **jQuery**: 一个含有要被添加拖动组件助手的元素的 Jquery 对象。
*   **Element**: 要被添加拖动组件助手的元素。
*   **Selector**: 一个用来识别要被添加拖动组件助手的元素的选择器。
*   **String**: 字符串`"parent"`将会使拖动组件助手成为组件的同级元素。

**Code examples:**

使用`appendTo`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ appendTo: "body" }); 
```

在组件初始化之后，读取或设置`appendTo`选项

```
// getter
var appendTo = $( ".selector" ).draggable( "option", "appendTo" );

// setter
$( ".selector" ).draggable( "option", "appendTo", "body" ); 
```

### axis**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `false`约束拖动的动作只能在水平(x 轴)或垂直(y 轴)上执行。可选值: `"x"`, `"y"`。**Code examples:**

使用`axis`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ axis: "x" }); 
```

在组件初始化之后，读取或设置`axis`选项：

```
// getter
var axis = $( ".selector" ).draggable( "option", "axis" );

// setter
$( ".selector" ).draggable( "option", "axis", "x" ); 
```

### cancel**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `"input,textarea,button,select,option"`防止在指定元素上开始拖动。**Code examples:**

使用`cancel`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ cancel: ".title" }); 
```

在组件初始化之后，读取或设置`cancel`选项：

```
// getter
var cancel = $( ".selector" ).draggable( "option", "cancel" );

// setter
$( ".selector" ).draggable( "option", "cancel", ".title" ); 
```

### connectToSortable**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `false`允许 draggable 被拖拽到指定的 sortables 中。如果使用了该选项，被拖动的元素可以被放置于一个应用了排序组件的元素列表中并成为该列表的一部分。注意: 为了完美的使用该特性，`helper`选项必须被设置为`"clone"`。 必须包含 jQuery UI 排序组件。**Code examples:**

使用`connectToSortable`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ connectToSortable: "#my-sortable" }); 
```

在组件初始化之后，读取或设置`connectToSortable`选项：

```
// getter
var connectToSortable = $( ".selector" ).draggable( "option", "connectToSortable" );

// setter
$( ".selector" ).draggable( "option", "connectToSortable", "#my-sortable" ); 
```

### containment**Type:** [Selector](http://api.jquery.com/Types/#Selector) or [Element](http://api.jquery.com/Types/#Element) or [String](http://api.jquery.com/Types/#String) or [Array](http://api.jquery.com/Types/#Array)

**Default:** `false`可以限制 draggable 只能在指定的元素或区域的边界以内进行拖动。**支持多种类型:**

*   **Selector**: 可拖动元素将被置于由选择器指定的第一个元素的起界限作用的盒模型中。如果没有找到任何元素，则不会设置界限。
*   **Element**: 可拖动的元素将包含该元素的边界框。
*   **String**:可选值: `"parent"`, `"document"`, `"window"`.
*   **Array**: 以 `[ x1, y1, x2, y2 ]` 数组形式定义一个限制区域.

**Code examples:**

使用`containment`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ containment: "parent" }); 
```

在组件初始化之后，读取或设置`containment`选项：

```
// getter
var containment = $( ".selector" ).draggable( "option", "containment" );

// setter
$( ".selector" ).draggable( "option", "containment", "parent" ); 
```

### cursor**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"auto"`指定在做拖拽动作时，鼠标的 CSS 样式。**Code examples:**

使用`cursor`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ cursor: "crosshair" }); 
```

在组件初始化之后，读取或设置`cursor`选项：

```
// getter
var cursor = $( ".selector" ).draggable( "option", "cursor" );

// setter
$( ".selector" ).draggable( "option", "cursor", "crosshair" ); 
```

### cursorAt**Type:** [Object](http://api.jquery.com/Types/#Object)

**Default:** `false`设置拖动帮手相对于鼠标光标的偏移量。坐标可被指定为一个散列 使用的组合中的一个或两个键：`{ top, left, right, bottom }` 。**Code examples:**

使用`cursorAt`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ cursorAt: { left: 5 } }); 
```

在组件初始化之后，读取或设置`cursorAt`选项：

```
// getter
var cursorAt = $( ".selector" ).draggable( "option", "cursorAt" );

// setter
$( ".selector" ).draggable( "option", "cursorAt", { left: 5 } ); 
```

### delay**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `0`当鼠标按下后，指定时延迟间后才开始激活拖拽动作（单位：毫秒）。此选项可用来阻止当点击一个元素时可能发生的非期望拖动行为。**Code examples:**

使用`delay`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ delay: 300 }); 
```

在组件初始化之后，读取或设置`delay`选项：

```
// getter
var delay = $( ".selector" ).draggable( "option", "delay" );

// setter
$( ".selector" ).draggable( "option", "delay", 300 ); 
```

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果该值设置为`true`，拖动特效将被禁用。**Code examples:**

使用`disabled`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ disabled: true }); 
```

在组件初始化之后，读取或设置`disabled`选项：

```
// getter
var disabled = $( ".selector" ).draggable( "option", "disabled" );

// setter
$( ".selector" ).draggable( "option", "disabled", true ); 
```

### distance**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `1`当鼠标点下后，只有移动指定像素后才开始激活拖拽动作，单位为像素。此选项可用来阻止当点击一个元素时可能发生的非期望拖动行为。**Code examples:**

使用`distance`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ distance: 10 }); 
```

在组件初始化之后，读取或设置`distance`选项：

```
// getter
var distance = $( ".selector" ).draggable( "option", "distance" );

// setter
$( ".selector" ).draggable( "option", "distance", 10 ); 
```

### grid**Type:** [Array](http://api.jquery.com/Types/#Array)

**Default:** `false`拖拽元素时，只能以指定大小的方格进行拖动。数组形式为`[ x, y ]`。**Code examples:**

使用`grid`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ grid: [ 50, 20 ] }); 
```

在组件初始化之后，读取或设置`grid` 选项:

```
// getter
var grid = $( ".selector" ).draggable( "option", "grid" );

// setter
$( ".selector" ).draggable( "option", "grid", [ 50, 20 ] ); 
```

### handle**Type:** [Selector](http://api.jquery.com/Types/#Selector) or [Element](http://api.jquery.com/Types/#Element)

**Default:** `false`当参数值为 true 时,只有在特定的元素上触发鼠标按下事件时，才可以拖动。 只有被拖到元素的子元素才可以应用该参数。**Code examples:**

使用`handle`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ handle: "h2" }); 
```

在组件初始化之后，读取或设置`handle` 选项:

```
// getter
var handle = $( ".selector" ).draggable( "option", "handle" );

// setter
$( ".selector" ).draggable( "option", "handle", "h2" ); 
```

### helper**Type:** [String](http://api.jquery.com/Types/#String) or [Function](http://api.jquery.com/Types/#Function)()

**Default:** `"original"`允许一个元素被用来进行拖动。**支持多种类型:**

*   **String**:如果值设置为`"clone"`, 那么该元素将会被复制，并且被复制的元素将被拖动。
*   **Function**: 当拖动时，函数将返回一个 DOM 元素以供使用。

**Code examples:**

使用`helper`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ helper: "clone" }); 
```

在组件初始化之后，读取或设置`helper` 选项:

```
// getter
var helper = $( ".selector" ).draggable( "option", "helper" );

// setter
$( ".selector" ).draggable( "option", "helper", "clone" ); 
```

### iframeFix**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `false`在拖动期间阻止 iframe 捕捉鼠标移过事件。与`cursorAt`选项搭配使用时或者当鼠标指针可能不在拖动助手元素之上时，该参数非常有用。**支持多种类型:**

*   **Boolean**: 当设置为`true`, 透明层将被放置于页面上的所有 iframe 之上。/li>
*   **Selector**: 任何由选择器匹配的 iframe 将被透明层覆盖。

**Code examples:**

使用`iframeFix`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ iframeFix: true }); 
```

在组件初始化之后，读取或设置`iframeFix` 选项:

```
// getter
var iframeFix = $( ".selector" ).draggable( "option", "iframeFix" );

// setter
$( ".selector" ).draggable( "option", "iframeFix", true ); 
```

### opacity**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `false`当拖动时，拖动助手元素的不透明度。**Code examples:**

使用`opacity`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ opacity: 0.35 }); 
```

在组件初始化之后，读取或设置`opacity` 选项:

```
// getter
var opacity = $( ".selector" ).draggable( "option", "opacity" );

// setter
$( ".selector" ).draggable( "option", "opacity", 0.35 ); 
```

### refreshPositions**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为`true`， 所有的可拖动位置在每次鼠标移动时都会被计算。 *注意: 这解决了具有高度动态内容页面的问题，但是却降低了性能。***Code examples:**

使用`refreshPositions`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ refreshPositions: true }); 
```

在组件初始化之后，读取或设置`refreshPositions` 选项:

```
// getter
var refreshPositions = $( ".selector" ).draggable( "option", "refreshPositions" );

// setter
$( ".selector" ).draggable( "option", "refreshPositions", true ); 
```

### revert**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [String](http://api.jquery.com/Types/#String)

**Default:** `false`当拖动停止时，元素是否要被重置到它的初始位置。**支持多种类型:**

*   **Boolean**: 如果设置为`true`，当拖动停止时，元素位置将被重置。
*   **String**: 如果设置为`"invalid"`, 重置仅当拖动没有被放置于一个可放置的对象时才会发生。如果设置为`"valid"`, 情况则相反。

**Code examples:**

使用`revert`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ revert: true }); 
```

在组件初始化之后，读取或设置`revert` 选项:

```
// getter
var revert = $( ".selector" ).draggable( "option", "revert" );

// setter
$( ".selector" ).draggable( "option", "revert", true ); 
```

### revertDuration**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `500`动画重置时间, 单位为微秒。如果`revert`选项设置为`false`，则忽略（译者注：即被拖到元素不会被重置。）。**Code examples:**

使用`revertDuration`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ revertDuration: 200 }); 
```

在组件初始化之后，读取或设置`revertDuration` 选项:

```
// getter
var revertDuration = $( ".selector" ).draggable( "option", "revertDuration" );

// setter
$( ".selector" ).draggable( "option", "revertDuration", 200 ); 
```

### scope**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"default"`被用来将拖动组件和拖动至容器组件的参数进行分组, 除了拖动至容器组件的`accept`选项。如果一个一般拖动组件的`scope`参数值和一个拖动至容器组件的`scope`参数值一样，那么这个一般拖动组件将被接受为拖动至容器组件。**Code examples:**

使用`scope`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ scope: "tasks" }); 
```

在组件初始化之后，读取或设置`scope` 选项:

```
// getter
var scope = $( ".selector" ).draggable( "option", "scope" );

// setter
$( ".selector" ).draggable( "option", "scope", "tasks" ); 
```

### scroll**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `true`如果设置为`true`, 当拖动时，div 盒模型将自动翻滚。**Code examples:**

使用`scroll`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ scroll: false }); 
```

在组件初始化之后，读取或设置`scroll` 选项:

```
// getter
var scroll = $( ".selector" ).draggable( "option", "scroll" );

// setter
$( ".selector" ).draggable( "option", "scroll", false ); 
```

### scrollSensitivity**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `20`离开可视区域边缘多少距离开始滚动。距离是相对指针进行计算的，而不是被拖到元素本身。如果`scroll` 选项设置为`false`，则不滚动。**Code examples:**

使用`scrollSensitivity`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ scrollSensitivity: 100 }); 
```

在组件初始化之后，读取或设置`scrollSensitivity` 选项:

```
// getter
var scrollSensitivity = $( ".selector" ).draggable( "option", "scrollSensitivity" );

// setter
$( ".selector" ).draggable( "option", "scrollSensitivity", 100 ); 
```

### scrollSpeed**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `20`当鼠标指针的值小于`scrollSensitivity`的值时，窗口滚动的速度。如果`scroll`选项设置为`false`，则该参数无效。**Code examples:**

使用`scrollSpeed`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ scrollSpeed: 100 }); 
```

在组件初始化之后，读取或设置`scrollSpeed` 选项:

```
// getter
var scrollSpeed = $( ".selector" ).draggable( "option", "scrollSpeed" );

// setter
$( ".selector" ).draggable( "option", "scrollSpeed", 100 ); 
```

### snap**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `false`决定一个元素是否应该吸附到其它元素上。**支持多种类型:**

*   **Boolean**: 当设置为 `true`时, 元素将可以吸附到所有其它可拖动元素上。
*   **Selector**: 确定被吸附元素。

**Code examples:**

使用`snap`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ snap: true }); 
```

在组件初始化之后，读取或设置`snap` 选项:

```
// getter
var snap = $( ".selector" ).draggable( "option", "snap" );

// setter
$( ".selector" ).draggable( "option", "snap", true ); 
```

### snapMode**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"both"`决定可拖动元素将要吸附到哪个元素的边缘。如果`snap`选项设置为`false`，则忽略该参数。 可选值: `"inner"`, `"outer"`, `"both"`.**Code examples:**

使用`snapMode`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ snapMode: "inner" }); 
```

在组件初始化之后，读取或设置`snapMode` 选项:

```
// getter
var snapMode = $( ".selector" ).draggable( "option", "snapMode" );

// setter
$( ".selector" ).draggable( "option", "snapMode", "inner" ); 
```

### snapTolerance**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `20`当距离可吸附元素多远时，触发吸附事件。如果`snap`选项设置为`false`，则忽略该参数。**Code examples:**

使用`snapTolerance`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ snapTolerance: 30 }); 
```

在组件初始化之后，读取或设置`snapTolerance` 选项:

```
// getter
var snapTolerance = $( ".selector" ).draggable( "option", "snapTolerance" );

// setter
$( ".selector" ).draggable( "option", "snapTolerance", 30 ); 
```

### stack**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `false`控制由选择器所触发的一系列元素的 z-index 值, 总是将当前被拖动对象至于最前。对于像窗口管理这样的应用来说，非常有用。**Code examples:**

使用`stack`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ stack: ".products" }); 
```

在组件初始化之后，读取或设置`stack` 选项:

```
// getter
var stack = $( ".selector" ).draggable( "option", "stack" );

// setter
$( ".selector" ).draggable( "option", "stack", ".products" ); 
```

### zIndex**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `false`当被拖动时，拖动助手的 Z-index 值。**Code examples:**

使用`zIndex`选项初始化 Draggable Widget：

```
$( ".selector" ).draggable({ zIndex: 100 }); 
```

在组件初始化之后，读取或设置`zIndex` 选项:

```
// getter
var zIndex = $( ".selector" ).draggable( "option", "zIndex" );

// setter
$( ".selector" ).draggable( "option", "zIndex", 100 ); 
```

## Methods

### destroy()

完全销毁一般拖动组件的功能，这将使元素返回它的初始状态。

*   这个方法不接受任何参数。

**Code examples:**

请求 destroy 方法:

```
$( ".selector" ).draggable( "destroy" ); 
```

### disable()

禁用一般拖动组件。

*   这个方法不接受任何参数。

**Code examples:**

请求 disable 方法:

```
$( ".selector" ).draggable( "disable" ); 
```

### enable()

启用一般拖动组件。

*   这个方法不接受任何参数。

**Code examples:**

请求 enable 方法:

```
$( ".selector" ).draggable( "enable" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取与`optionName`对应的参数值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取的值所对应的选项的名称。

**Code examples:**

请求方法:

```
var isDisabled = $( ".selector" ).draggable( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含有描述当前一般拖动组件选项哈希值的键/值对。

*   这个方法不接受任何参数。

**Code examples:**

请求方法:

```
var options = $( ".selector" ).draggable( "option" ); 
```

### option( optionName, value )

设置一般拖动组件选项的值，选项名称由`optionName`指定。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的参数值。

**Code examples:**

请求方法:

```
$( ".selector" ).draggable( "option", "disabled", true ); 
```

### option( options )

为一般拖动组件设置一个或多个选项值。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的选项与值之间的映射关系。

**Code examples:**

请求方法:

```
$( ".selector" ).draggable( "option", { disabled: true } ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个包含有可拖动元素的`jQuery`对象。

*   这个方法不接受任何参数。

**Code examples:**

请求 widget 方法:

```
var widget = $( ".selector" ).draggable( "widget" ); 
```

## Events

### create( event, ui )Type: `dragcreate`

当一般拖动组件被创建时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意: `ui`对象是空的，但是为了与其它元素保持一直，它总是被包含。*

**Code examples:**

使用 create 回调函数指定事件:

```
$( ".selector" ).draggable({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 dragcreate 事件:

```
$( ".selector" ).on( "dragcreate", function( event, ui ) {} ); 
```

### drag( event, ui )Type: `drag`

当鼠标在拖动过程中移动时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)代表被拖动的元素。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)当前元素的 CSS 位置，以`{ top, left }`形式给出。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)当前元素的偏移位置，以`{ top, left }`形式给出。

**Code examples:**

使用 drag 回调函数指定事件:

```
$( ".selector" ).draggable({
  drag: function( event, ui ) {}
}); 
```

绑定一个事件监听者到 drag 事件:

```
$( ".selector" ).on( "drag", function( event, ui ) {} ); 
```

### start( event, ui )Type: `dragstart`

当拖动开始时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)代表被拖动的元素。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)当前元素的 CSS 位置，以`{ top, left }`形式给出。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)当前元素的偏移位置，以`{ top, left }`形式给出。

**Code examples:**

使用 start callback specified:

```
$( ".selector" ).draggable({
  start: function( event, ui ) {}
}); 
```

拖动事件绑定一个事件监听器：

```
$( ".selector" ).on( "dragstart", function( event, ui ) {} ); 
```

### stop( event, ui )Type: `dragstop`

当拖动停止时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)代表被拖动的元素。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)当前元素的 CSS 位置，以`{ top, left }`形式给出。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)当前元素的偏移位置，以`{ top, left }`形式给出。

**Code examples:**

使用 start 回调函数指定事件:

```
$( ".selector" ).draggable({
  stop: function( event, ui ) {}
}); 
```

绑定一个事件监听者到 dragstart 事件:

```
$( ".selector" ).on( "dragstop", function( event, ui ) {} ); 
```

## Example:

#### 一个简单的 jQuery UI 一般拖动

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>draggable demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #draggable {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<div id="draggable">Drag me</div>

<script>
$( "#draggable" ).draggable();
</script>

</body>
</html> 
```

# Droppable Widget

Categories: [Interactions](http://www.css88.com/jquery-ui-api/category/interactions/ "View all posts in Interactions")

## version added: 1.0

**Description:** 创建拖动元素的目标。

## QuickNavExamples

### Options

*   accept
*   activeClass
*   addClasses
*   disabled
*   greedy
*   hoverClass
*   scope
*   tolerance

### Methods

*   destroy
*   disable
*   enable
*   option
*   widget

### Events

*   activate
*   create
*   deactivate
*   drop
*   out
*   over

jQuery UI 拖放插件可以使所选元素可拖放（这意味着 draggables 拖动可以被拖放接受）。您可以指定哪个拖动被接受。

### Dependencies（依赖性）

*   UI Core
*   Widget Factory
*   Mouse Interaction

## Options

### accept**Type:** [Selector](http://api.jquery.com/Types/#Selector) or [Function](http://api.jquery.com/Types/#Function)()

**Default:** `"*"`控制可拖动的元素被拖放接受。**支持多种类型：**

*   **Selector**: 一个选择器可拖动的元素。
*   **Function**: 函数将被调用页面上的每一个可拖动的（传递给函数的第一个参数）。该函数必须返回`true`，如果可拖动应该接受。

**Code examples:**

使用指定的`accept`参数初始化一个 droppable：

```
$( ".selector" ).droppable({ accept: ".special" }); 
```

在初始化后设置或者获取`accept`参数：

```
// getter
var accept = $( ".selector" ).droppable( "option", "accept" );

// setter
$( ".selector" ).droppable( "option", "accept", ".special" ); 
```

### activeClass**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `false`如果指定了该参数,在被允许的 draggable 对象填充时,droppable 会被添加上指定的样式。**Code examples:**

使用指定的`activeClass` 参数初始化一个 droppable：

```
$( ".selector" ).droppable({ activeClass: "ui-state-highlight" }); 
```

在初始化后设置或者获取`activeClass`参数：

```
// getter
var activeClass = $( ".selector" ).droppable( "option", "activeClass" );

// setter
$( ".selector" ).droppable( "option", "activeClass", "ui-state-highlight" ); 
```

### addClasses**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `true`如果设置为`false`, 可以防止`ui-droppable`类在进行时添加. 这可能会使在初始化数百个元素执行`.droppable()`时使性能得到理想的优化.**Code examples:**

使用指定的`addClasses` 参数初始化一个 droppable：

```
$( ".selector" ).droppable({ addClasses: false }); 
```

在初始化后设置或者获取`addClasses`参数：

```
// getter
var addClasses = $( ".selector" ).droppable( "option", "addClasses" );

// setter
$( ".selector" ).droppable( "option", "addClasses", false ); 
```

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为 `true`将禁止拖放。**Code examples:**

使用指定的`disabled` 参数初始化一个 droppable：

```
$( ".selector" ).droppable({ disabled: true }); 
```

在初始化后设置或者获取`disabled`参数：

```
// getter
var disabled = $( ".selector" ).droppable( "option", "disabled" );

// setter
$( ".selector" ).droppable( "option", "disabled", true ); 
```

### greedy**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`默认情况下，当一个元素被放到嵌套的放置（droppable）对象时，每个放置（droppable）对象都将接收到这个元素。然而，当设置这个选项为`true`时，任何父级的放置（droppable）对象不会接收元素。`drop`事件将依然会正常的泡沫，但`event.target`查看哪个放置（droppable）对象接受了拖动元素。**Code examples:**

使用指定的`greedy` 参数初始化一个 droppable：

```
$( ".selector" ).droppable({ greedy: true }); 
```

在初始化后设置或者获取`greedy`参数：

```
// getter
var greedy = $( ".selector" ).droppable( "option", "greedy" );

// setter
$( ".selector" ).droppable( "option", "greedy", true ); 
```

### hoverClass**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `false`如果设置了该参数,将在一个被允许的拖动元素悬停在放置（droppable）对象上时，向放置（droppable）对象添加一个指定的样式.**Code examples:**

使用指定的`hoverClass` 参数初始化一个 droppable：

```
$( ".selector" ).droppable({ hoverClass: "drop-hover" }); 
```

在初始化后设置或者获取`hoverClass`参数：

```
// getter
var hoverClass = $( ".selector" ).droppable( "option", "hoverClass" );

// setter
$( ".selector" ).droppable( "option", "hoverClass", "drop-hover" ); 
```

### scope**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"default"`用来设置拖动（draggle）元素和放置（droppable）对象的集合, 除了 droppable 中的`accept`属性指定的元素外,和放置（droppable）对象相同集合的放置（droppable）对象也被允许添加到放置（droppable）对象中.**Code examples:**

使用指定的`scope` 参数初始化一个 droppable：

```
$( ".selector" ).droppable({ scope: "tasks" }); 
```

在初始化后设置或者获取`scope`参数：

```
// getter
var scope = $( ".selector" ).droppable( "option", "scope" );

// setter
$( ".selector" ).droppable( "option", "scope", "tasks" ); 
```

### tolerance**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"intersect"`指定使用那种模式来测试一个拖动(draggable)元素"经过"一个放置（droppable）对象。 允许使用的值:

*   `"fit"`: 拖动(draggable)元素 完全重叠到放置（droppable）对象。
*   `"intersect"`: 拖动(draggable)元素 和放置（droppable）对象至少重叠 50%。
*   `"pointer"`: 鼠标重叠到放置（droppable）对象上。
*   `"touch"`: 拖动(draggable)元素 和放置（droppable）对象的任意重叠

**Code examples:**

使用指定的`tolerance` 参数初始化一个 droppable：

```
$( ".selector" ).droppable({ tolerance: "fit" }); 
```

在初始化后设置或者获取`tolerance`参数：

```
// getter
var tolerance = $( ".selector" ).droppable( "option", "tolerance" );

// setter
$( ".selector" ).droppable( "option", "tolerance", "fit" ); 
```

## Methods（方法）

### destroy()

完全移除拖放功能. 这将使元素返回到之前的初始化状态.

*   这个方法不接受任何参数

**Code examples:**

调用 destroy 方法

```
$( ".selector" ).droppable( "destroy" ); 
```

### disable()

禁用拖放。

*   这个方法不接受任何参数

**Code examples:**

调用 disable 方法

```
$( ".selector" ).droppable( "disable" ); 
```

### enable()

启用拖放。

*   这个方法不接受任何参数

**Code examples:**

调用 enable 方法

```
$( ".selector" ).droppable( "enable" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

通过指定的`optionName`获取当前关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项名

**Code examples:**

调用这个方法：

```
var isDisabled = $( ".selector" ).droppable( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个对象，它包含表示当前 droppable 的选项 hash 的键/值对。

*   这个方法不接受任何参数

**Code examples:**

调用这个方法：

```
var options = $( ".selector" ).droppable( "option" ); 
```

### option( optionName, value )

通过指定的`optionName`，设置 droppable 的相关选项值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置值的选项名。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要设置选项的值。

**Code examples:**

调用这个方法：

```
$( ".selector" ).droppable( "option", "disabled", true ); 
```

### option( options )

为 droppable 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)设置的选项/值对的对象。

**Code examples:**

调用这个方法：

```
$( ".selector" ).droppable( "option", { disabled: true } ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个`jQuery` ，它包含了 droppable 元素。

*   这个方法不接受任何参数

**Code examples:**

调用 widget 方法

```
var widget = $( ".selector" ).droppable( "widget" ); 
```

## Events

### activate( event, ui )Type: `dropactivate`

这个事件会在任何允许的 draggable 对象开始拖动时触发。它可以用来在你想让 droppable 对象在可以被填充的时"亮起来"的时候。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **draggable**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表的拖动元素。
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被拖动元素的助手。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)当前可拖动助手的 CSS 的 position（位置）对象，如`{ top, left }`。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)当前可拖动助手的偏移位置对象，如`{ top, left }`。

**Code examples:**

使用指定的 activate 回调初始化一个 droppable：

```
$( ".selector" ).droppable({
 activate: function( event, ui ) {}
}); 
```

绑定一个事件监听到 dropactivate 事件:

```
$( ".selector" ).on( "dropactivate", function( event, ui ) {} ); 
```

### create( event, ui )Type: `dropcreate`

此事件会在 droppable 创建时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui`对象是空对象，包括是为了和其他事件的一致性。*

**Code examples:**

使用指定的 create 回调初始化一个 droppable：

```
$( ".selector" ).droppable({
 create: function( event, ui ) {}
}); 
```

绑定一个事件监听到 dropcreate 事件：

```
$( ".selector" ).on( "dropcreate", function( event, ui ) {} ); 
```

### deactivate( event, ui )Type: `dropdeactivate`

此事件会在任何允许的 draggable 对象停止拖动时触发.

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **draggable**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表的拖动元素。
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被拖动元素的助手。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)当前可拖动助手的 CSS 的 position（位置）对象，如`{ top, left }`。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)当前可拖动助手的偏移位置对象，如`{ top, left }`。

**Code examples:**

使用指定的 deactivate 回调初始化一个 droppable：

```
$( ".selector" ).droppable({
 deactivate: function( event, ui ) {}
}); 
```

绑定一个事件监听到 dropdeactivate 事件：

```
$( ".selector" ).on( "dropdeactivate", function( event, ui ) {} ); 
```

### drop( event, ui )Type: `drop`

这个事件会在一个允许的拖动（draggable）元素填充进这个放置（droppable）对象时触发.（基于`tolerance`选项）。（愚人码头注释： 回调函数中, $(this) 表示被填充的 droppable 对象. ui.draggable 表示 draggable 对象.）

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **draggable**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表的拖动元素。
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被拖动元素的助手。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)当前可拖动助手的 CSS 的 position（位置）对象，如`{ top, left }`。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)当前可拖动助手的偏移位置对象，如`{ top, left }`。

**Code examples:**

使用指定的 drop 回调初始化一个 droppable：

```
$( ".selector" ).droppable({
 drop: function( event, ui ) {}
}); 
```

绑定一个事件监听到 drop 事件：

```
$( ".selector" ).on( "drop", function( event, ui ) {} ); 
```

### out( event, ui )Type: `dropout`

此事件会在一个允许的拖动（draggable）元素离开这个放置（droppable）对象时触发（基于`tolerance`选项）。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui`对象是空对象，包括是为了和其他事件的一致性。*

**Code examples:**

使用指定的 out 回调初始化一个 droppable：

```
$( ".selector" ).droppable({
 out: function( event, ui ) {}
}); 
```

绑定一个事件监听到 dropout 事件：

```
$( ".selector" ).on( "dropout", function( event, ui ) {} ); 
```

### over( event, ui )Type: `dropover`

此事件会在一个允许的拖动（draggable）元素经过这个放置（droppable）对象时触发（基于`tolerance`选项）。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **draggable**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表的拖动元素。
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被拖动元素的助手。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)当前可拖动助手的 CSS 的 position（位置）对象，如`{ top, left }`。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)当前可拖动助手的偏移位置对象，如`{ top, left }`。

**Code examples:**

使用指定的 over 回调初始化一个 droppable：

```
$( ".selector" ).droppable({
 over: function( event, ui ) {}
}); 
```

绑定一个事件监听到 dropover 事件：

```
$( ".selector" ).on( "dropover", function( event, ui ) {} ); 
```

## Example:

#### A pair of draggable and droppable elements.

```
<!doctype html>
<html lang="en">
<head>
 <meta charset="utf-8">
 <title>droppable demo</title>
 <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
 <style>
 #draggable {
 width: 100px;
 height: 100px;
 background: #ccc;
 }
 #droppable {
 position: absolute;
 left: 250px;
 top: 0;
 width: 125px;
 height: 125px;
 background: #999;
 color: #fff;
 padding: 10px;
 }
 </style>
 <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
 <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<div id="droppable">Drop here</div>
<div id="draggable">Drag me</div>

<script>
$( "#draggable" ).draggable();
$( "#droppable" ).droppable({
 drop: function() {
 alert( "dropped" );
 }
});
</script>

</body>
</html> 
```

# Mouse Interaction

Categories: [Interactions](http://www.css88.com/jquery-ui-api/category/interactions/ "View all posts in Interactions") | [Utilities](http://www.css88.com/jquery-ui-api/category/utilities/ "View all posts in Utilities")

**Description:** 底层的交互组件

## QuickNav

### Options

*   cancel
*   delay
*   distance

### Methods

*   _mouseCapture
*   _mouseDelayMet
*   _mouseDestroy
*   _mouseDistanceMet
*   _mouseDown
*   _mouseDrag
*   _mouseInit
*   _mouseMove
*   _mouseStart
*   _mouseStop
*   _mouseUp

### Events

像 `jQuery.Widget`, Mouse Interaction（鼠标交互）的目的不是直接使用。这纯粹是一个让其他部件（widget）继承基础组件。这个页面只文档被添加到`jQuery.Widget`，但它包括不打算被重写的内部方法。对外公开的 API 是`_mouseStart()`, `_mouseDrag()`, `_mouseStop()`, 和 `_mouseCapture()`.

### Dependencies

*   Widget Factory

## Options

### cancel**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `"input,textarea,button,select,option"`防止在指定的元素上相互作用。**Code examples:**

使用指定的 `cancel` 参数初始化一个:

```
$( ".selector" ).mouse({ cancel: ".title" }); 
```

在初始化后设置或者获取`cancel` 参数：

```
// getter
var cancel = $( ".selector" ).mouse( "option", "cancel" );

// setter
$( ".selector" ).mouse( "option", "cancel", ".title" ); 
```

### delay**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `0`时间（以毫秒为单位），当鼠标按下后直到的互动（interactions）激活。此选项可用来阻止当点击一个元素时可能发生的非期望互动（interactions）行为。**Code examples:**

使用指定的 `delay` 参数初始化一个:

```
$( ".selector" ).mouse({ delay: 300 }); 
```

在初始化后设置或者获取`delay` 参数：

```
// getter
var delay = $( ".selector" ).mouse( "option", "delay" );

// setter
$( ".selector" ).mouse( "option", "delay", 300 ); 
```

### distance**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `1`当鼠标点下后，只有移动指定像素后才开始激活互动（interactions）动作，单位为像素。此选项可用来阻止当点击一个元素时可能发生的非期望拖动行为。**Code examples:**

使用指定的 `distance` 参数初始化一个:

```
$( ".selector" ).mouse({ distance: 10 }); 
```

在初始化后设置或者获取`distance` 参数：

```
// getter
var distance = $( ".selector" ).mouse( "option", "distance" );

// setter
$( ".selector" ).mouse( "option", "distance", 10 ); 
```

## Methods

### _mouseCapture()Returns: [Boolean](http://api.jquery.com/Types/#Boolean)

确定一个互动（interaction）是否基于事件目标元素。默认总是返回 `true`。

*   这个方法不接受任何参数。

**Code examples:**

调用 _mouseCapture 方法:

```
$( ".selector" ).mouse( "_mouseCapture" ); 
```

### _mouseDelayMet()Returns: [Boolean](http://api.jquery.com/Types/#Boolean)

确定`delay`选项是否满足当前的互动（interaction）。

*   这个方法不接受任何参数。

**Code examples:**

调用 _mouseDelayMet 方法:

```
$( ".selector" ).mouse( "_mouseDelayMet" ); 
```

### _mouseDestroy()

破坏互动（interaction）的事件处理程序。这个必须调用从 widget 的`_destroy()`方法。 Destroys the interaction event handlers. This must be called from the extending widget's `_destroy()` method.

*   这个方法不接受任何参数。

**Code examples:**

调用 _mouseDestroy 方法:

```
$( ".selector" ).mouse( "_mouseDestroy" ); 
```

### _mouseDistanceMet()Returns: [Boolean](http://api.jquery.com/Types/#Boolean)

确认`distance`选项是否已满足当前的互动（interaction）

*   这个方法不接受任何参数。

**Code examples:**

调用 _mouseDistanceMet 方法:

```
$( ".selector" ).mouse( "_mouseDistanceMet" ); 
```

### _mouseDown()

互动（interaction）开始处理。验证该事件原先相关的鼠标按钮键 并确保`delay`和`distance`选项符合之前激活的互动（interaction）。当互动（interaction）准备开始时，调用 `_mouseStart()` 方法来处理扩展部件。

*   这个方法不接受任何参数。

**Code examples:**

调用 _mouseDown 方法:

```
$( ".selector" ).mouse( "_mouseDown" ); 
```

### _mouseDrag()

扩展部件需要执行一个 `_mouseDrag()`方法来处理互动（interaction）的每次移动。此方法将接收鼠标移动相关事件。

*   这个方法不接受任何参数。

**Code examples:**

调用 _mouseDrag 方法:

```
$( ".selector" ).mouse( "_mouseDrag" ); 
```

### _mouseInit()

初始化的互动（interaction）事件处理程序。这必须调用扩展部件的`_create()` 方法。

*   这个方法不接受任何参数。

**Code examples:**

调用 _mouseInit 方法:

```
$( ".selector" ).mouse( "_mouseInit" ); 
```

### _mouseMove()

处理互动（interaction）的每次移动。为扩展部件处理器调用`mouseDrag()`方法。

*   这个方法不接受任何参数。

**Code examples:**

调用 _mouseMove 方法:

```
$( ".selector" ).mouse( "_mouseMove" ); 
```

### _mouseStart()

扩展部件需要执行一个 `_mouseStart()`方法来处理互动（interaction）的开始激活。此方法将接收互动（interaction）开始激活的相关鼠标事件。

*   这个方法不接受任何参数。

**Code examples:**

调用 _mouseStart 方法:

```
$( ".selector" ).mouse( "_mouseStart" ); 
```

### _mouseStop()

扩展部件需要执行一个 `_mouseStop()`方法来处理互动（interaction）的结束。此方法将接收互动（interaction）结束的相关鼠标事件。

*   这个方法不接受任何参数。

**Code examples:**

调用 _mouseStop 方法:

```
$( ".selector" ).mouse( "_mouseStop" ); 
```

### _mouseUp()

互动（interaction）结束的处理程序。调用 `mouseStop()` 方法来处理扩展部件。

*   这个方法不接受任何参数。

**Code examples:**

调用 _mouseUp 方法:

```
$( ".selector" ).mouse( "_mouseUp" ); 
```

# Resizable Widget

Categories: [Interactions](http://www.css88.com/jquery-ui-api/category/interactions/ "View all posts in Interactions")

## version added: 1.0

**Description:** 使用鼠标改变一个元素的尺寸。

## QuickNavExamples

### Options

*   alsoResize
*   animate
*   animateDuration
*   animateEasing
*   aspectRatio
*   autoHide
*   cancel
*   containment
*   delay
*   disabled
*   distance
*   ghost
*   grid
*   handles
*   helper
*   maxHeight
*   maxWidth
*   minHeight
*   minWidth

### Methods

*   destroy
*   disable
*   enable
*   option
*   widget

### Events

*   create
*   resize
*   start
*   stop

jQuery UI Resizable 插件使选定的内容可以调整大小(这以为着那么拥有一些可以拖动的手柄). 你可以指定一个或者多个操作手柄以及指定最小和最大宽度与高度.

### Dependencies

*   UI Core
*   Widget Factory
*   Mouse Interaction

### 其他注意事项：

*   这个 widget 需要一些功能性的 CSS，否则将无法正常工作。 如果你建立一个自定义的主题，使用 widget 指定的 CSS 文件作为一个激活点。

## Options

### alsoResize**Type:** [Selector](http://api.jquery.com/Types/#Selector) or [jQuery](http://api.jquery.com/Types/#jQuery) or [Element](http://api.jquery.com/Types/#Element)

**Default:** `false`在重置元素尺寸大小的同时重置指定的一个或多个元素的尺寸大小。**Code examples:**

使用指定的 `alsoResize` 参数初始化 resizable :

```
$( ".selector" ).resizable({ alsoResize: "#mirror" }); 
```

在初始化后设置或者获取 `alsoResize` 参数 :

```
// getter
var alsoResize = $( ".selector" ).resizable( "option", "alsoResize" );

// setter
$( ".selector" ).resizable( "option", "alsoResize", "#mirror" ); 
```

### animate**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`在调整大小后使用一段动画完成调整.**Code examples:**

使用指定的 `animate` 参数初始化 resizable :

```
$( ".selector" ).resizable({ animate: true }); 
```

在初始化后设置或者获取 `animate` 参数 :

```
// getter
var animate = $( ".selector" ).resizable( "option", "animate" );

// setter
$( ".selector" ).resizable( "option", "animate", true ); 
```

### animateDuration**Type:** [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)

**Default:** `"slow"`当使用`animate`选项时，动画持续的时间。单位毫秒。**允许使用的值:**

*   **Number**: 毫秒数。
*   **String**: 一个表示持续时间的字符串，比如 `"slow"` or `"fast"`。

**Code examples:**

使用指定的 `animateDuration` 参数初始化 resizable :

```
$( ".selector" ).resizable({ animateDuration: "fast" }); 
```

在初始化后设置或者获取 `animateDuration` 参数 :

```
// getter
var animateDuration = $( ".selector" ).resizable( "option", "animateDuration" );

// setter
$( ".selector" ).resizable( "option", "animateDuration", "fast" ); 
```

### animateEasing**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"swing"`动画执行时的缓冲效果。当使用`animate`选项时，哪个 easing （缓冲函数）被应用。**Code examples:**

使用指定的 `animateEasing` 参数初始化 resizable :

```
$( ".selector" ).resizable({ animateEasing: "easeOutBounce" }); 
```

在初始化后设置或者获取 `animateEasing` 参数 :

```
// getter
var animateEasing = $( ".selector" ).resizable( "option", "animateEasing" );

// setter
$( ".selector" ).resizable( "option", "animateEasing", "easeOutBounce" ); 
```

### aspectRatio**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Number](http://api.jquery.com/Types/#Number)

**Default:** `false`该元素是否应限制在一个特定的比例进行缩放。**允许使用的值:**

*   **Boolean**: 如果设置为`true`, 大小将按照原先的宽高比进行调整。
*   **Number**: 强制元素调整大小时保持一个特定的宽高比。

**Code examples:**

使用指定的 `aspectRatio` 参数初始化 resizable :

```
$( ".selector" ).resizable({ aspectRatio: true }); 
```

在初始化后设置或者获取 `aspectRatio` 参数 :

```
// getter
var aspectRatio = $( ".selector" ).resizable( "option", "aspectRatio" );

// setter
$( ".selector" ).resizable( "option", "aspectRatio", true ); 
```

### autoHide**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为真, 将会自动隐藏调整手柄图标,除非鼠标移动到该元素上.**Code examples:**

使用指定的 `autoHide` 参数初始化 resizable :

```
$( ".selector" ).resizable({ autoHide: true }); 
```

在初始化后设置或者获取 `autoHide` 参数 :

```
// getter
var autoHide = $( ".selector" ).resizable( "option", "autoHide" );

// setter
$( ".selector" ).resizable( "option", "autoHide", true ); 
```

### cancel**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `"input,textarea,button,select,option"`如果设置了选择器匹配,将拒绝对匹配元素的大小调整.**Code examples:**

使用指定的 `cancel` 参数初始化 resizable :

```
$( ".selector" ).resizable({ cancel: ".cancel" }); 
```

在初始化后设置或者获取 `cancel` 参数 :

```
// getter
var cancel = $( ".selector" ).resizable( "option", "cancel" );

// setter
$( ".selector" ).resizable( "option", "cancel", ".cancel" ); 
```

### containment**Type:** [Selector](http://api.jquery.com/Types/#Selector) or [Element](http://api.jquery.com/Types/#Element) or [String](http://api.jquery.com/Types/#String)

**Default:** `false`使用指定的元素强制性限制大小调整的界限.**允许使用的值：**

*   **Selector**:resizable 元素将被限制在该选择器匹配的第一个元素的边界内。 如果没有匹配的元素，那么设置将不起作用。
*   **Element**: resizable 元素将被限制在这个元素的边界内。
*   **String**: 可能的值： `"parent"` 和 `"document"`.

**Code examples:**

使用指定的 `containment` 参数初始化 resizable :

```
$( ".selector" ).resizable({ containment: "parent" }); 
```

在初始化后设置或者获取 `containment` 参数 :

```
// getter
var containment = $( ".selector" ).resizable( "option", "containment" );

// setter
$( ".selector" ).resizable( "option", "containment", "parent" ); 
```

### delay**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `0`设定需要经过多少毫秒以后调整才会开始. 如果指定了该参数, 调整不会马上开始,除非鼠标调整动作已经持续了指定的时间.这可以防止误操作对元素进行了非预期的调整.**Code examples:**

使用指定的 `delay` 参数初始化 resizable :

```
$( ".selector" ).resizable({ delay: 150 }); 
```

在初始化后设置或者获取 `delay` 参数 :

```
// getter
var delay = $( ".selector" ).resizable( "option", "delay" );

// setter
$( ".selector" ).resizable( "option", "delay", 150 ); 
```

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为 `true` 将禁止 resizable（缩放）。**Code examples:**

使用指定的 `disabled` 参数初始化 resizable :

```
$( ".selector" ).resizable({ disabled: true }); 
```

在初始化后设置或者获取 `disabled` 参数 :

```
// getter
var disabled = $( ".selector" ).resizable( "option", "disabled" );

// setter
$( ".selector" ).resizable( "option", "disabled", true ); 
```

### distance**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `1`设定调整操作需要移动多少个像素后调整才会开始. 如果指定了该参数, 调整不会马上开始,直到鼠标移动了指定的像素后.这可以防止误操作对元素进行了非预期的调整.**Code examples:**

使用指定的 `distance` 参数初始化 resizable :

```
$( ".selector" ).resizable({ distance: 30 }); 
```

在初始化后设置或者获取 `distance` 参数 :

```
// getter
var distance = $( ".selector" ).resizable( "option", "distance" );

// setter
$( ".selector" ).resizable( "option", "distance", 30 ); 
```

### ghost**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为`true`, 将会在调整过程中看到一个半透明的辅助元素。**Code examples:**

使用指定的 `ghost` 参数初始化 resizable :

```
$( ".selector" ).resizable({ ghost: true }); 
```

在初始化后设置或者获取 `ghost` 参数 :

```
// getter
var ghost = $( ".selector" ).resizable( "option", "ghost" );

// setter
$( ".selector" ).resizable( "option", "ghost", true ); 
```

### grid**Type:** [Array](http://api.jquery.com/Types/#Array)

**Default:** `false`设置调整 x 和 y 改变的像素. 调整大小的元素到网格，每 x 和 y 个像素。数组值: [x, y]。**Code examples:**

使用指定的 `grid` 参数初始化 resizable :

```
$( ".selector" ).resizable({ grid: [ 20, 10 ] }); 
```

在初始化后设置或者获取 `grid` 参数 :

```
// getter
var grid = $( ".selector" ).resizable( "option", "grid" );

// setter
$( ".selector" ).resizable( "option", "grid", [ 20, 10 ] ); 
```

### handles**Type:** [String](http://api.jquery.com/Types/#String) or [Object](http://api.jquery.com/Types/#Object)

**Default:** `"e, s, se"`哪个处理程序被用来 resizing（缩放大小）。**允许使用的值：**

*   **String**: 如果指定一个字符串, 应该是下列清单中的组合:'n, e, s, w, ne, se, sw, nw, all',每项之间使用逗号分隔. 必要的手柄将由插件自动生成.
*   **Object**:

    如果指定一个对象, 要支持下面的键值: { n, e, s, w, ne, se, sw, nw }. 指定的用户调整手柄的任何值应该是一个 jQuery 选择器匹配的子元素. 如果该操作柄不是 resizable 的一个子元素, 你可以提供一个有效的 DOMElement 或者直接提供一个 jQuery 对象.

    *注意: 当生成您自己的手柄，每个手柄必须有`ui-resizable-handle` 样式类，以及适当的`ui-resizable-{direction}`样式类，例如`ui-resizable-s`。*

**Code examples:**

使用指定的 `handles` 参数初始化 resizable :

```
$( ".selector" ).resizable({ handles: "n, e, s, w" }); 
```

在初始化后设置或者获取 `handles` 参数 :

```
// getter
var handles = $( ".selector" ).resizable( "option", "handles" );

// setter
$( ".selector" ).resizable( "option", "handles", "n, e, s, w" ); 
```

### helper**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `false`为大小调整时的代理元素指定一个 css 样式.当调整完成时,这些元素将回到它以前的状态.**Code examples:**

使用指定的 `helper` 参数初始化 resizable :

```
$( ".selector" ).resizable({ helper: "resizable-helper" }); 
```

在初始化后设置或者获取 `helper` 参数 :

```
// getter
var helper = $( ".selector" ).resizable( "option", "helper" );

// setter
$( ".selector" ).resizable( "option", "helper", "resizable-helper" ); 
```

### maxHeight**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `null`为大小调整设定一个最大高度.**Code examples:**

使用指定的 `maxHeight` 参数初始化 resizable :

```
$( ".selector" ).resizable({ maxHeight: 300 }); 
```

在初始化后设置或者获取 `maxHeight` 参数 :

```
// getter
var maxHeight = $( ".selector" ).resizable( "option", "maxHeight" );

// setter
$( ".selector" ).resizable( "option", "maxHeight", 300 ); 
```

### maxWidth**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `null`为大小调整设定一个最大宽度.**Code examples:**

使用指定的 `maxWidth` 参数初始化 resizable :

```
$( ".selector" ).resizable({ maxWidth: 300 }); 
```

在初始化后设置或者获取 `maxWidth` 参数 :

```
// getter
var maxWidth = $( ".selector" ).resizable( "option", "maxWidth" );

// setter
$( ".selector" ).resizable( "option", "maxWidth", 300 ); 
```

### minHeight**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `10`为大小调整设定一个最小高度.**Code examples:**

使用指定的 `minHeight` 参数初始化 resizable :

```
$( ".selector" ).resizable({ minHeight: 150 }); 
```

在初始化后设置或者获取 `minHeight` 参数 :

```
// getter
var minHeight = $( ".selector" ).resizable( "option", "minHeight" );

// setter
$( ".selector" ).resizable( "option", "minHeight", 150 ); 
```

### minWidth**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `10`为大小调整设定一个最小宽度.**Code examples:**

使用指定的 `minWidth` 参数初始化 resizable :

```
$( ".selector" ).resizable({ minWidth: 150 }); 
```

在初始化后设置或者获取 `minWidth` 参数 :

```
// getter
var minWidth = $( ".selector" ).resizable( "option", "minWidth" );

// setter
$( ".selector" ).resizable( "option", "minWidth", 150 ); 
```

## Methods

### destroy()

完全移除调整功能. 这将使元素返回到之前的初始化状态.

*   这个方法不接受任何参数。

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).resizable( "destroy" ); 
```

### disable()

关闭 resizable.

*   这个方法不接受任何参数。

**Code examples:**

调用 disable 方法：

```
$( ".selector" ).resizable( "disable" ); 
```

### enable()

打开 resizable.

*   这个方法不接受任何参数。

**Code examples:**

调用 enable 方法：

```
$( ".selector" ).resizable( "enable" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

通过指定的`optionName`，获取当前关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项名

**Code examples:**

调用这个方法：

```
var isDisabled = $( ".selector" ).resizable( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个对象，它包含表示当前 resizable 的选项 hash 的键/值对。

*   这个方法不接受任何参数。

**Code examples:**

调用这个方法：

```
var options = $( ".selector" ).resizable( "option" ); 
```

### option( optionName, value )

通过指定的`optionName`，设置 resizable 的相关选项值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置值的选项名。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要设置选项的值。

**Code examples:**

调用这个方法：

```
$( ".selector" ).resizable( "option", "disabled", true ); 
```

### option( options )

为 resizable 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)设置的选项/值对的对象。

**Code examples:**

调用这个方法：

```
$( ".selector" ).resizable( "option", { disabled: true } ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个`jQuery`，它包含了 resizable 元素。

*   这个方法不接受任何参数。

**Code examples:**

调用 widget 方法：

```
var widget = $( ".selector" ).resizable( "widget" ); 
```

## Events

### create( event, ui )Type: `resizecreate`

此事件会在 resizable 创建时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空对象，包括是为了和其他事件的一致性。*

**Code examples:**

使用指定的 create 回调初始化一个 resizable：

```
$( ".selector" ).resizable({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听到 resizecreate 事件：

```
$( ".selector" ).on( "resizecreate", function( event, ui ) {} ); 
```

### resize( event, ui )Type: `resize`

这个事件将在拖动手柄进行调整时触发.

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **element**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被 resized 的元素。
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被 resized 元素的助手。
    *   **originalElement**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被包裹前原先的元素。
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)resizable 元素被 resized（缩放）前的 CSS 的 position（位置）对象，如`{ left, top }` 。
    *   **originalSize**Type: [Object](http://api.jquery.com/Types/#Object)resizable 元素被 resized（缩放）前的尺寸对象，如`{ width, height }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)当前可 resizable（缩放）元素的 CSS 的 position（位置）对象，如{ top, left }。
    *   **size**Type: [Object](http://api.jquery.com/Types/#Object)当前可 resizable（缩放）元素的尺寸对象，`{ width, height }`。

**Code examples:**

使用指定的 resize 回调初始化一个 resizable：

```
$( ".selector" ).resizable({
  resize: function( event, ui ) {}
}); 
```

绑定一个事件监听到 resize 事件：

```
$( ".selector" ).on( "resize", function( event, ui ) {} ); 
```

### start( event, ui )Type: `resizestart`

这个事件将在调整操作开始时触发.

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **element**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被 resized 的元素。
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被 resized 元素的助手。
    *   **originalElement**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被包裹前原先的元素。
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)resizable 元素被 resized（缩放）前的 CSS 的 position（位置）对象，如`{ left, top }` 。
    *   **originalSize**Type: [Object](http://api.jquery.com/Types/#Object)resizable 元素被 resized（缩放）前的尺寸对象，如`{ width, height }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)当前可 resizable（缩放）元素的 CSS 的 position（位置）对象，如{ top, left }。
    *   **size**Type: [Object](http://api.jquery.com/Types/#Object)当前可 resizable（缩放）元素的尺寸对象，`{ width, height }`。

**Code examples:**

使用指定的 start 回调初始化一个 resizable：

```
$( ".selector" ).resizable({
  start: function( event, ui ) {}
}); 
```

绑定一个事件监听到 resizestart 事件：

```
$( ".selector" ).on( "resizestart", function( event, ui ) {} ); 
```

### stop( event, ui )Type: `resizestop`

这个事件将在调整操作结束后触发.

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **element**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被 resized 的元素。
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被 resized 元素的助手。
    *   **originalElement**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被包裹前原先的元素。
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)resizable 元素被 resized（缩放）前的 CSS 的 position（位置）对象，如`{ left, top }` 。
    *   **originalSize**Type: [Object](http://api.jquery.com/Types/#Object)resizable 元素被 resized（缩放）前的尺寸对象，如`{ width, height }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)当前可 resizable（缩放）元素的 CSS 的 position（位置）对象，如{ top, left }。
    *   **size**Type: [Object](http://api.jquery.com/Types/#Object)当前可 resizable（缩放）元素的尺寸对象，`{ width, height }`。

**Code examples:**

使用指定的 stop 回调初始化一个 resizable：

```
$( ".selector" ).resizable({
  stop: function( event, ui ) {}
}); 
```

绑定一个事件监听到 resizestop 事件：

```
$( ".selector" ).on( "resizestop", function( event, ui ) {} ); 
```

## Example:

#### A simple jQuery UI Resizable.

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>resizable demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #resizable {
    width: 100px;
    height: 100px;
    background: #ccc;
}    </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<div id="resizable"></div>

<script>
$( "#resizable" ).resizable();
</script>

</body>
</html> 
```

# Resizable Widget

Categories: [Interactions](http://www.css88.com/jquery-ui-api/category/interactions/ "View all posts in Interactions")

## version added: 1.0

**Description:** 使用鼠标改变一个元素的尺寸。

## QuickNavExamples

### Options

*   alsoResize
*   animate
*   animateDuration
*   animateEasing
*   aspectRatio
*   autoHide
*   cancel
*   containment
*   delay
*   disabled
*   distance
*   ghost
*   grid
*   handles
*   helper
*   maxHeight
*   maxWidth
*   minHeight
*   minWidth

### Methods

*   destroy
*   disable
*   enable
*   option
*   widget

### Events

*   create
*   resize
*   start
*   stop

jQuery UI Resizable 插件使选定的内容可以调整大小(这以为着那么拥有一些可以拖动的手柄). 你可以指定一个或者多个操作手柄以及指定最小和最大宽度与高度.

### Dependencies

*   UI Core
*   Widget Factory
*   Mouse Interaction

### 其他注意事项：

*   这个 widget 需要一些功能性的 CSS，否则将无法正常工作。 如果你建立一个自定义的主题，使用 widget 指定的 CSS 文件作为一个激活点。

## Options

### alsoResize**Type:** [Selector](http://api.jquery.com/Types/#Selector) or [jQuery](http://api.jquery.com/Types/#jQuery) or [Element](http://api.jquery.com/Types/#Element)

**Default:** `false`在重置元素尺寸大小的同时重置指定的一个或多个元素的尺寸大小。**Code examples:**

使用指定的 `alsoResize` 参数初始化 resizable :

```
$( ".selector" ).resizable({ alsoResize: "#mirror" }); 
```

在初始化后设置或者获取 `alsoResize` 参数 :

```
// getter
var alsoResize = $( ".selector" ).resizable( "option", "alsoResize" );

// setter
$( ".selector" ).resizable( "option", "alsoResize", "#mirror" ); 
```

### animate**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`在调整大小后使用一段动画完成调整.**Code examples:**

使用指定的 `animate` 参数初始化 resizable :

```
$( ".selector" ).resizable({ animate: true }); 
```

在初始化后设置或者获取 `animate` 参数 :

```
// getter
var animate = $( ".selector" ).resizable( "option", "animate" );

// setter
$( ".selector" ).resizable( "option", "animate", true ); 
```

### animateDuration**Type:** [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)

**Default:** `"slow"`当使用`animate`选项时，动画持续的时间。单位毫秒。**允许使用的值:**

*   **Number**: 毫秒数。
*   **String**: 一个表示持续时间的字符串，比如 `"slow"` or `"fast"`。

**Code examples:**

使用指定的 `animateDuration` 参数初始化 resizable :

```
$( ".selector" ).resizable({ animateDuration: "fast" }); 
```

在初始化后设置或者获取 `animateDuration` 参数 :

```
// getter
var animateDuration = $( ".selector" ).resizable( "option", "animateDuration" );

// setter
$( ".selector" ).resizable( "option", "animateDuration", "fast" ); 
```

### animateEasing**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"swing"`动画执行时的缓冲效果。当使用`animate`选项时，哪个 easing （缓冲函数）被应用。**Code examples:**

使用指定的 `animateEasing` 参数初始化 resizable :

```
$( ".selector" ).resizable({ animateEasing: "easeOutBounce" }); 
```

在初始化后设置或者获取 `animateEasing` 参数 :

```
// getter
var animateEasing = $( ".selector" ).resizable( "option", "animateEasing" );

// setter
$( ".selector" ).resizable( "option", "animateEasing", "easeOutBounce" ); 
```

### aspectRatio**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Number](http://api.jquery.com/Types/#Number)

**Default:** `false`该元素是否应限制在一个特定的比例进行缩放。**允许使用的值:**

*   **Boolean**: 如果设置为`true`, 大小将按照原先的宽高比进行调整。
*   **Number**: 强制元素调整大小时保持一个特定的宽高比。

**Code examples:**

使用指定的 `aspectRatio` 参数初始化 resizable :

```
$( ".selector" ).resizable({ aspectRatio: true }); 
```

在初始化后设置或者获取 `aspectRatio` 参数 :

```
// getter
var aspectRatio = $( ".selector" ).resizable( "option", "aspectRatio" );

// setter
$( ".selector" ).resizable( "option", "aspectRatio", true ); 
```

### autoHide**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为真, 将会自动隐藏调整手柄图标,除非鼠标移动到该元素上.**Code examples:**

使用指定的 `autoHide` 参数初始化 resizable :

```
$( ".selector" ).resizable({ autoHide: true }); 
```

在初始化后设置或者获取 `autoHide` 参数 :

```
// getter
var autoHide = $( ".selector" ).resizable( "option", "autoHide" );

// setter
$( ".selector" ).resizable( "option", "autoHide", true ); 
```

### cancel**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `"input,textarea,button,select,option"`如果设置了选择器匹配,将拒绝对匹配元素的大小调整.**Code examples:**

使用指定的 `cancel` 参数初始化 resizable :

```
$( ".selector" ).resizable({ cancel: ".cancel" }); 
```

在初始化后设置或者获取 `cancel` 参数 :

```
// getter
var cancel = $( ".selector" ).resizable( "option", "cancel" );

// setter
$( ".selector" ).resizable( "option", "cancel", ".cancel" ); 
```

### containment**Type:** [Selector](http://api.jquery.com/Types/#Selector) or [Element](http://api.jquery.com/Types/#Element) or [String](http://api.jquery.com/Types/#String)

**Default:** `false`使用指定的元素强制性限制大小调整的界限.**允许使用的值：**

*   **Selector**:resizable 元素将被限制在该选择器匹配的第一个元素的边界内。 如果没有匹配的元素，那么设置将不起作用。
*   **Element**: resizable 元素将被限制在这个元素的边界内。
*   **String**: 可能的值： `"parent"` 和 `"document"`.

**Code examples:**

使用指定的 `containment` 参数初始化 resizable :

```
$( ".selector" ).resizable({ containment: "parent" }); 
```

在初始化后设置或者获取 `containment` 参数 :

```
// getter
var containment = $( ".selector" ).resizable( "option", "containment" );

// setter
$( ".selector" ).resizable( "option", "containment", "parent" ); 
```

### delay**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `0`设定需要经过多少毫秒以后调整才会开始. 如果指定了该参数, 调整不会马上开始,除非鼠标调整动作已经持续了指定的时间.这可以防止误操作对元素进行了非预期的调整.**Code examples:**

使用指定的 `delay` 参数初始化 resizable :

```
$( ".selector" ).resizable({ delay: 150 }); 
```

在初始化后设置或者获取 `delay` 参数 :

```
// getter
var delay = $( ".selector" ).resizable( "option", "delay" );

// setter
$( ".selector" ).resizable( "option", "delay", 150 ); 
```

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为 `true` 将禁止 resizable（缩放）。**Code examples:**

使用指定的 `disabled` 参数初始化 resizable :

```
$( ".selector" ).resizable({ disabled: true }); 
```

在初始化后设置或者获取 `disabled` 参数 :

```
// getter
var disabled = $( ".selector" ).resizable( "option", "disabled" );

// setter
$( ".selector" ).resizable( "option", "disabled", true ); 
```

### distance**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `1`设定调整操作需要移动多少个像素后调整才会开始. 如果指定了该参数, 调整不会马上开始,直到鼠标移动了指定的像素后.这可以防止误操作对元素进行了非预期的调整.**Code examples:**

使用指定的 `distance` 参数初始化 resizable :

```
$( ".selector" ).resizable({ distance: 30 }); 
```

在初始化后设置或者获取 `distance` 参数 :

```
// getter
var distance = $( ".selector" ).resizable( "option", "distance" );

// setter
$( ".selector" ).resizable( "option", "distance", 30 ); 
```

### ghost**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为`true`, 将会在调整过程中看到一个半透明的辅助元素。**Code examples:**

使用指定的 `ghost` 参数初始化 resizable :

```
$( ".selector" ).resizable({ ghost: true }); 
```

在初始化后设置或者获取 `ghost` 参数 :

```
// getter
var ghost = $( ".selector" ).resizable( "option", "ghost" );

// setter
$( ".selector" ).resizable( "option", "ghost", true ); 
```

### grid**Type:** [Array](http://api.jquery.com/Types/#Array)

**Default:** `false`设置调整 x 和 y 改变的像素. 调整大小的元素到网格，每 x 和 y 个像素。数组值: [x, y]。**Code examples:**

使用指定的 `grid` 参数初始化 resizable :

```
$( ".selector" ).resizable({ grid: [ 20, 10 ] }); 
```

在初始化后设置或者获取 `grid` 参数 :

```
// getter
var grid = $( ".selector" ).resizable( "option", "grid" );

// setter
$( ".selector" ).resizable( "option", "grid", [ 20, 10 ] ); 
```

### handles**Type:** [String](http://api.jquery.com/Types/#String) or [Object](http://api.jquery.com/Types/#Object)

**Default:** `"e, s, se"`哪个处理程序被用来 resizing（缩放大小）。**允许使用的值：**

*   **String**: 如果指定一个字符串, 应该是下列清单中的组合:'n, e, s, w, ne, se, sw, nw, all',每项之间使用逗号分隔. 必要的手柄将由插件自动生成.
*   **Object**:

    如果指定一个对象, 要支持下面的键值: { n, e, s, w, ne, se, sw, nw }. 指定的用户调整手柄的任何值应该是一个 jQuery 选择器匹配的子元素. 如果该操作柄不是 resizable 的一个子元素, 你可以提供一个有效的 DOMElement 或者直接提供一个 jQuery 对象.

    *注意: 当生成您自己的手柄，每个手柄必须有`ui-resizable-handle` 样式类，以及适当的`ui-resizable-{direction}`样式类，例如`ui-resizable-s`。*

**Code examples:**

使用指定的 `handles` 参数初始化 resizable :

```
$( ".selector" ).resizable({ handles: "n, e, s, w" }); 
```

在初始化后设置或者获取 `handles` 参数 :

```
// getter
var handles = $( ".selector" ).resizable( "option", "handles" );

// setter
$( ".selector" ).resizable( "option", "handles", "n, e, s, w" ); 
```

### helper**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `false`为大小调整时的代理元素指定一个 css 样式.当调整完成时,这些元素将回到它以前的状态.**Code examples:**

使用指定的 `helper` 参数初始化 resizable :

```
$( ".selector" ).resizable({ helper: "resizable-helper" }); 
```

在初始化后设置或者获取 `helper` 参数 :

```
// getter
var helper = $( ".selector" ).resizable( "option", "helper" );

// setter
$( ".selector" ).resizable( "option", "helper", "resizable-helper" ); 
```

### maxHeight**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `null`为大小调整设定一个最大高度.**Code examples:**

使用指定的 `maxHeight` 参数初始化 resizable :

```
$( ".selector" ).resizable({ maxHeight: 300 }); 
```

在初始化后设置或者获取 `maxHeight` 参数 :

```
// getter
var maxHeight = $( ".selector" ).resizable( "option", "maxHeight" );

// setter
$( ".selector" ).resizable( "option", "maxHeight", 300 ); 
```

### maxWidth**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `null`为大小调整设定一个最大宽度.**Code examples:**

使用指定的 `maxWidth` 参数初始化 resizable :

```
$( ".selector" ).resizable({ maxWidth: 300 }); 
```

在初始化后设置或者获取 `maxWidth` 参数 :

```
// getter
var maxWidth = $( ".selector" ).resizable( "option", "maxWidth" );

// setter
$( ".selector" ).resizable( "option", "maxWidth", 300 ); 
```

### minHeight**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `10`为大小调整设定一个最小高度.**Code examples:**

使用指定的 `minHeight` 参数初始化 resizable :

```
$( ".selector" ).resizable({ minHeight: 150 }); 
```

在初始化后设置或者获取 `minHeight` 参数 :

```
// getter
var minHeight = $( ".selector" ).resizable( "option", "minHeight" );

// setter
$( ".selector" ).resizable( "option", "minHeight", 150 ); 
```

### minWidth**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `10`为大小调整设定一个最小宽度.**Code examples:**

使用指定的 `minWidth` 参数初始化 resizable :

```
$( ".selector" ).resizable({ minWidth: 150 }); 
```

在初始化后设置或者获取 `minWidth` 参数 :

```
// getter
var minWidth = $( ".selector" ).resizable( "option", "minWidth" );

// setter
$( ".selector" ).resizable( "option", "minWidth", 150 ); 
```

## Methods

### destroy()

完全移除调整功能. 这将使元素返回到之前的初始化状态.

*   这个方法不接受任何参数。

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).resizable( "destroy" ); 
```

### disable()

关闭 resizable.

*   这个方法不接受任何参数。

**Code examples:**

调用 disable 方法：

```
$( ".selector" ).resizable( "disable" ); 
```

### enable()

打开 resizable.

*   这个方法不接受任何参数。

**Code examples:**

调用 enable 方法：

```
$( ".selector" ).resizable( "enable" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

通过指定的`optionName`，获取当前关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项名

**Code examples:**

调用这个方法：

```
var isDisabled = $( ".selector" ).resizable( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个对象，它包含表示当前 resizable 的选项 hash 的键/值对。

*   这个方法不接受任何参数。

**Code examples:**

调用这个方法：

```
var options = $( ".selector" ).resizable( "option" ); 
```

### option( optionName, value )

通过指定的`optionName`，设置 resizable 的相关选项值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置值的选项名。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要设置选项的值。

**Code examples:**

调用这个方法：

```
$( ".selector" ).resizable( "option", "disabled", true ); 
```

### option( options )

为 resizable 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)设置的选项/值对的对象。

**Code examples:**

调用这个方法：

```
$( ".selector" ).resizable( "option", { disabled: true } ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个`jQuery`，它包含了 resizable 元素。

*   这个方法不接受任何参数。

**Code examples:**

调用 widget 方法：

```
var widget = $( ".selector" ).resizable( "widget" ); 
```

## Events

### create( event, ui )Type: `resizecreate`

此事件会在 resizable 创建时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空对象，包括是为了和其他事件的一致性。*

**Code examples:**

使用指定的 create 回调初始化一个 resizable：

```
$( ".selector" ).resizable({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听到 resizecreate 事件：

```
$( ".selector" ).on( "resizecreate", function( event, ui ) {} ); 
```

### resize( event, ui )Type: `resize`

这个事件将在拖动手柄进行调整时触发.

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **element**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被 resized 的元素。
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被 resized 元素的助手。
    *   **originalElement**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被包裹前原先的元素。
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)resizable 元素被 resized（缩放）前的 CSS 的 position（位置）对象，如`{ left, top }` 。
    *   **originalSize**Type: [Object](http://api.jquery.com/Types/#Object)resizable 元素被 resized（缩放）前的尺寸对象，如`{ width, height }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)当前可 resizable（缩放）元素的 CSS 的 position（位置）对象，如{ top, left }。
    *   **size**Type: [Object](http://api.jquery.com/Types/#Object)当前可 resizable（缩放）元素的尺寸对象，`{ width, height }`。

**Code examples:**

使用指定的 resize 回调初始化一个 resizable：

```
$( ".selector" ).resizable({
  resize: function( event, ui ) {}
}); 
```

绑定一个事件监听到 resize 事件：

```
$( ".selector" ).on( "resize", function( event, ui ) {} ); 
```

### start( event, ui )Type: `resizestart`

这个事件将在调整操作开始时触发.

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **element**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被 resized 的元素。
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被 resized 元素的助手。
    *   **originalElement**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被包裹前原先的元素。
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)resizable 元素被 resized（缩放）前的 CSS 的 position（位置）对象，如`{ left, top }` 。
    *   **originalSize**Type: [Object](http://api.jquery.com/Types/#Object)resizable 元素被 resized（缩放）前的尺寸对象，如`{ width, height }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)当前可 resizable（缩放）元素的 CSS 的 position（位置）对象，如{ top, left }。
    *   **size**Type: [Object](http://api.jquery.com/Types/#Object)当前可 resizable（缩放）元素的尺寸对象，`{ width, height }`。

**Code examples:**

使用指定的 start 回调初始化一个 resizable：

```
$( ".selector" ).resizable({
  start: function( event, ui ) {}
}); 
```

绑定一个事件监听到 resizestart 事件：

```
$( ".selector" ).on( "resizestart", function( event, ui ) {} ); 
```

### stop( event, ui )Type: `resizestop`

这个事件将在调整操作结束后触发.

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **element**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被 resized 的元素。
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被 resized 元素的助手。
    *   **originalElement**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象代表被包裹前原先的元素。
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)resizable 元素被 resized（缩放）前的 CSS 的 position（位置）对象，如`{ left, top }` 。
    *   **originalSize**Type: [Object](http://api.jquery.com/Types/#Object)resizable 元素被 resized（缩放）前的尺寸对象，如`{ width, height }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)当前可 resizable（缩放）元素的 CSS 的 position（位置）对象，如{ top, left }。
    *   **size**Type: [Object](http://api.jquery.com/Types/#Object)当前可 resizable（缩放）元素的尺寸对象，`{ width, height }`。

**Code examples:**

使用指定的 stop 回调初始化一个 resizable：

```
$( ".selector" ).resizable({
  stop: function( event, ui ) {}
}); 
```

绑定一个事件监听到 resizestop 事件：

```
$( ".selector" ).on( "resizestop", function( event, ui ) {} ); 
```

## Example:

#### A simple jQuery UI Resizable.

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>resizable demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #resizable {
    width: 100px;
    height: 100px;
    background: #ccc;
}    </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<div id="resizable"></div>

<script>
$( "#resizable" ).resizable();
</script>

</body>
</html> 
```

# Selectable Widget

Categories: [Interactions](http://www.css88.com/jquery-ui-api/category/interactions/ "View all posts in Interactions")

## version added: 1.0

**Description:** 使用鼠标选择一个或一组元素。

## QuickNavExamples

### Options

*   appendTo
*   autoRefresh
*   cancel
*   delay
*   disabled
*   distance
*   filter
*   tolerance

### Methods

*   destroy
*   disable
*   enable
*   option
*   refresh
*   widget

### Events

*   create
*   selected
*   selecting
*   start
*   stop
*   unselected
*   unselectingjQuery UI Selectable 插件允许一个元素被鼠标划出的选择区域选中. 同样, 元素也可以被点击选中或者同时按住 Ctrl/Meta 键, 允许多个(非连续)的选择.

### 依赖关系

*   UI Core
*   Widget Factory
*   Mouse Interaction

### 其他注意事项：

*   这个 widget 需要一些功能性的 CSS，否则将无法正常工作。 如果你建立一个自定义的主题，使用 widget 指定的 CSS 文件作为一个激活点。

## Options

### appendTo**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `"body"`选择帮手（套索） 应追加到哪个元素 。**Code examples:**

使用指定的 `appendTo` 参数初始化 selectable :

```
$( ".selector" ).selectable({ appendTo: "#someElem" }); 
```

在初始化后设置或者获取 `appendTo` 选项 :

```
// getter
var appendTo = $( ".selector" ).selectable( "option", "appendTo" );

// setter
$( ".selector" ).selectable( "option", "appendTo", "#someElem" ); 
```

### autoRefresh**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `true`这个选项确定每个选择操作开始时如何刷新(重新计算)每个选择项的位置和大小. 如果你有很多很多选择项, 你应当设置此项为 false 并且手动调用`refresh()` 方法.**Code examples:**

使用指定的 `autoRefresh` 参数初始化 selectable :

```
$( ".selector" ).selectable({ autoRefresh: false }); 
```

在初始化后设置或者获取 `autoRefresh` 选项 :

```
// getter
var autoRefresh = $( ".selector" ).selectable( "option", "autoRefresh" );

// setter
$( ".selector" ).selectable( "option", "autoRefresh", false ); 
```

### cancel**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `"input,textarea,button,select,option"`如果你使用了匹配选择器,符合匹配的元素将被禁止可选.**Code examples:**

使用指定的 `cancel` 参数初始化 selectable :

```
$( ".selector" ).selectable({ cancel: "a,.cancel" }); 
```

在初始化后设置或者获取 `cancel` 选项 :

```
// getter
var cancel = $( ".selector" ).selectable( "option", "cancel" );

// setter
$( ".selector" ).selectable( "option", "cancel", "a,.cancel" ); 
```

### delay**Type:** [Integer](http://api.jquery.com/Types/#Integer)

**Default:** `0`定义需要经过多少毫秒后选择才会开始. 这可以预防意外的点击造成元素被选择.**Code examples:**

使用指定的 `delay` 参数初始化 selectable :

```
$( ".selector" ).selectable({ delay: 150 }); 
```

在初始化后设置或者获取 `delay` 选项 :

```
// getter
var delay = $( ".selector" ).selectable( "option", "delay" );

// setter
$( ".selector" ).selectable( "option", "delay", 150 ); 
```

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为 `true` 将禁止 selectable。**Code examples:**

使用指定的 `disabled` 参数初始化 selectable :

```
$( ".selector" ).selectable({ disabled: true }); 
```

在初始化后设置或者获取 `disabled` 选项 :

```
// getter
var disabled = $( ".selector" ).selectable( "option", "disabled" );

// setter
$( ".selector" ).selectable( "option", "disabled", true ); 
```

### distance**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `0`定义需要移动多少个像素选择才会开始. 如果指定了该项, 选择不会马上开始,而是会在鼠标移动了指定像素的距离之后才会开始.**Code examples:**

使用指定的 `distance` 参数初始化 selectable :

```
$( ".selector" ).selectable({ distance: 30 }); 
```

在初始化后设置或者获取 `distance` 选项 :

```
// getter
var distance = $( ".selector" ).selectable( "option", "distance" );

// setter
$( ".selector" ).selectable( "option", "distance", 30 ); 
```

### filter**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `"*"`匹配子元素中那些符合条件的元素才可以被选择.**Code examples:**

使用指定的 `filter` 参数初始化 selectable :

```
$( ".selector" ).selectable({ filter: "li" }); 
```

在初始化后设置或者获取 `filter` 选项 :

```
// getter
var filter = $( ".selector" ).selectable( "option", "filter" );

// setter
$( ".selector" ).selectable( "option", "filter", "li" ); 
```

### tolerance**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"touch"`指定那种模式，用来测试套索是否应该选择一个项目。允许使用的值:

*   `"fit"`: 套索完全重叠的项目。
*   `"touch"`: 套索重叠的项目任何部分。

**Code examples:**

使用指定的 `tolerance` 参数初始化 selectable :

```
$( ".selector" ).selectable({ tolerance: "fit" }); 
```

在初始化后设置或者获取 `tolerance` 选项 :

```
// getter
var tolerance = $( ".selector" ).selectable( "option", "tolerance" );

// setter
$( ".selector" ).selectable( "option", "tolerance", "fit" ); 
```

## Methods

### destroy()

完全移除 selectable 功能. 这将使元素返回到之前的初始化状态.

*   这个方法不接受任何参数。

**Code examples:**

调用 destroy 方法:

```
$( ".selector" ).selectable( "destroy" ); 
```

### disable()

禁用 selectable.

*   这个方法不接受任何参数。

**Code examples:**

调用 disable 方法:

```
$( ".selector" ).selectable( "disable" ); 
```

### enable()

启用 selectable.

*   这个方法不接受任何参数。

**Code examples:**

调用 enable 方法:

```
$( ".selector" ).selectable( "enable" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

通过指定的`optionName`，获取当前关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项名

**Code examples:**

调用 方法:

```
var isDisabled = $( ".selector" ).selectable( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个对象，它包含表示当前 resizable 的选项 hash 的键/值对。

*   这个方法不接受任何参数。

**Code examples:**

调用这个方法:

```
var options = $( ".selector" ).selectable( "option" ); 
```

### option( optionName, value )

通过指定的`optionName`，设置 selectable 的相关选项值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置值的选项名。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要设置选项的值。

**Code examples:**

调用这个方法:

```
$( ".selector" ).selectable( "option", "disabled", true ); 
```

### option( options )

为 selectable 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)用来设置的选项/值对的对象。

**Code examples:**

调用这个方法:

```
$( ".selector" ).selectable( "option", { disabled: true } ); 
```

### refresh()

刷新每个选择项的位置和大小. 这个方法用来手动重新计算选择项的位置和大小,在`autoRefresh`设置为`false`时很有用。

*   这个方法不接受任何参数。

**Code examples:**

调用 refresh 方法:

```
$( ".selector" ).selectable( "refresh" ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个`jQuery`，它包含了 selectable 元素。

*   这个方法不接受任何参数。

**Code examples:**

调用 widget 方法:

```
var widget = $( ".selector" ).selectable( "widget" ); 
```

## Events

### create( event, ui )Type: `selectablecreate`

此事件会在 selectable 创建时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空对象，包括是为了和其他事件的一致性。*

**Code examples:**

使用指定的 create 回调初始化一个 selectable：

```
$( ".selector" ).selectable({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听到 selectablecreate 事件：

```
$( ".selector" ).on( "selectablecreate", function( event, ui ) {} ); 
```

### selected( event, ui )Type: `selectableselected`

此事件会在选择操作结束时，在添加到选择的每个元素上触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **selected**Type: [Element](http://api.jquery.com/Types/#Element)已被选择的 selectable 项。

**Code examples:**

使用指定的 selected 回调初始化一个 selectable：

```
$( ".selector" ).selectable({
  selected: function( event, ui ) {}
}); 
```

绑定一个事件监听到 selectableselected 事件：

```
$( ".selector" ).on( "selectableselected", function( event, ui ) {} ); 
```

### selecting( event, ui )Type: `selectableselecting`

此事件会在选择操作过程中，在添加到选择的每个元素上触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **selecting**Type: [Element](http://api.jquery.com/Types/#Element)当前已被选择的 selectable 项。

**Code examples:**

使用指定的 selecting 回调初始化一个 selectablec：

```
$( ".selector" ).selectable({
  selecting: function( event, ui ) {}
}); 
```

绑定一个事件监听到 selectableselecting 事件：

```
$( ".selector" ).on( "selectableselecting", function( event, ui ) {} ); 
```

### start( event, ui )Type: `selectablestart`

这个事件将在选择操作开始时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空对象，包括是为了和其他事件的一致性。*

**Code examples:**

使用指定的 start 回调初始化一个 selectable：

```
$( ".selector" ).selectable({
  start: function( event, ui ) {}
}); 
```

绑定一个事件监听到 selectablestart 事件：

```
$( ".selector" ).on( "selectablestart", function( event, ui ) {} ); 
```

### stop( event, ui )Type: `selectablestop`

这个事件将在选择操作结束后触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空对象，包括是为了和其他事件的一致性。*

**Code examples:**

使用指定的 stop 回调初始化一个 selectable：

```
$( ".selector" ).selectable({
  stop: function( event, ui ) {}
}); 
```

绑定一个事件监听到 selectablestop 事件：

```
$( ".selector" ).on( "selectablestop", function( event, ui ) {} ); 
```

### unselected( event, ui )Type: `selectableunselected`

此事件会在选择操作结束时，在从选择元素集合中移除的每个元素上触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **unselected**Type: [Element](http://api.jquery.com/Types/#Element)已被取消选中的可选择项。

**Code examples:**

使用指定的 unselected 回调初始化一个 selectable：

```
$( ".selector" ).selectable({
  unselected: function( event, ui ) {}
}); 
```

绑定一个事件监听到 selectableunselected 事件：

```
$( ".selector" ).on( "selectableunselected", function( event, ui ) {} ); 
```

### unselecting( event, ui )Type: `selectableunselecting`

此事件会在选择操作过程中，在从选择元素集合中移除的每个元素上触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **unselecting**Type: [Element](http://api.jquery.com/Types/#Element)当前已被取消选中的可选择项。

**Code examples:**

使用指定的 unselecting 回调初始化一个 selectable：

```
$( ".selector" ).selectable({
  unselecting: function( event, ui ) {}
}); 
```

绑定一个事件监听到 selectableunselecting 事件：

```
$( ".selector" ).on( "selectableunselecting", function( event, ui ) {} ); 
```

## Example:

#### A simple jQuery UI Selectable.

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>selectable demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #selectable .ui-selecting {
    background: #ccc;
  }
  #selectable .ui-selected {
    background: #999;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<ul id="selectable">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
  <li>Item 4</li>
  <li>Item 5</li>
</ul>

<script>
$( "#selectable" ).selectable();
</script>

</body>
</html> 
```

# Sortable Widget

Categories: [Interactions](http://www.css88.com/jquery-ui-api/category/interactions/ "View all posts in Interactions")

## version added: 1.0

**Description:** 使用鼠标调整列表中或者网格中元素的排序。

## QuickNavExamples

### Options

*   appendTo
*   axis
*   cancel
*   connectWith
*   containment
*   cursor
*   cursorAt
*   delay
*   disabled
*   distance
*   dropOnEmpty
*   forceHelperSize
*   forcePlaceholderSize
*   grid
*   handle
*   helper
*   items
*   opacity
*   placeholder
*   revert
*   scroll
*   scrollSensitivity
*   scrollSpeed
*   tolerance
*   zIndex

### Methods

*   cancel
*   destroy
*   disable
*   enable
*   option
*   refresh
*   refreshPositions
*   serialize
*   toArray
*   widget

### Events

*   activate
*   beforeStop
*   change
*   create
*   deactivate
*   out
*   over
*   receive
*   remove
*   sort
*   start
*   stop
*   update

jQuery UI 可排序（Sortable）插件让被被选择的元素通过鼠标拖拽进行排序。

*注意：为了排序表格中的行，`tbody`元素必须作为 sortable（可排序元素），而不是在`table`。*

### Dependencies

*   UI Core
*   Widget Factory
*   Mouse Interaction

## Options

### appendTo**Type:** [jQuery](http://api.jquery.com/Types/#jQuery) or [Element](http://api.jquery.com/Types/#Element) or [Selector](http://api.jquery.com/Types/#Selector) or [String](http://api.jquery.com/Types/#String)

**Default:** `"parent"`确定可移动的辅助元素在拖动时可以被添加到何处 (例如, 解决重叠/ zIndex 问题)。**支持多种类型:**

*   **jQuery**: 一个 jQuery 对象，包含辅助（helper）元素要追加到的元素。
*   **Element**: 要被追加辅助（helper）元素的元素。
*   **Selector**: 一个选择器，指定哪个元素要追加辅助（helper）元素。
*   **String**:字符串`"parent"`将促使助手（helper）成为 sortable 项目的同级。

**Code examples:**

使用指定的 `appendTo` 参数初始化 sortable :

```
$( ".selector" ).sortable({ appendTo: document.body }); 
```

在初始化后设置或者获取 `appendTo` 参数：

```
// getter
var appendTo = $( ".selector" ).sortable( "option", "appendTo" );

// setter
$( ".selector" ).sortable( "option", "appendTo", document.body ); 
```

### axis**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `false`如果定义了该参数, 元素可以在水平或垂直方向上实现拖动. 允许使用的值:`"x"`, `"y"`。**Code examples:**

使用指定的 `axis` 参数初始化 sortable :

```
$( ".selector" ).sortable({ axis: "x" }); 
```

在初始化后设置或者获取 `axis` 参数：

```
// getter
var axis = $( ".selector" ).sortable( "option", "axis" );

// setter
$( ".selector" ).sortable( "option", "axis", "x" ); 
```

### cancel**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `"input,textarea,button,select,option"`对符合选择器匹配规则的元素不进行排序。**Code examples:**

使用指定的 `cancel` 参数初始化 sortable :

```
$( ".selector" ).sortable({ cancel: "a,button" }); 
```

在初始化后设置或者获取 `cancel` 参数：

```
// getter
var cancel = $( ".selector" ).sortable( "option", "cancel" );

// setter
$( ".selector" ).sortable( "option", "cancel", "a,button" ); 
```

### connectWith**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `false`列表中的项目需被连接的另一个 sortable 元素的选择器。这是一个单向关系，如果您想要项目被双向连接，必须在两个 sortable 元素上都设置 `connectWith` 选项。**Code examples:**

使用指定的 `connectWith` 参数初始化 sortable :

```
$( ".selector" ).sortable({ connectWith: "#shopping-cart" }); 
```

在初始化后设置或者获取 `connectWith` 参数：

```
// getter
var connectWith = $( ".selector" ).sortable( "option", "connectWith" );

// setter
$( ".selector" ).sortable( "option", "connectWith", "#shopping-cart" ); 
```

### containment**Type:** [Element](http://api.jquery.com/Types/#Element) or [Selector](http://api.jquery.com/Types/#Selector) or [String](http://api.jquery.com/Types/#String)

**Default:** `false`

定义一个边界，限制拖动范围在指定的 DOM 元素内。

注意：为限制拖动范围，指定的元素必须有一个可计算的宽度和高度（但不一定是显式的）。例如，如果你的 sortable 元素的子元素有`float: left`样式，并且指定`containment: "parent"`，那么 sortable/parent 容器必须要有`float: left`样式，或者他将有`height: 0`样式，导致不确定的行为。

**支持多种类型:**

*   **Element**: 一个用来作为容器的元素。
*   **Selector**:一个选择器指定的元素，这个元素用来作为容器
*   **String**: 一个字符串指定的元素，这个元素用来作为容器。可能的值: `"parent"`, `"document"`, `"window"`。

**Code examples:**

使用指定的 `containment` 参数初始化 sortable :

```
$( ".selector" ).sortable({ containment: "parent" }); 
```

在初始化后设置或者获取 `containment` 参数：

```
// getter
var containment = $( ".selector" ).sortable( "option", "containment" );

// setter
$( ".selector" ).sortable( "option", "containment", "parent" ); 
```

### cursor**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"auto"`定义排序拖动时的鼠标指针样式.**Code examples:**

使用指定的 `cursor` 参数初始化 sortable :

```
$( ".selector" ).sortable({ cursor: "move" }); 
```

在初始化后设置或者获取 `cursor` 参数：

```
// getter
var cursor = $( ".selector" ).sortable( "option", "cursor" );

// setter
$( ".selector" ).sortable( "option", "cursor", "move" ); 
```

### cursorAt**Type:** [Object](http://api.jquery.com/Types/#Object)

**Default:** `false`移动排序元素或助手（helper），这样光标总是出现，以便从相同的位置进行拖拽。坐标可通过一个或两个键的组合成一个哈希给出： `{ top, left, right, bottom }`。**Code examples:**

使用指定的 `cursorAt` 参数初始化 sortable :

```
$( ".selector" ).sortable({ cursorAt: { left: 5 } }); 
```

在初始化后设置或者获取 `cursorAt` 参数：

```
// getter
var cursorAt = $( ".selector" ).sortable( "option", "cursorAt" );

// setter
$( ".selector" ).sortable( "option", "cursorAt", { left: 5 } ); 
```

### delay**Type:** [Integer](http://api.jquery.com/Types/#Integer)

**Default:** `0`在排序拖动开始多少毫秒后元素才开始移动. 这可以防止意外的点击造成元素的拖动.**Code examples:**

使用指定的 `delay` 参数初始化 sortable :

```
$( ".selector" ).sortable({ delay: 150 }); 
```

在初始化后设置或者获取 `delay` 参数：

```
// getter
var delay = $( ".selector" ).sortable( "option", "delay" );

// setter
$( ".selector" ).sortable( "option", "delay", 150 ); 
```

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为`true`，将禁用 sortable。**Code examples:**

使用指定的 `disabled` 参数初始化 sortable :

```
$( ".selector" ).sortable({ disabled: true }); 
```

在初始化后设置或者获取 `disabled` 参数：

```
// getter
var disabled = $( ".selector" ).sortable( "option", "disabled" );

// setter
$( ".selector" ).sortable( "option", "disabled", true ); 
```

### distance**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `1`设置当排序拖动开始多少个像素之后元素才开始移动.以像素计。 如果指定了该参数, 排序不会马上开始,直到鼠标移动达到了指定的像素值.**Code examples:**

使用指定的 `distance` 参数初始化 sortable :

```
$( ".selector" ).sortable({ distance: 5 }); 
```

在初始化后设置或者获取 `distance` 参数：

```
// getter
var distance = $( ".selector" ).sortable( "option", "distance" );

// setter
$( ".selector" ).sortable( "option", "distance", 5 ); 
```

### dropOnEmpty**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `true`如果为`false`，这个 sortable 中项不能拖动到一个空的 sortable 中。(查看`connectWith` 选项.**Code examples:**

使用指定的 `dropOnEmpty` 参数初始化 sortable :

```
$( ".selector" ).sortable({ dropOnEmpty: false }); 
```

在初始化后设置或者获取 `dropOnEmpty` 参数：

```
// getter
var dropOnEmpty = $( ".selector" ).sortable( "option", "dropOnEmpty" );

// setter
$( ".selector" ).sortable( "option", "dropOnEmpty", false ); 
```

### forceHelperSize**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果为`true`, 强迫辅助元素（helper）有一个尺寸大小。**Code examples:**

使用指定的 `forceHelperSize` 参数初始化 sortable :

```
$( ".selector" ).sortable({ forceHelperSize: true }); 
```

在初始化后设置或者获取 `forceHelperSize` 参数：

```
// getter
var forceHelperSize = $( ".selector" ).sortable( "option", "forceHelperSize" );

// setter
$( ".selector" ).sortable( "option", "forceHelperSize", true ); 
```

### forcePlaceholderSize**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果为`true`, 强迫占位符（placeholder）有一个尺寸大小。**Code examples:**

使用指定的 `forcePlaceholderSize` 参数初始化 sortable :

```
$( ".selector" ).sortable({ forcePlaceholderSize: true }); 
```

在初始化后设置或者获取 `forcePlaceholderSize` 参数：

```
// getter
var forcePlaceholderSize = $( ".selector" ).sortable( "option", "forcePlaceholderSize" );

// setter
$( ".selector" ).sortable( "option", "forcePlaceholderSize", true ); 
```

### grid**Type:** [Array](http://api.jquery.com/Types/#Array)

**Default:** `false`设置排序对象或者辅助对象（helper）有一个 x 和 y 边距,(单位:像素). 数组值: `[ x, y ]`。**Code examples:**

使用指定的 `grid` 参数初始化 sortable :

```
$( ".selector" ).sortable({ grid: [ 20, 10 ] }); 
```

在初始化后设置或者获取 `grid` 参数：

```
// getter
var grid = $( ".selector" ).sortable( "option", "grid" );

// setter
$( ".selector" ).sortable( "option", "grid", [ 20, 10 ] ); 
```

### handle**Type:** [Selector](http://api.jquery.com/Types/#Selector) or [Element](http://api.jquery.com/Types/#Element)

**Default:** `false`如果设定了此参数,那么拖动会在对象内指定的元素上开始.**Code examples:**

使用指定的 `handle` 参数初始化 sortable :

```
$( ".selector" ).sortable({ handle: ".handle" }); 
```

在初始化后设置或者获取 `handle` 参数：

```
// getter
var handle = $( ".selector" ).sortable( "option", "handle" );

// setter
$( ".selector" ).sortable( "option", "handle", ".handle" ); 
```

### helper**Type:** [String](http://api.jquery.com/Types/#String) or [Function](http://api.jquery.com/Types/#Function)()

**Default:** `"original"`允许使用一个辅助元素来进行拖动时展示. 所提供的函数在拖动时接受事件和对象元素, 并且需要返回一个 DOMElement 对象用来当作辅助对象.**允许使用的值：**

*   **String**:如果设置为`"clone"`，那么这个元素将被克隆，并且克隆出来的元素将被拖动。
*   **Function**: 一个函数，将返回拖拽时要使用的 DOMElement。函数接收事件，且元素正被排序。

**Code examples:**

使用指定的 `helper` 参数初始化 sortable :

```
$( ".selector" ).sortable({ helper: "clone" }); 
```

在初始化后设置或者获取 `helper` 参数：

```
// getter
var helper = $( ".selector" ).sortable( "option", "helper" );

// setter
$( ".selector" ).sortable( "option", "helper", "clone" ); 
```

### items**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `"> *"`指定元素内的哪一个项目应是 sortable。**Code examples:**

使用指定的 `items` 参数初始化 sortable :

```
$( ".selector" ).sortable({ items: "> li" }); 
```

在初始化后设置或者获取 `items` 参数：

```
// getter
var items = $( ".selector" ).sortable( "option", "items" );

// setter
$( ".selector" ).sortable( "option", "items", "> li" ); 
```

### opacity**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `false`当排序时助手（helper）的不透明度。从`0.01` 到 `1`。**Code examples:**

使用指定的 `opacity` 参数初始化 sortable :

```
$( ".selector" ).sortable({ opacity: 0.5 }); 
```

在初始化后设置或者获取 `opacity` 参数：

```
// getter
var opacity = $( ".selector" ).sortable( "option", "opacity" );

// setter
$( ".selector" ).sortable( "option", "opacity", 0.5 ); 
```

### placeholder**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `false`要应用的 class 名称，否则为白色空白。**Code examples:**

使用指定的 `placeholder` 参数初始化 sortable :

```
$( ".selector" ).sortable({ placeholder: "sortable-placeholder" }); 
```

在初始化后设置或者获取 `placeholder` 参数：

```
// getter
var placeholder = $( ".selector" ).sortable( "option", "placeholder" );

// setter
$( ".selector" ).sortable( "option", "placeholder", "sortable-placeholder" ); 
```

### revert**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Number](http://api.jquery.com/Types/#Number)

**Default:** `false`sortable 项目是否使用一个流畅的动画还原到它的新位置。**支持多个类型：**

*   **Boolean**:当设置为 `true`，该项目将会使用动画，动画使用默认的持续时间。
*   **Number**: 动画的持续时间，以毫秒计。

**Code examples:**

使用指定的 `revert` 参数初始化 sortable :

```
$( ".selector" ).sortable({ revert: true }); 
```

在初始化后设置或者获取 `revert` 参数：

```
// getter
var revert = $( ".selector" ).sortable( "option", "revert" );

// setter
$( ".selector" ).sortable( "option", "revert", true ); 
```

### scroll**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `true`如果设置为 `true`，当到达边缘时页面会滚动。**Code examples:**

使用指定的 `scroll` 参数初始化 sortable :

```
$( ".selector" ).sortable({ scroll: false }); 
```

在初始化后设置或者获取 `scroll` 参数：

```
// getter
var scroll = $( ".selector" ).sortable( "option", "scroll" );

// setter
$( ".selector" ).sortable( "option", "scroll", false ); 
```

### scrollSensitivity**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `20`定义鼠标距离边缘多少距离时开始滚动。**Code examples:**

使用指定的 `scrollSensitivity` 参数初始化 sortable :

```
$( ".selector" ).sortable({ scrollSensitivity: 10 }); 
```

在初始化后设置或者获取 `scrollSensitivity` 参数：

```
// getter
var scrollSensitivity = $( ".selector" ).sortable( "option", "scrollSensitivity" );

// setter
$( ".selector" ).sortable( "option", "scrollSensitivity", 10 ); 
```

### scrollSpeed**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `20`当鼠标指针获取到在 `scrollSensitivity` 距离内时，窗体滚动的速度。如果 scroll 选项是 false 则忽略。**Code examples:**

使用指定的 `scrollSpeed` 参数初始化 sortable :

```
$( ".selector" ).sortable({ scrollSpeed: 40 }); 
```

在初始化后设置或者获取 `scrollSpeed` 参数：

```
// getter
var scrollSpeed = $( ".selector" ).sortable( "option", "scrollSpeed" );

// setter
$( ".selector" ).sortable( "option", "scrollSpeed", 40 ); 
```

### tolerance**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"intersect"`指定用于测试项目被移动时是否覆盖在另一个项目上的模式。可能的值：

*   `"intersect"`：项目至少 50% 重叠在其他项目上。
*   `"pointer"`：鼠标指针重叠在其他项目上。

**Code examples:**

使用指定的 `tolerance` 参数初始化 sortable :

```
$( ".selector" ).sortable({ tolerance: "pointer" }); 
```

在初始化后设置或者获取 `tolerance` 参数：

```
// getter
var tolerance = $( ".selector" ).sortable( "option", "tolerance" );

// setter
$( ".selector" ).sortable( "option", "tolerance", "pointer" ); 
```

### zIndex**Type:** [Integer](http://api.jquery.com/Types/#Integer)

**Default:** `1000`当被排序时，元素/助手（helper）元素的 Z-index。**Code examples:**

使用指定的 `zIndex` 参数初始化 sortable :

```
$( ".selector" ).sortable({ zIndex: 9999 }); 
```

在初始化后设置或者获取 `zIndex` 参数：

```
// getter
var zIndex = $( ".selector" ).sortable( "option", "zIndex" );

// setter
$( ".selector" ).sortable( "option", "zIndex", 9999 ); 
```

## Methods

### cancel()

当前排序开始时，取消一个在当前 sortable 中的改变，且恢复到之前的状态。在 stop 和 receive 回调函数中非常有用。

*   该方法不接受任何参数。

**Code examples:**

调用 cancel 方法：

```
$( ".selector" ).sortable( "cancel" ); 
```

### destroy()

完全移除 sortable 功能。这会把元素返回到它的预初始化状态。

*   该方法不接受任何参数。

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).sortable( "destroy" ); 
```

### disable()

禁用 sortable。

*   该方法不接受任何参数。

**Code examples:**

调用 disable 方法：

```
$( ".selector" ).sortable( "disable" ); 
```

### enable()

启用 sortable。

*   该方法不接受任何参数。

**Code examples:**

调用 enable 方法：

```
$( ".selector" ).sortable( "enable" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取当前与指定的 `optionName` 关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项的名称。

**Code examples:**

调用该方法：

```
var isDisabled = $( ".selector" ).sortable( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含键/值对的对象，键/值对表示当前 sortable 选项哈希。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
var options = $( ".selector" ).sortable( "option" ); 
```

### option( optionName, value )

设置与指定的 `optionName` 关联的 sortable 选项的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的值。

**Code examples:**

调用该方法：

```
$( ".selector" ).sortable( "option", "disabled", true ); 
```

### option( options )

为 sortable 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的 option-value 对。

**Code examples:**

调用该方法：

```
$( ".selector" ).sortable( "option", { disabled: true } ); 
```

### refresh()

刷新 sortable 项目。触发所有 sortable 项目重新加载，导致新的项目被认可。

*   该方法不接受任何参数。

**Code examples:**

调用 refresh 方法：

```
$( ".selector" ).sortable( "refresh" ); 
```

### refreshPositions()

刷新 sortable 项目的缓存位置。调用该方法刷新所有 sortable 的已缓存的项目位置。

*   该方法不接受任何参数。

**Code examples:**

调用 refreshPositions 方法：

```
$( ".selector" ).sortable( "refreshPositions" ); 
```

### serialize( options )Returns: [String](http://api.jquery.com/Types/#String)

序列化 sortable 的项目 `id` 为一个 form/ajax 可提交的字符串。调用该方法会产生一个可被追加到任何 url 中的哈希，以便简单地把一个新的项目顺序提交回服务器。

默认情况下，它通过每个项目的 `id` 进行工作，id 格式为 `"setname_number"`，且它会产生一个形如 `"setname[]=number&setname[]=number"` 的哈希。

注释：如果序列化返回一个空的字符串，请确认 `id` 属性包含一个下划线（*）。形式必须是 `"set_number"`。例如，一个 `id` 属性为 `"foo_1"`、`"foo_5"`、`"foo_2"` 的 3 元素列表将序列化为 `"foo[]=1&foo[]=5&foo[]=2"`。您可以使用下划线（*）、等号（=）或连字符（-）来分隔集合和数字。例如，`"foo=1"`、`"foo-1"`、`"foo_1"` 所有都序列化为 `"foo[]=1"`。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要自定义序列化的选项。
    *   **key**（默认值：`属性中分隔符前面的部分`） 类型：String 描述：把 `part1[]` 替换为指定的值。
    *   **attribute**（默认值：`"id"`） 类型：String 描述：值要使用的属性名称。
    *   **expression**（默认值：`/(.+)-=_/`） 类型：RegExp 描述：用于把属性值分隔为键和值两部分的正则表达式。

**Code examples:**

调用 serialize 方法：

```
var sorted = $( ".selector" ).sortable( "serialize", { key: "sort" } ); 
```

### toArray( options )Returns: [Array](http://api.jquery.com/Types/#Array)

序列化 sortable 的项目 id 为一个字符串的数组。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要自定义序列化的选项。
    *   **attribute** (default: `"id"`)Type: [String](http://api.jquery.com/Types/#String)值要使用的属性名称。

**Code examples:**

调用 toArray 方法：

```
var sortedIDs = $( ".selector" ).sortable( "toArray" ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个包含 sortable 元素的 `jQuery` 对象。

*   该方法不接受任何参数。

**Code examples:**

调用 widget 方法：

```
var widget = $( ".selector" ).sortable( "widget" ); 
```

## Events

### activate( event, ui )Type: `sortactivate`

当使用被连接列表时触发该事件，每个被连接列表在拖拽开始时接收它。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被排序的助手（helper）。
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示当前被拖拽的元素。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前的绝对位置，表示为 `{ top, left }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前位置，表示为 `{ top, left }`.
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)元素的原始位置，表示为`{ top, left }`.
    *   **sender**Type: [jQuery](http://api.jquery.com/Types/#jQuery)如果从一个 sortable 移动到另一个 sortable，项目来自的那个
    *   **placeholder**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被作为占位符使用的元素。

**Code examples:**

使用指定的 activate 回调的 sortable：

```
$( ".selector" ).sortable({
  activate: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 sortactivate 事件：

```
$( ".selector" ).on( "sortactivate", function( event, ui ) {} ); 
```

### beforeStop( event, ui )Type: `sortbeforestop`

当排序停止时触发该事件，除了当占位符（placeholder）/助手（helper）仍然可用时。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被排序的助手（helper）。
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示当前被拖拽的元素。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前的绝对位置，表示为 `{ top, left }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前位置，表示为 `{ top, left }`.
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)元素的原始位置，表示为`{ top, left }`.
    *   **sender**Type: [jQuery](http://api.jquery.com/Types/#jQuery)如果从一个 sortable 移动到另一个 sortable，项目来自的那个
    *   **placeholder**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被作为占位符使用的元素。

**Code examples:**

使用指定的 beforeStop 回调的 sortable：

```
$( ".selector" ).sortable({
  beforeStop: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 sortbeforestop 事件：

```
$( ".selector" ).on( "sortbeforestop", function( event, ui ) {} ); 
```

### change( event, ui )Type: `sortchange`

在排序期间触发该事件，除了当 DOM 位置改变时。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被排序的助手（helper）。
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示当前被拖拽的元素。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前的绝对位置，表示为 `{ top, left }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前位置，表示为 `{ top, left }`.
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)元素的原始位置，表示为`{ top, left }`.
    *   **sender**Type: [jQuery](http://api.jquery.com/Types/#jQuery)如果从一个 sortable 移动到另一个 sortable，项目来自的那个
    *   **placeholder**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被作为占位符使用的元素。

**Code examples:**

使用指定的 change 回调的 sortable：

```
$( ".selector" ).sortable({
  change: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 sortchange 事件：

```
$( ".selector" ).on( "sortchange", function( event, ui ) {} ); 
```

### create( event, ui )Type: `sortcreate`

当 droppable 被创建时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

使用指定的 create 回调的 sortable：

```
$( ".selector" ).sortable({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 sortcreate 事件：

```
$( ".selector" ).on( "sortcreate", function( event, ui ) {} ); 
```

### deactivate( event, ui )Type: `sortdeactivate`

当排序停止时触发该事件，该事件传播到所有可能的连接列表。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被排序的助手（helper）。
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示当前被拖拽的元素。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前的绝对位置，表示为 `{ top, left }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前位置，表示为 `{ top, left }`.
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)元素的原始位置，表示为`{ top, left }`.
    *   **sender**Type: [jQuery](http://api.jquery.com/Types/#jQuery)如果从一个 sortable 移动到另一个 sortable，项目来自的那个
    *   **placeholder**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被作为占位符使用的元素。

**Code examples:**

使用指定的 deactivate 回调的 sortable：

```
$( ".selector" ).sortable({
  deactivate: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 sortdeactivate 事件：

```
$( ".selector" ).on( "sortdeactivate", function( event, ui ) {} ); 
```

### out( event, ui )Type: `sortout`

当一个 sortable 项目从一个 sortable 列表移除时触发该事件。

*Note: 当一个 sortable 项目被撤销时也会触发该事件。*

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被排序的助手（helper）。
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示当前被拖拽的元素。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前的绝对位置，表示为 `{ top, left }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前位置，表示为 `{ top, left }`.
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)元素的原始位置，表示为`{ top, left }`.
    *   **sender**Type: [jQuery](http://api.jquery.com/Types/#jQuery)如果从一个 sortable 移动到另一个 sortable，项目来自的那个
    *   **placeholder**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被作为占位符使用的元素。

**Code examples:**

使用指定的 out 回调的 sortable：

```
$( ".selector" ).sortable({
  out: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 sortout 事件：

```
$( ".selector" ).on( "sortout", function( event, ui ) {} ); 
```

### over( event, ui )Type: `sortover`

当一个 sortable 项目移动到一个 sortable 列表时触发该事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被排序的助手（helper）。
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示当前被拖拽的元素。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前的绝对位置，表示为 `{ top, left }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前位置，表示为 `{ top, left }`.
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)元素的原始位置，表示为`{ top, left }`.
    *   **sender**Type: [jQuery](http://api.jquery.com/Types/#jQuery)如果从一个 sortable 移动到另一个 sortable，项目来自的那个
    *   **placeholder**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被作为占位符使用的元素。

**Code examples:**

使用指定的 over 回调的 sortable：

```
$( ".selector" ).sortable({
  over: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 sortover 事件：

```
$( ".selector" ).on( "sortover", function( event, ui ) {} ); 
```

### receive( event, ui )Type: `sortreceive`

当来自一个连接的 sortable 列表的一个项目被放置到另一个列表时触发该事件。后者是事件目标。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被排序的助手（helper）。
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示当前被拖拽的元素。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前的绝对位置，表示为 `{ top, left }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前位置，表示为 `{ top, left }`.
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)元素的原始位置，表示为`{ top, left }`.
    *   **sender**Type: [jQuery](http://api.jquery.com/Types/#jQuery)如果从一个 sortable 移动到另一个 sortable，项目来自的那个
    *   **placeholder**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被作为占位符使用的元素。

**Code examples:**

使用指定的 receive 回调的 sortable：

```
$( ".selector" ).sortable({
  receive: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 sortreceive 事件：

```
$( ".selector" ).on( "sortreceive", function( event, ui ) {} ); 
```

### remove( event, ui )Type: `sortremove`

当来自一个连接的 sortable 列表的一个项目被放置到另一个列表时触发该事件。前者是事件目标。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被排序的助手（helper）。
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示当前被拖拽的元素。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前的绝对位置，表示为 `{ top, left }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前位置，表示为 `{ top, left }`.
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)元素的原始位置，表示为`{ top, left }`.
    *   **sender**Type: [jQuery](http://api.jquery.com/Types/#jQuery)如果从一个 sortable 移动到另一个 sortable，项目来自的那个
    *   **placeholder**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被作为占位符使用的元素。

**Code examples:**

使用指定的 remove 回调的 sortable：

```
$( ".selector" ).sortable({
  remove: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 sortremove 事件：

```
$( ".selector" ).on( "sortremove", function( event, ui ) {} ); 
```

### sort( event, ui )Type: `sort`

在排序期间触发该事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被排序的助手（helper）。
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示当前被拖拽的元素。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前的绝对位置，表示为 `{ top, left }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前位置，表示为 `{ top, left }`.
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)元素的原始位置，表示为`{ top, left }`.
    *   **sender**Type: [jQuery](http://api.jquery.com/Types/#jQuery)如果从一个 sortable 移动到另一个 sortable，项目来自的那个
    *   **placeholder**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被作为占位符使用的元素。

**Code examples:**

使用指定的 sort 回调的 sortable：

```
$( ".selector" ).sortable({
  sort: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 sort 事件：

```
$( ".selector" ).on( "sort", function( event, ui ) {} ); 
```

### start( event, ui )Type: `sortstart`

当排序开始时触发该事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被排序的助手（helper）。
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示当前被拖拽的元素。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前的绝对位置，表示为 `{ top, left }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前位置，表示为 `{ top, left }`.
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)元素的原始位置，表示为`{ top, left }`.
    *   **sender**Type: [jQuery](http://api.jquery.com/Types/#jQuery)如果从一个 sortable 移动到另一个 sortable，项目来自的那个
    *   **placeholder**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被作为占位符使用的元素。

**Code examples:**

使用指定的 start 回调的 sortable：

```
$( ".selector" ).sortable({
  start: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 sortstart 事件：

```
$( ".selector" ).on( "sortstart", function( event, ui ) {} ); 
```

### stop( event, ui )Type: `sortstop`

当排序停止时触发该事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被排序的助手（helper）。
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示当前被拖拽的元素。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前的绝对位置，表示为 `{ top, left }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前位置，表示为 `{ top, left }`.
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)元素的原始位置，表示为`{ top, left }`.
    *   **sender**Type: [jQuery](http://api.jquery.com/Types/#jQuery)如果从一个 sortable 移动到另一个 sortable，项目来自的那个
    *   **placeholder**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被作为占位符使用的元素。

**Code examples:**

使用指定的 stop 回调的 sortable：

```
$( ".selector" ).sortable({
  stop: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 sortstop 事件：

```
$( ".selector" ).on( "sortstop", function( event, ui ) {} ); 
```

### update( event, ui )Type: `sortupdate`

当用户停止排序且 DOM 位置改变时触发该事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **helper**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被排序的助手（helper）。
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示当前被拖拽的元素。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前的绝对位置，表示为 `{ top, left }`。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)助手（helper）的当前位置，表示为 `{ top, left }`.
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)元素的原始位置，表示为`{ top, left }`.
    *   **sender**Type: [jQuery](http://api.jquery.com/Types/#jQuery)如果从一个 sortable 移动到另一个 sortable，项目来自的那个
    *   **placeholder**Type: [jQuery](http://api.jquery.com/Types/#jQuery)jQuery 对象，表示被作为占位符使用的元素。

**Code examples:**

使用指定的 update 回调的 sortable：

```
$( ".selector" ).sortable({
  update: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 sortupdate 事件：

```
$( ".selector" ).on( "sortupdate", function( event, ui ) {} ); 
```

## Example:

#### A simple jQuery UI Sortable.

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>sortable demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<ul id="sortable">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
  <li>Item 4</li>
  <li>Item 5</li>
</ul>

<script>$("#sortable").sortable();</script>

</body>
</html> 
```