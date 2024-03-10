# Widgets

小部件（Widgets）是功能丰富、有状态的插件，它有一个完整的生命周期，带有方法和事件。您可以查看 部件库（Widget Factory）文档 了解更多详情。

## Accordion Widget

把一对标题和内容面板转换成折叠面板。

## Autocomplete Widget

自动完成功能根据用户输入值进行搜索和过滤，让用户快速找到并从预设值列表中选择。

## Button Widget

可主题化的按钮和按钮集合。

## Datepicker Widget

从弹出框或在线日历选择一个日期。

## Dialog Widget

在一个交互覆盖层中打开内容。

Also in: [Utilities](http://www.css88.com/jquery-ui-api/category/utilities/ "View all posts in Utilities")

## Widget Factory

使用与所有 jQuery UI 小部件相同的抽象化来创建有状态的 jQuery 插件。

Also in: [Utilities](http://www.css88.com/jquery-ui-api/category/utilities/ "View all posts in Utilities")

## Widget Plugin Bridge

jQuery.widget.bridge() 方法是 jQuery 部件库（Widget Factory）的一部分。它扮演着由 $.widget() 创建的对象和 jQuery API 之间的中介。

## Menu Widget

带有鼠标和键盘交互的用于导航的可主题化菜单。

## Progressbar Widget

显示一个确定的或不确定的进程状态。

## Slider Widget

拖动手柄可以选择一个数值。

## Spinner Widget

通过向上/向下按钮和箭头键处理，为输入数值增强文本输入功能。

## Tabs Widget

一种多面板的单内容区，每个面板与列表中的标题相关。

## Tooltip Widget

可自定义的、可主题化的工具提示框，替代原生的工具提示框。

# Accordion Widget

Categories: [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## version added: 1.0

**Description:** 使一对标题和内容面板转换成折叠面板（Accordion）。

## QuickNavExamples

### Options

*   active
*   animate
*   collapsible
*   disabled
*   event
*   header
*   heightStyle
*   icons

### Methods

*   destroy
*   disable
*   enable
*   option
*   refresh
*   widget

### Events

*   activate
*   beforeActivate
*   create

你的 accordion 容器需要按照一个元素成组的满足拥有配对的头部和内容面板的格式要求：

```
<div id="accordion">
  <h3>First header</h3>
  <div>First content panel</div>
  <h3>Second header</h3>
  <div>Second content panel</div>
</div> 
```

Accordions （折叠面板）支持任意的标记，但每个内容面板必须始终是 其相关联头部之后的下一个兄弟节点。请参阅有关如何使用自定义标记结构的`header`选项。

面板可以通过设置 `active`选项来激活。

### 键盘交互(Keyboard interaction)

当焦点在标题（header）上时，下面的键盘命令可用：

*   UP/LEFT - 移动焦点到上一个标题（header）。如果在第一个标题（header）上，则移动焦点到最后一个标题（header）上。
*   DOWN/RIGHT - 移动焦点到下一个标题（header）。如果在最后一个标题（header）上，则移动焦点到第一个标题（header）上。
*   HOME - 移动焦点到第一个标题（header）上。
*   END - 移动焦点到最后一个标题（header）上。
*   SPACE/ENTER - 激活与获得焦点的标题（header）相关的面板（panel）。

当焦点在面板（panel）中时，下面的键盘命令可用：

*   CTRL+UP: 移动焦点到相关的标题（header）。

### 主题(Theming)

折叠面板部件（Accordion Widget）使用 jQuery UI CSS 框架 来定义它的外观和感观的样式。如果需要使用折叠面板指定的样式，则可以使用下面的 CSS class 名称： ui-accordion：折叠面板的外层容器。 ui-accordion-header：折叠面板的标题。如果标题包含 icons，则标题会另外有个 ui-accordion-icons class。 ui-accordion-content：折叠面板的内容面板。

折叠面板部件（Accordion Widget）使用 jQuery UI CSS framework 框架 来定义它的外观和感观的样式。如果需要使用折叠面板指定的样式，则可以使用下面的 CSS class 名称：

*   `ui-accordion`: 折叠面板的外层容器。
    *   `ui-accordion-header`: 折叠面板的标题。如果标题包含 `icons`，则标题会另外有个 `ui-accordion-icons` class。
    *   `ui-accordion-content`: 折叠面板的内容面板。

### 依赖

*   UI 核心（UI Core）
*   部件库（Widget Factory）
*   特效核心（Effects Core） （可选的；当与 `animate`选项一起使用时）

### 其他注意事项:

*   该部件要求一些功能性的 CSS，否则将无法工作。如果您创建了一个自定义的主题，请使用小部件指定的 CSS 文件作为起点。

## 选项

### active**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Integer](http://api.jquery.com/Types/#Integer)

**Default:** `0`当前打开哪一个面板。**支持多个类型：**

*   **Boolean**:设置 `active` 为 `false` 将折叠所有的面板。这要求 `collapsible` 选项必须为 `true`。
*   **Integer**: 激活打开的面板索引，以零为基础。负值则表示从最后一个面板后退选择面板。

**Code examples:**

初始化带有指定 `active`选项的 Accordion（折叠面板）：

```
$( ".selector" ).accordion({ active: 2 }); 
```

在初始化后，获取或设置 `active` 选项：

```
// getter
var active = $( ".selector" ).accordion( "option", "active" );

// setter
$( ".selector" ).accordion( "option", "active", 2 ); 
```

### animate**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String) or [Object](http://api.jquery.com/Types/#Object)

**Default:** `{}`是否使用动画改变面板，且如何使用动画改变面板。**支持多个类型：**

*   **Boolean**:`false` 值将禁用动画。
*   **Number**: 默认 easing 动画的持续时间，以毫秒为单位。
*   **String**: 默认的持续时间要使用的 easing 动画形式 名称。
*   **Object**: `easing` 和 `duration` 属性的动画设置。
    *   上面任意的选项都可以包含 `down` 属性。
    *   当被激活的面板有一个比当前激活面板较低的指数时，发生 "Down" 动画。

**Code examples:**

初始化带有指定 `animate`选项的 Accordion（折叠面板）：

```
$( ".selector" ).accordion({ animate: "bounceslide" }); 
```

在初始化后，获取或设置 `animate` 选项：

```
// getter
var animate = $( ".selector" ).accordion( "option", "animate" );

// setter
$( ".selector" ).accordion( "option", "animate", "bounceslide" ); 
```

### collapsible**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`所有部分是否都可以马上关闭。允许折叠激活的部分。**Code examples:**

初始化带有指定 `collapsible`选项的 Accordion（折叠面板）：

```
$( ".selector" ).accordion({ collapsible: true }); 
```

在初始化后，获取或设置 `collapsible` 选项：

```
// getter
var collapsible = $( ".selector" ).accordion( "option", "collapsible" );

// setter
$( ".selector" ).accordion( "option", "collapsible", true ); 
```

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为 `true`，则禁用该 Accordion（折叠面板）。**Code examples:**

初始化带有指定 `disabled`选项的 Accordion（折叠面板）：

```
$( ".selector" ).accordion({ disabled: true }); 
```

在初始化后，获取或设置 `disabled` 选项：

```
// getter
var disabled = $( ".selector" ).accordion( "option", "disabled" );

// setter
$( ".selector" ).accordion( "option", "disabled", true ); 
```

### event**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"click"`Accordion（折叠面板） 头部会作出反应的事件，用以激活相关的面板。可以指定多个事件，用空格隔开。**Code examples:**

初始化带有指定 `event`选项的 Accordion（折叠面板）：

```
$( ".selector" ).accordion({ event: "mouseover" }); 
```

在初始化后，获取或设置 `event` 选项：

```
// getter
var event = $( ".selector" ).accordion( "option", "event" );

// setter
$( ".selector" ).accordion( "option", "event", "mouseover" ); 
```

### header**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `"> li > :first-child,> :not(li):even"`

标题元素的选择器，通过主要 accordion 元素上的 `.find()` 进行应用。内容面板必须是紧跟在与其相关的标题后的同级元素。

**Code examples:**

初始化带有指定 `header`选项的 Accordion（折叠面板）：

```
$( ".selector" ).accordion({ header: "h3" }); 
```

在初始化后，获取或设置 `header` 选项：

```
// getter
var header = $( ".selector" ).accordion( "option", "header" );

// setter
$( ".selector" ).accordion( "option", "header", "h3" ); 
```

### heightStyle**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"auto"`

控制 Accordion（折叠面板） 和每个面板的高度。可能的值：

*   `"auto"`: 所有的面板将会被设置为最高的面板的高度。
*   `"fill"`: 基于 accordion 的父元素的高度，扩展到可用的高度。
*   `"content"`: 每个面板的高度取决于它的内容。

**Code examples:**

初始化带有指定 `heightStyle`选项的 Accordion（折叠面板）：

```
$( ".selector" ).accordion({ heightStyle: "fill" }); 
```

在初始化后，获取或设置 `heightStyle` 选项：

```
// getter
var heightStyle = $( ".selector" ).accordion( "option", "heightStyle" );

// setter
$( ".selector" ).accordion( "option", "heightStyle", "fill" ); 
```

### icons**Type:** [Object](http://api.jquery.com/Types/#Object)

**Default:** `{ "header": "ui-icon-triangle-1-e", "activeHeader": "ui-icon-triangle-1-s" }`

标题要使用的图标，与 jQuery UI CSS 框架提供的图标（Icons） 匹配。设置为 false 则不显示图标。

*   header (string, 默认值： "ui-icon-triangle-1-e")
*   activeHeader (string, 默认值： "ui-icon-triangle-1-s")

**Code examples:**

初始化带有指定 `icons`选项的 Accordion（折叠面板）：

```
$( ".selector" ).accordion({ icons: { "header": "ui-icon-plus", "activeHeader": "ui-icon-minus" } }); 
```

在初始化后，获取或设置 `icons` 选项：

```
// getter
var icons = $( ".selector" ).accordion( "option", "icons" );

// setter
$( ".selector" ).accordion( "option", "icons", { "header": "ui-icon-plus", "activeHeader": "ui-icon-minus" } ); 
```

## Methods

### destroy()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

完全移除 accordion 功能。这会把元素返回到它的预初始化状态。

*   该方法不接受任何参数。

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).accordion( "destroy" ); 
```

### disable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

禁用 accordion。

*   该方法不接受任何参数。

**Code examples:**

调用 disable 方法：

```
$( ".selector" ).accordion( "disable" ); 
```

### enable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

启用 accordion。

*   该方法不接受任何参数。

**Code examples:**

调用 enable 方法：

```
$( ".selector" ).accordion( "enable" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取当前与指定的 `optionName` 关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项的名称。

**Code examples:**

调用该方法：

```
var isDisabled = $( ".selector" ).accordion( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含键/值对的对象，键/值对表示当前 accordion 选项哈希。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
var options = $( ".selector" ).accordion( "option" ); 
```

### option( optionName, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置与指定的 `optionName` 关联的 accordion 选项的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的值。

**Code examples:**

调用该方法：

```
$( ".selector" ).accordion( "option", "disabled", true ); 
```

### option( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

为 accordion 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的 option-value 对。

**Code examples:**

调用该方法：

```
$( ".selector" ).accordion( "option", { disabled: true } ); 
```

### refresh()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

处理任何在 DOM 中直接添加或移除的标题和面板，并重新计算 accordion 的高度。结果取决于内容和 `heightStyle` 选项。

*   该方法不接受任何参数。

**Code examples:**

调用 refresh 方法：

```
$( ".selector" ).accordion( "refresh" ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个包含 accordion 的 `jQuery` 对象。

*   该方法不接受任何参数。

**Code examples:**

调用 widget 方法：

```
var widget = $( ".selector" ).accordion( "widget" ); 
```

## Events

### activate( event, ui )Type: `accordionactivate`

面板被激活后触发（在动画完成之后）。如果 accordion 之前是折叠的，则 `ui.oldHeader` 和 `ui.oldPanel` 将是空的 jQuery 对象。如果 accordion 正在折叠，则 `ui.newHeader` 和 `ui.newPanel` 将是空的 jQuery 对象。

**注意：** 由于 `activate` 事件只有在面板激活时才能触发，当创建 accordion 部件时，最初的面板不会触发该事件。如果您需要一个用于部件创建的钩，请使用 `create` 事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **newHeader**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚被激活的标题。
    *   **oldHeader**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚被取消激活的标题。
    *   **newPanel**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚被激活的面板。
    *   **oldPanel**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚被取消激活的面板。

**Code examples:**

初始化带有指定 activate 回调的 accordion：

```
$( ".selector" ).accordion({
  activate: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 accordionactivate 事件:

```
$( ".selector" ).on( "accordionactivate", function( event, ui ) {} ); 
```

### beforeActivate( event, ui )Type: `accordionbeforeactivate`

面板被激活前直接触发。可以取消以防止面板被激活。如果 accordion 当前是折叠的，则 `ui.oldHeader` 和 `ui.oldPanel` 将是空的 jQuery 对象。如果 accordion 正在折叠，则 `ui.newHeader` 和 `ui.newPanel` 将是空的 jQuery 对象。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **newHeader**Type: [jQuery](http://api.jquery.com/Types/#jQuery)将被激活的标题。
    *   **oldHeader**Type: [jQuery](http://api.jquery.com/Types/#jQuery)将被取消激活的标题。
    *   **newPanel**Type: [jQuery](http://api.jquery.com/Types/#jQuery)将被激活的面板。
    *   **oldPanel**Type: [jQuery](http://api.jquery.com/Types/#jQuery)将被取消激活的面板。

**Code examples:**

初始化带有指定 beforeActivate 回调的 accordion：

```
$( ".selector" ).accordion({
  beforeActivate: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 accordionbeforeactivate 事件:

```
$( ".selector" ).on( "accordionbeforeactivate", function( event, ui ) {} ); 
```

### create( event, ui )Type: `accordioncreate`

当创建 accordion 时触发。如果 accordion 是折叠的，`ui.header` 和 `ui.panel` 将是空的 jQuery 对象。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **header**Type: [jQuery](http://api.jquery.com/Types/#jQuery)激活的标题。
    *   **panel**Type: [jQuery](http://api.jquery.com/Types/#jQuery)激活的面板。

**Code examples:**

初始化带有指定 create 回调的 accordion：

```
$( ".selector" ).accordion({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 accordioncreate 事件:

```
$( ".selector" ).on( "accordioncreate", function( event, ui ) {} ); 
```

## Example:

#### 一个简单的 jQuery UI 折叠面板（Accordion）。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>accordion demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<div id="accordion">
  <h3>Section 1</h3>
  <div>
    <p>Mauris mauris ante, blandit et, ultrices a, suscipit eget.
    Integer ut neque. Vivamus nisi metus, molestie vel, gravida in,
    condimentum sit amet, nunc. Nam a nibh. Donec suscipit eros.
    Nam mi. Proin viverra leo ut odio.</p>
  </div>
  <h3>Section 2</h3>
  <div>
    <p>Sed non urna. Phasellus eu ligula. Vestibulum sit amet purus.
    Vivamus hendrerit, dolor aliquet laoreet, mauris turpis velit,
    faucibus interdum tellus libero ac justo.</p>
  </div>
  <h3>Section 3</h3>
  <div>
    <p>Nam enim risus, molestie et, porta ac, aliquam ac, risus.
    Quisque lobortis.Phasellus pellentesque purus in massa.</p>
    <ul>
      <li>List item one</li>
      <li>List item two</li>
      <li>List item three</li>
    </ul>
  </div>
</div>

<script>
$( "#accordion" ).accordion();
</script>

</body>
</html> 
```

# Autocomplete Widget

Categories: [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## version added: 1.8

**Description:** 自动完成功能根据用户输入值进行搜索和过滤，让用户快速找到并从预设值列表中选择。

## QuickNavExamples

### Options

*   appendTo
*   autoFocus
*   delay
*   disabled
*   minLength
*   position
*   source

### Methods

*   close
*   destroy
*   disable
*   enable
*   option
*   search
*   widget

### Extension Points

*   _renderItem
*   _renderMenu
*   _resizeMenu

### Events

*   change
*   close
*   create
*   focus
*   open
*   response
*   search
*   select

任何可以接收输入的字段都可以转换为 Autocomplete，即，`&lt;input&gt;` 元素，`&lt;textarea&gt;` 元素及带有 `contenteditable` 属性的元素。

通过给 Autocomplete 字段焦点或者在其中输入字符，插件开始搜索匹配的条目并显示供选择的值的列表。通过输入更多的字符，用户可以过滤列表以获得更好的匹配。

该部件可用于选择先前选定的值，比如输入文章标签或者输入从地址簿中输入地址邮件地址。Autocomplete 也可以用来填充相关的信息，比如输入一个城市的名称来获得该城市的邮政编码。

您可以从本地源或者远程源获取数据：本地源适用于小数据集，例如，带有 50 个条目的地址簿；远程源适用于大数据集，比如，带有数百个或者成千上万个条目的数据库。如需了解更多有关自定义数据源的信息，请查看 `source` 选项的文档。

### 键盘交互(Keyboard interaction)

当菜单打开时，下面的键盘命令可用：

*   UP - 移动焦点到上一个项目。如果在第一个项目上，则移动焦点到输入（input）。如果在输入（input）上，则移动焦点到最后一个项目。
*   DOWN - 移动焦点到下一个项目。如果在最后一个项目上，则移动焦点到输入（input）。如果在输入（input）上，则移动焦点到第一个项目。
*   ESCAPE - 关闭菜单。
*   ENTER - 选择当前获得焦点的项目，并关闭菜单。
*   TAB - 选择当前获得焦点的项目，关闭菜单，并移动焦点到下一个可聚焦（focusable）的元素。
*   PAGE UP/DOWN - 滚动一屏的项目（基于菜单的高度）。

当菜单关闭时，下面的键盘命令可用：

*   UP/DOWN - 如果满足 `minLength`，则打开菜单。

### 主题(Theming)

自动完成部件（Autocomplete Widget）使用 jQuery UI CSS 框架 来定义它的外观和感观的样式。如果需要使用自动完成部件指定的样式，则可以使用下面的 CSS class 名称：

*   `ui-autocomplete`：用于显示匹配用户的 菜单（menu）
*   `ui-autocomplete-input`：自动完成部件（Autocomplete Widget）实例化的 input 元素。

### 依赖(Dependencies)

*   UI 核心（UI Core）
*   部件库（Widget Factory）
*   定位（Position）
*   菜单部件（Menu Widget）

### 其他注意事项:

*   该部件要求一些功能性的 CSS，否则将无法工作。如果您创建了一个自定义的主题，请使用小部件指定的 CSS 文件作为起点。
*   该部件以编程方式操作元素的值，因此当元素的值改变时不会触发原生的 `change` 事件。

## 选项

### appendTo**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `null`

菜单应该被附加到哪一个元素。当该值为 `null` 时，输入域的父元素将检查 `ui-front` class。如果找到带有 `ui-front` class 的元素，菜单将被附加到该元素。如果未找到带有 `ui-front` class 的元素，不管值为多少，菜单将被附加到 body。

**注意:** 当建议菜单打开时，`appendTo` 选项不应改变。**Code examples:**

初始化带有指定 `appendTo` 选项的 autocomplete：

```
$( ".selector" ).autocomplete({ appendTo: "#someElem" }); 
```

在初始化后，获取或设置 `appendTo` 选项：

```
// getter
var appendTo = $( ".selector" ).autocomplete( "option", "appendTo" );

// setter
$( ".selector" ).autocomplete( "option", "appendTo", "#someElem" ); 
```

### autoFocus**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为 `true`，当菜单显示时，第一个条目将自动获得焦点。**Code examples:**

初始化带有指定 `autoFocus` 选项的 autocomplete：

```
$( ".selector" ).autocomplete({ autoFocus: true }); 
```

在初始化后，获取或设置 `autoFocus` 选项：

```
// getter
var autoFocus = $( ".selector" ).autocomplete( "option", "autoFocus" );

// setter
$( ".selector" ).autocomplete( "option", "autoFocus", true ); 
```

### delay**Type:** [Integer](http://api.jquery.com/Types/#Integer)

**Default:** `300`按键和执行搜索之间的延迟，以毫秒计。对于本地数据，采用零延迟是有意义的（更具响应性），但对于远程数据会产生大量的负荷，同时降低了响应性。**Code examples:**

初始化带有指定 `delay` 选项的 autocomplete：

```
$( ".selector" ).autocomplete({ delay: 500 }); 
```

在初始化后，获取或设置 `delay` 选项：

```
// getter
var delay = $( ".selector" ).autocomplete( "option", "delay" );

// setter
$( ".selector" ).autocomplete( "option", "delay", 500 ); 
```

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为 `true`，则禁用该 autocomplete。**Code examples:**

初始化带有指定 `disabled` 选项的 autocomplete：

```
$( ".selector" ).autocomplete({ disabled: true }); 
```

在初始化后，获取或设置 `disabled` 选项：

```
// getter
var disabled = $( ".selector" ).autocomplete( "option", "disabled" );

// setter
$( ".selector" ).autocomplete( "option", "disabled", true ); 
```

### minLength**Type:** [Integer](http://api.jquery.com/Types/#Integer)

**Default:** `1`执行搜索前用户必须输入的最小字符数。对于仅带有几项条目的本地数据，通常设置为零，但是当单个字符搜索会匹配几千项条目时，设置个高数值是很有必要的。**Code examples:**

初始化带有指定 `minLength` 选项的 autocomplete：

```
$( ".selector" ).autocomplete({ minLength: 0 }); 
```

在初始化后，获取或设置 `minLength` 选项：

```
// getter
var minLength = $( ".selector" ).autocomplete( "option", "minLength" );

// setter
$( ".selector" ).autocomplete( "option", "minLength", 0 ); 
```

### position**Type:** [Object](http://api.jquery.com/Types/#Object)

**Default:** `{ my: "left top", at: "left bottom", collision: "none" }`标识建议菜单的位置与相关的 input 元素有关系。`of` 选项默认为 input 元素，但是您可以指定另一个定位元素。如需了解各种选项的更多细节，请查看 jQuery UI Position。**Code examples:**

初始化带有指定 `position` 选项的 autocomplete：

```
$( ".selector" ).autocomplete({ position: { my : "right top", at: "right bottom" } }); 
```

在初始化后，获取或设置 `position` 选项：

```
// getter
var position = $( ".selector" ).autocomplete( "option", "position" );

// setter
$( ".selector" ).autocomplete( "option", "position", { my : "right top", at: "right bottom" } ); 
```

### source**Type:** [Array](http://api.jquery.com/Types/#Array) or [String](http://api.jquery.com/Types/#String) or [Function](http://api.jquery.com/Types/#Function)( [Object](http://api.jquery.com/Types/#Object) request, [Function](http://api.jquery.com/Types/#Function) response( [Object](http://api.jquery.com/Types/#Object) data ) )

**Default:** `none`; 必须指定定义要使用的数据，必须指定。

独立于您要使用的变量，标签总是被视为文本。如果您想要标签被视为 html，您可以使用 [Scott González' html 扩展](https://github.com/scottgonzalez/jquery-ui-extensions/blob/master/src/autocomplete/jquery.ui.autocomplete.html.js) 。演示侧重于 `source` 选项的不同变量 - 您可以查找其中匹配您的使用情况的那个，并查看相关代码。

**支持多个类型：**

*   **Array**：可用于本地数据的一个数组。支持两种格式：
    *   字符串数组：`[ "Choice1", "Choice2" ]`
    *   带有 `label` 和 `value` 属性的对象数组：`[ { label: "Choice1", value: "value1" }, ... ]`label 属性显示在建议菜单中。当用户选择一个条目时，value 将被插入到 input 元素中。如果只是指定了一个属性，则该属性将被视为 label 和 value，例如，如果您只提供了 `value` 属性，value 也会被视为标签。
*   **String**：当使用一个字符串，Autocomplete 插件希望该字符串指向一个能返回 JSON 数据的 URL 资源。它可以是在相同的主机上，也可以是在不同的主机上（必须提供 JSONP）。Autocomplete 插件不过滤结果，而是通过一个 `term` 字段添加了一个查询字符串，用于服务器端脚本过滤结果。例如，如果 `source` 选项设置为 `"http://example.com"`，且用户键入了 `foo`，GET 请求则为 `http://example.com?term=foo`。数据本身的格式可以与前面描述的本地数据的格式相同。
*   **Function**：第三个变量，一个回调函数，提供最大的灵活性，可用于连接任何数据源到 Autocomplete。回调函数接受两个参数：

    *   一个 `request` 对象，带有一个 `term` 属性，表示当前文本输入中的值。例如，如果用户在 city 字段输入 `"new yo"`，则 Autocomplete term 等同于 `"new yo"`。
    *   一个 `response` 回调函数，提供单个参数：建议给用户的数据。该数据应基于被提供的 term 进行过滤，且可以是上面描述的本地数据的任何格式。用于在请求期间提供自定义 source 回调来处理错误。即使遇到错误，您也必须调用 `response` 回调函数。这就确保了小部件总是正确的状态。

    当过滤本地数据时，您可以使用内置的 `$.ui.autocomplete.escapeRegex` 函数。它会接受一个字符串参数，转义所有的正则表达式字符，让结果安全地传递到 `new RegExp()`。

**Code examples:**

初始化带有指定 `source` 选项的 autocomplete：

```
$( ".selector" ).autocomplete({ source: [ "c++", "java", "php", "coldfusion", "javascript", "asp", "ruby" ] }); 
```

在初始化后，获取或设置 `source` 选项：

```
// getter
var source = $( ".selector" ).autocomplete( "option", "source" );

// setter
$( ".selector" ).autocomplete( "option", "source", [ "c++", "java", "php", "coldfusion", "javascript", "asp", "ruby" ] ); 
```

## Methods

### close()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

关闭 Autocomplete 菜单。当与 `search` 方法结合使用时，可用于关闭打开的菜单。

*   该方法不接受任何参数。

**Code examples:**

调用 close 方法：

```
$( ".selector" ).autocomplete( "close" ); 
```

### destroy()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

完全移除 autocomplete 功能。这会把元素返回到它的预初始化状态。

*   该方法不接受任何参数。

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).autocomplete( "destroy" ); 
```

### disable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

禁用 autocomplete。

*   该方法不接受任何参数。

**Code examples:**

调用 disable 方法：

```
$( ".selector" ).autocomplete( "disable" ); 
```

### enable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

启用 autocomplete。

*   该方法不接受任何参数。

**Code examples:**

调用 enable 方法：

```
$( ".selector" ).autocomplete( "enable" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取当前与指定的 `optionName` 关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项的名称。

**Code examples:**

调用该方法：

```
var isDisabled = $( ".selector" ).autocomplete( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含键/值对的对象，键/值对表示当前 autocomplete 选项哈希。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
var options = $( ".selector" ).autocomplete( "option" ); 
```

### option( optionName, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置与指定的 `optionName` 关联的 autocomplete 选项的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的值。

**Code examples:**

调用该方法：

```
$( ".selector" ).autocomplete( "option", "disabled", true ); 
```

### option( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

为 autocomplete 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的 option-value 对。

**Code examples:**

调用该方法：

```
$( ".selector" ).autocomplete( "option", { disabled: true } ); 
```

### search( [value ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

触发 `search` 事件，如果该事件未被取消则调用数据源。当被点击时，可被类似选择框按钮用来打开建议。当不带参数调用该方法时，则使用当前输入的值。可带一个空字符串和 `minLength: 0` 进行调用，来显示所有的条目。

*   **value**Type: [String](http://api.jquery.com/Types/#String)

**Code examples:**

调用 search 方法：

```
$( ".selector" ).autocomplete( "search", "" ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个包含菜单元素的 `jQuery` 对象。虽然菜单项不断地被创建和销毁。菜单元素本身会在初始化时创建，并不断的重复使用。

*   该方法不接受任何参数。

**Code examples:**

调用 widget 方法：

```
$( ".selector" ).autocomplete( "widget" ); 
```

## Extension Points

自动完成部件（Autocomplete Widget）通过 [部件库（Widget Factory）](http://www.css88.com/jquery-ui-api/jQuery.widget/) 创建的，且可被扩展。当对部件进行扩展时，您可以重载或者添加扩展部件的行为。下面提供的方法作为扩展点，与上面列出的 插件方法 具有相同的 API 稳定性。如需了解更多有关小部件扩展的知识，请查看 [通过部件库（Widget Factory）扩展小部件](http://learn.jquery.com/jquery-ui/widget-factory/extending-widgets/)。

### _renderItem( ul, item )Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

控制在部件菜单中每个选项的创建的格式化方法 该方法必须创建一个新的`&lt;li&gt;`元素，追加到菜单中，并返回它。

*注意: 为了与 menu 小部件兼容，这时创建的`&lt;ul&gt;`元素必须包含一个`&lt;a&gt;`元素。 请看下面的例子。*

*   **ul**Type: [jQuery](http://api.jquery.com/Types/#jQuery)新创建的 `&lt;li&gt;` 元素必须追加到的 `&lt;ul&gt;` 元素。
*   **item**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **label**Type: [String](http://api.jquery.com/Types/#String)条目显示的字符串。
    *   **value**Type: [String](http://api.jquery.com/Types/#String)当条目被选中时插入到输入框中的值。

**Code examples:**

添加条目的值作为 `&lt;li&gt;` 上的 data 属性。

```
_renderItem: function( ul, item ) {
  return $( "<li>" )
    .attr( "data-value", item.value )
    .append( $( "<a>" ).text( item.label ) )
    .appendTo( ul );
} 
```

### _renderMenu( ul, items )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

控制建立部件菜单的方法。该方法传递一个空`<ul>`和匹配用户输入的术语的项目数组。 创建当个的`<li>`元素应该委派给`_renderItemData()`。

*   **ul**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个要作为小部件的菜单使用的空的 `&lt;ul&gt;`元素。
*   **items**Type: [Array](http://api.jquery.com/Types/#Array)一个数组，数组元素为匹配用户输入的条目。每个条目是一个带有 `label` 和 `value` 属性的对象。

**Code examples:**

添加一个 CSS class 名称到旧的菜单项。

```
_renderMenu: function( ul, items ) {
  var that = this;
  $.each( items, function( index, item ) {
    that._renderItemData( ul, item );
  });
  $( ul ).find( "li:odd" ).addClass( "odd" );
} 
```

thod-_resizeMenu">

### _resizeMenu()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

该方法负责在菜单显示前调整菜单尺寸。菜单元素可通过 `this.menu.element` 使用。

*   该方法不接受任何参数。

**Code examples:**

菜单总是显示为 500 像素宽。

```
_resizeMenu: function() {
  this.menu.element.outerWidth( 500 );
} 
```

ction id="events">

## Events

### change( event, ui )Type: `autocompletechange`

如果输入域的值改变则触发该事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **item**Type: [Object](http://api.jquery.com/Types/#Object)从菜单中选择的条目，否则属性为 `null`。

**Code examples:**

初始化带有指定 change 回调的 autocomplete：

```
$( ".selector" ).autocomplete({
  change: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 autocompletechange 事件：

```
$( ".selector" ).on( "autocompletechange", function( event, ui ) {} ); 
```

### close( event, ui )Type: `autocompleteclose`

当菜单隐藏时触发。不是每一个 `close` 事件都伴随着 `change` 事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 close 回调的 autocomplete：

```
$( ".selector" ).autocomplete({
  close: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 autocompleteclose 事件：

```
$( ".selector" ).on( "autocompleteclose", function( event, ui ) {} ); 
```

### create( event, ui )Type: `autocompletecreate`

当创建 autocomplete 时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 create 回调的 autocomplete：

```
$( ".selector" ).autocomplete({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 autocompletecreate 事件：

```
$( ".selector" ).on( "autocompletecreate", function( event, ui ) {} ); 
```

### focus( event, ui )Type: `autocompletefocus`

当焦点移动到一个条目上（未选择）时触发。默认的动作是把文本域中的值替换为获得焦点的条目的值，即使该事件是通过键盘交互触发的。

取消该事件会阻止值被更新，但不会阻止菜单项获得焦点。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **item**Type: [Object](http://api.jquery.com/Types/#Object)获得焦点的条目。

**Code examples:**

初始化带有指定 focus 回调的 autocomplete：

```
$( ".selector" ).autocomplete({
  focus: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 autocompletefocus 事件：

```
$( ".selector" ).on( "autocompletefocus", function( event, ui ) {} ); 
```

### open( event, ui )Type: `autocompleteopen`

当打开建议菜单或者更新建议菜单时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 open 回调的 autocomplete：

```
$( ".selector" ).autocomplete({
  open: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 autocompleteopen 事件：

```
$( ".selector" ).on( "autocompleteopen", function( event, ui ) {} ); 
```

### response( event, ui )Type: `autocompleteresponse`

在搜索完成后菜单显示前触发。用于建议数据的本地操作，其中自定义的 `source` 选项回调不是必需的。该事件总是在搜索完成时触发，如果搜索无结果或者禁用了 Autocomplete，导致菜单未显示，该事件一样会被触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **content**Type: [Array](http://api.jquery.com/Types/#Array)包含响应数据，且可被修改来改变显示结果。该数据已经标准化，所以如果您要修改数据，请确保每个条目都包含 `value` 和 `label` 属性。

**Code examples:**

初始化带有指定 response 回调的 autocomplete：

```
$( ".selector" ).autocomplete({
  response: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 autocompleteresponse 事件：

```
$( ".selector" ).on( "autocompleteresponse", function( event, ui ) {} ); 
```

### search( event, ui )Type: `autocompletesearch`

在搜索执行前满足`minLength` 和 `delay` 后触发。如果取消该事件，则不会提交请求，也不会提供建议条目。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 search 回调的 autocomplete：

```
$( ".selector" ).autocomplete({
  search: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 autocompletesearch 事件：

```
$( ".selector" ).on( "autocompletesearch", function( event, ui ) {} ); 
```

### select( event, ui )Type: `autocompleteselect`

当从菜单中选择条目时触发。默认的动作是把文本域中的值替换为被选中的条目的值。

取消该事件会阻止值被更新，但不会阻止菜单关闭。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **item**Type: [Object](http://api.jquery.com/Types/#Object)An Object with `label` and `value` properties for the selected option.

**Code examples:**

初始化带有指定 select 回调的 autocomplete：

```
$( ".selector" ).autocomplete({
  select: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 autocompleteselect 事件：

```
$( ".selector" ).on( "autocompleteselect", function( event, ui ) {} ); 
```

## Examples:

#### Example: 一个简单的 jQuery UI 自动完成（Autocomplete）。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>autocomplete demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<label for="autocomplete">Select a programming language: </label>
<input id="autocomplete">

<script>
$( "#autocomplete" ).autocomplete({
  source: [ "c++", "java", "php", "coldfusion", "javascript", "asp", "ruby" ]
});
</script>

</body>
</html> 
```

#### Example: Using a custom source callback to match only the beginning of terms

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>autocomplete demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<label for="autocomplete">Select a programming language: </label>
<input id="autocomplete">

<script>
var tags = [ "c++", "java", "php", "coldfusion", "javascript", "asp", "ruby" ];
$( "#autocomplete" ).autocomplete({
  source: function( request, response ) {
          var matcher = new RegExp( "^" + $.ui.autocomplete.escapeRegex( request.term ), "i" );
          response( $.grep( tags, function( item ){
              return matcher.test( item );
          }) );
      }
});
</script>

</body>
</html> 
```

# Button Widget

Categories: [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## version added: 1.8

**Description:** 可主题化的按钮和按钮集合。

## QuickNavExamples

### Options

*   disabled
*   icons
*   label
*   text

### Methods

*   destroy
*   disable
*   enable
*   option
*   refresh
*   widget

### Events

*   create

按钮部件（Button Widget）加强了标准表单元素的功能，比如按钮（button）、输入（input）、锚（anchor），用适当的悬停（hover）和激活（active）样式来主题化按钮。

除了基本的按钮，单选按钮和复选框（input 类型为 radio 和 checkbox）也可以转换为按钮。相关的标签（label）设计成按钮的样式，点击时更新底层的输入。为了能正常工作，需要给 input 一个 `id` 属性，并指向标签（label）的 `for` 属性。不要把 input 放在标签（label）内，否则会引起可访问性问题。

为了分组单选按钮，Button 也提供了一个额外的小部件，名为 Buttonset。Buttonset 通过选择一个容器元素（包含单选按钮）并调用 `.buttonset()` 来使用。Buttonset 也提供了可视化分组，因此当有一组按钮时都可考虑使用它。它会选择所有的后代，并对它们应用 `.button()`。您可以启用和禁用一个按钮集，这将会启用和禁用所有包含的按钮。销毁按钮集会调用每个按钮的 `destroy` 方法。对于分组的单选按钮和复选框按钮，推荐使用带有 `legend` 的 `fieldset` 来提供一个可访问的分组标签。

当使用一个类型为 button、submit 或 reset 的 input 时，仅限于支持纯文本无图标标签。

### 主题

按钮部件（Button Widget）使用 jQuery UI CSS 框架 来定义它的外观和感观的样式。如果需要使用按钮指定的样式，则可以使用下面的 CSS class 名称：

*   `ui-button`：表示按钮的 DOM 元素。该元素会根据 text 和 icons 选项添加下列 class 之一：`ui-button-text-only`、`ui-button-icon-only`、`ui-button-icons-only`、`ui-button-text-icons`。
    *   `ui-button-icon-primary`：用于显示按钮主要图标的元素。只有当主要图标在 icons 选项中提供时才呈现。
    *   `ui-button-text`：在按钮的文本内容周围的容器。
    *   `ui-button-icon-secondary`：用于显示按钮的次要图标。只有当次要图标在 icons 选项中提供时才呈现。
*   `ui-buttonset`：Buttonset 的外层容器。

### 依赖

*   UI 核心（UI Core）
*   部件库（Widget Factory）

### 其他注意事项：

*   该部件要求一些功能性的 CSS，否则将无法工作。如果您创建了一个自定义的主题，请使用小部件指定的 CSS 文件作为起点。

## Options

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为 `true`，则禁用该 button。**Code examples:**

初始化带有指定 `disabled` 选项的 button：

```
$( ".selector" ).button({ disabled: true }); 
```

在初始化后，获取或设置`disabled` 选项：

```
// getter
var disabled = $( ".selector" ).button( "option", "disabled" );

// setter
$( ".selector" ).button( "option", "disabled", true ); 
```

### icons**Type:** [Object](http://api.jquery.com/Types/#Object)

**Default:** `{ primary: null, secondary: null }`

要显示的图标，包括带有文本的图标和不带有文本的图标（查看 `text` 选项）。默认情况下 ，主图标显示在标签文本的左边，副图标显示在右边。显示位置可通过 CSS 进行控制。

`primary` 和 `secondary` 属性值必须是 图标 class 名称，例如，`"ui-icon-gear"`。如果只使用一个图标，则 `icons: { primary: "ui-icon-locked" }`。如果使用两个图标，则 `icons: { primary: "ui-icon-gear", secondary: "ui-icon-triangle-1-s" }`。

**Code examples:**

初始化带有指定 `icons` 选项的 button：

```
$( ".selector" ).button({ icons: { primary: "ui-icon-gear", secondary: "ui-icon-triangle-1-s" } }); 
```

在初始化后，获取或设置`icons` 选项：

```
// getter
var icons = $( ".selector" ).button( "option", "icons" );

// setter
$( ".selector" ).button( "option", "icons", { primary: "ui-icon-gear", secondary: "ui-icon-triangle-1-s" } ); 
```

### label**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `null`要显示在按钮中的文本。当未指定时（`null`），则使用元素的 HTML 内容，或者如果元素是一个 submit 或 reset 类型的 input 元素，则使用它的 `value` 属性，或者如果元素是一个 radio 或 checkbox 类型的 input 元素，则使用相关的 label 元素的 HTML 内容。**Code examples:**

初始化带有指定 `label` 选项的 button：

```
$( ".selector" ).button({ label: "custom label" }); 
```

在初始化后，获取或设置`label` 选项：

```
// getter
var label = $( ".selector" ).button( "option", "label" );

// setter
$( ".selector" ).button( "option", "label", "custom label" ); 
```

### text**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `true`是否显示标签。当设置为 `false` 时，不显示文本，但是此时必须启用 `icons` 选项，否则 `text` 选项将被忽略。**Code examples:**

初始化带有指定 `text` 选项的 button：

```
$( ".selector" ).button({ text: false }); 
```

在初始化后，获取或设置`text` 选项：

```
// getter
var text = $( ".selector" ).button( "option", "text" );

// setter
$( ".selector" ).button( "option", "text", false ); 
```

## Methods

### destroy()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

完全移除 button 功能。这会把元素返回到它的预初始化状态。

*   该方法不接受任何参数。

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).button( "destroy" ); 
```

### disable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

禁用 button。

*   该方法不接受任何参数。

**Code examples:**

调用 disable 方法：

```
$( ".selector" ).button( "disable" ); 
```

### enable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

启用 button。

*   该方法不接受任何参数。

**Code examples:**

调用 enable 方法：

```
$( ".selector" ).button( "enable" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取当前与指定的 `optionName` 关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项的名称。

**Code examples:**

调用该方法：

```
var isDisabled = $( ".selector" ).button( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含键/值对的对象，键/值对表示当前 button 选项哈希。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
var options = $( ".selector" ).button( "option" ); 
```

### option( optionName, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置与指定的 `optionName` 关联的 button 选项的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的值。

**Code examples:**

调用该方法：

```
$( ".selector" ).button( "option", "disabled", true ); 
```

### option( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

为 button 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的 option-value 对。

**Code examples:**

调用该方法：

```
$( ".selector" ).button( "option", { disabled: true } ); 
```

### refresh()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

刷新按钮的视觉状态。用于在以编程方式改变原生元素的选中状态或禁用状态后更新按钮状态。

*   该方法不接受任何参数。

**Code examples:**

调用 refresh 方法：

```
$( ".selector" ).button( "refresh" ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个包含 button 的 `jQuery` 对象。

*   该方法不接受任何参数。

**Code examples:**

调用 widget 方法：

```
var widget = $( ".selector" ).button( "widget" ); 
```

## Events

### create( event, ui )Type: `buttoncreate`

当创建按钮 button 时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 create 回调的 button

```
$( ".selector" ).button({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 buttoncreate 事件：

```
$( ".selector" ).on( "buttoncreate", function( event, ui ) {} ); 
```

## Examples:

#### Example: 一个简单的 jQuery UI 按钮（Button）。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>button demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<button>Button label</button>

<script>
$( "button" ).button();
</script>

</body>
</html> 
```

#### Example: 一个简单的 jQuery UI 按钮集（Buttonset）。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>button demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<form>
  <fieldset>
    <legend>Favorite jQuery Project</legend>
    <div id="radio">
      <input type="radio" id="sizzle" name="project">
      <label for="sizzle">Sizzle</label>

      <input type="radio" id="qunit" name="project" checked="checked">
      <label for="qunit">QUnit</label>

      <input type="radio" id="color" name="project">
      <label for="color">Color</label>
    </div>
  </fieldset>
</form>

<script>
$( "#radio" ).buttonset();
</script>

</body>
</html> 
```

# Datepicker Widget

Categories: [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## version added: 1.0

**Description:** 从弹出框或内联日历选择一个日期。

## QuickNavExamples

### Options

*   altField
*   altFormat
*   appendText
*   autoSize
*   beforeShow
*   beforeShowDay
*   buttonImage
*   buttonImageOnly
*   buttonText
*   calculateWeek
*   changeMonth
*   changeYear
*   closeText
*   constrainInput
*   currentText
*   dateFormat
*   dayNames
*   dayNamesMin
*   dayNamesShort
*   defaultDate
*   duration
*   firstDay
*   gotoCurrent
*   hideIfNoPrevNext
*   isRTL
*   maxDate
*   minDate
*   monthNames
*   monthNamesShort
*   navigationAsDateFormat
*   nextText
*   numberOfMonths
*   onChangeMonthYear
*   onClose
*   onSelect
*   prevText
*   selectOtherMonths
*   shortYearCutoff
*   showAnim
*   showButtonPanel
*   showCurrentAtPos
*   showMonthAfterYear
*   showOn
*   showOptions
*   showOtherMonths
*   showWeek
*   stepMonths
*   weekHeader
*   yearRange
*   yearSuffix

### Methods

*   destroy
*   dialog
*   getDate
*   hide
*   isDisabled
*   option
*   refresh
*   setDate
*   show
*   widget

### Events

jQuery UI 日期选择器（Datepicker）是向页面添加日期选择功能的高度可配置插件。您可以自定义日期格式和语言，限制可选择的日期范围，添加按钮和其他导航选项。

默认情况下，当相关的文本域获得焦点时，在一个小的覆盖层打开日期选择器。对于一个内联的日历，只需简单地将日期选择器附加到 div 或者 span 上。

### 键盘交互

当日期选择器打开时，下面的键盘命令可用：

*   PAGE UP：移到上一个月。
*   PAGE DOWN：移到下一个月。
*   CTRL+PAGE UP：移到上一年。
*   CTRL+PAGE DOWN：移到下一年。
*   CTRL+HOME：移到当前月份。如果日期选择器是关闭的则打开。
*   CTRL+LEFT：移到上一天。
*   CTRL+RIGHT：移到下一天。
*   CTRL+UP：移到上一周。
*   CTRL+DOWN：移到下一周。
*   ENTER：选择聚焦的日期。
*   CTRL+END：关闭日期选择器，并清除日期。
*   ESCAPE：关闭日期选择器，不做任何选择。

### 实用功能

#### $.datepicker.setDefaults( settings )

为所有的日期选择器改变默认设置。

使用 `option()` 方法来改变个别实例的设置。

**Code examples:**

设置所有的日期选择器在获得焦点时或点击图标时打开。

```
$.datepicker.setDefaults({
  showOn: "both",
  buttonImageOnly: true,
  buttonImage: "calendar.gif",
  buttonText: "Calendar"
}); 
```

设置所有的日期选择器都有法语文本。

```
$.datepicker.setDefaults( $.datepicker.regional[ "fr" ] ); 
```

#### $.datepicker.formatDate( format, date, settings )

格式化日期为一个带有指定格式的字符串值。

格式可以是下列组合：

*   d - 一月中的第几天（没有前导零）
*   dd - 一月中的第几天（两位数）
*   o - 一年中的第几天（没有前导零）
*   oo - 一年中的第几天（三位数）
*   D - 天的短名称
*   DD - 天的长名称
*   m - 一年中的第几月（没有前导零）
*   mm - 一年中的第几月（两位数）
*   M - 月的短名称
*   MM - 月的长名称
*   y - 年（两位数）
*   yy - 年（四位数）
*   @ - Unix 时间戳（ms since 01/01/1970）
*   ! - Windows 钟表（100ns since 01/01/0001）
*   '...' - 文本
*   '' - 单引号
*   其他 - 文本

也有一些 `$.datepicker` 预定义的标准日期格式：

*   ATOM - 'yy-mm-dd' （与 RFC 3339/ISO 8601 相同）
*   COOKIE - 'D, dd M yy'
*   ISO_8601 - 'yy-mm-dd'
*   RFC_822 - 'D, d M y' （参照 RFC 822）
*   RFC_850 - 'DD, dd-M-y' （参照 RFC 850）
*   RFC_1036 - 'D, d M y' （参照 RFC 1036）
*   RFC_1123 - 'D, d M yy' （参照 RFC 1123）
*   RFC_2822 - 'D, d M yy' （参照 RFC 2822）
*   RSS - 'D, d M y' （与 RFC 822 相同）
*   TICKS - '!'
*   TIMESTAMP - '@'
*   W3C - 'yy-mm-dd' （与 ISO 8601 相同）

**Code examples:**

以 ISO 格式显示日期。产生 "2007-01-26"。

```
$.datepicker.formatDate( "yy-mm-dd", new Date( 2007, 1 - 1, 26 ) ); 
```

以扩展法语格式显示日期。产生 "Samedi, Juillet 14, 2007"。

```
$.datepicker.formatDate( "DD, MM d, yy", new Date( 2007, 7 - 1, 14 ), {
  dayNamesShort: $.datepicker.regional[ "fr" ].dayNamesShort,
  dayNames: $.datepicker.regional[ "fr" ].dayNames,
  monthNamesShort: $.datepicker.regional[ "fr" ].monthNamesShort,
  monthNames: $.datepicker.regional[ "fr" ].monthNames
}); 
```

#### $.datepicker.parseDate( format, value, settings )

从一个指定格式的字符串值中提取日期。

格式可以是下列组合：

*   d - 一月中的第几天（没有前导零）
*   dd - 一月中的第几天（两位数）
*   o - 一年中的第几天（没有前导零）
*   oo - 一年中的第几天（三位数）
*   D - 星期几的短名称
*   DD - 星期几的长名称
*   m - 一年中的第几月（没有前导零）
*   mm - 一年中的第几月（两位数）
*   M - 月的短名称
*   MM - 月的长名称
*   y - 年（两位数）
*   yy - 年（四位数）
*   @ - Unix 时间戳（ms since 01/01/1970）
*   ! - Windows 钟表（100ns since 01/01/0001）
*   '...' - 文本
*   '' - 单引号
*   其他 - 文本

一些可能被抛出的异常：

*   'Invalid arguments' - 如果格式或值为空则抛出此异常。
*   'Missing number at position nn' - 如果格式显示一个未找到的数值则抛出此异常。
*   'Unknown name at position nn' - 如果格式显示一个未找到的星期几名称或月份名称则抛出此异常。
*   'Unexpected literal at position nn' - 如果格式显示一个未找到的文本值则抛出此异常。
*   'Invalid date' - 如果日期无效则抛出此异常，比如 '31/02/2007'。

**Code examples:**

提取一个 ISO 格式的日期。

```
$.datepicker.parseDate( "yy-mm-dd", "2007-01-26" ); 
```

提取一个扩展法语格式的日期。

```
$.datepicker.parseDate( "DD, MM d, yy", "Samedi, Juillet 14, 2007", {
  shortYearCuroff: 20,
  dayNamesShort: $.datepicker.regional[ "fr" ].dayNamesShort,
  dayNames: $.datepicker.regional[ "fr" ].dayNames,
  monthNamesShort: $.datepicker.regional[ "fr" ].monthNamesShort,
  monthNames: $.datepicker.regional[ "fr" ].monthNames
}); 
```

#### $.datepicker.iso8601Week( date )

确定一个给定的日期在一年中的第几周：1 到 53。

该函数使用 ISO 8601 定义一周：一周从星期一开始，每一年的第一周包含 1 月 4 日。这意味着上一年至多有三天可能包含在当年的第一周中，当年至多有三天可能包含在上一年的最后一周中。

该函数是 `calculateWeek` 选项的默认实现。

**Code examples:**

查找日期在一年中的第几周。

```
$.datepicker.iso8601Week( new Date( 2007, 1 - 1, 26 ) ); 
```

#### $.datepicker.noWeekends

设置如 beforeShowDay 函数，防止选择周末。

我们可以在 `beforeShowDay` 选项中提供 `noWeekends()` 函数，用来计算所有工作日，提供一个 `true`/`false` 值的数组，用来指示日期是否可选择。

**Code examples:**

设置 DatePicker，让周末不可选。

```
$( "#datepicker" ).datepicker({
  beforeShowDay: $.datepicker.noWeekends
}); 
```

### 局限

日期选择器提供了迎合不同的语言和日期格式本地化内容的支持。每个本地化包含在名称后追加语言代码的文件中，例如法语为 `jquery.ui.datepicker-fr.js`。所需的本地化文件需要包含在主要的日期选择器代码后面。每个本地化文件添加了它自己的设置到可用的本地化集合中，所有实例自动应用这些设置为默认设置。

`$.datepicker.regional` 属性保存了一个本地化数组，以语言代码作为前置，默认前置为 `""`，表示英语。每个条目是一个带有下列属性的对象：`closeText` 、 `prevText` 、 `nextText` 、 `currentText` 、 `monthNames` 、 `monthNamesShort` 、 `dayNames` 、 `dayNamesShort` 、 `dayNamesMin` 、 `weekHeader` 、 `dateFormat` 、 `firstDay` 、 `isRTL` 、 `showMonthAfterYear` 和 `yearSuffix`。

您可以通过下面代码恢复默认的本地化：

`$.datepicker.setDefaults( $.datepicker.regional[ "" ] );`

您可以通过下面代码覆盖一个特定地点的日期选择器：

`$( selector ).datepicker( $.datepicker.regional[ "fr" ] );`

### 主题

日期选择器部件（Datepicker Widget）使用 jQuery UI CSS 框架 来定义它的外观和感观的样式。如果需要使用日期选择器指定的样式，则可以使用下面的 CSS class 名称：

*   `ui-datepicker`：日期选择器的外层容器。如果日期选择器是内联的，该元素会另外带有一个 `ui-datepicker-inline` class。如果设置了 `isRTL` 选项，该元素会另外带有一个 `ui-datepicker-rtl` class。
    *   `ui-datepicker-header`：日期选择器的头部容器。
        *   `ui-datepicker-prev`：用于选择上一月的控件。
        *   `ui-datepicker-next`：用于选择下一月的控件。
        *   `ui-datepicker-title`：日期选择器包含月和年的标题容器。
            *   `ui-datepicker-month`：月的文本显示，如果设置了 `changeMonth` 选项则显示 `&lt;select&gt;` 元素。
            *   `ui-datepicker-year`：年的文本显示，如果设置了 `changeYear` 选项则显示 `&lt;select&gt;` 元素。
    *   `ui-datepicker-calendar`：包含日历的表格。
        *   `ui-datepicker-week-end`：周末的单元格。: Cells containing weekend days.
        *   `ui-datepicker-other-month`：发生在某月但不是当前月天数的单元格。
        *   `ui-datepicker-unselectable`：用户不可选择的单元格。
        *   `ui-datepicker-current-day`：已选中日期的单元格。
        *   `ui-datepicker-today`：当天日期的单元格。
    *   `ui-datepicker-buttonpane`：当设置 `showButtonPanel` 选项时使用按钮面板（buttonpane）。
        *   `ui-datepicker-current`：用于选择当天日期的按钮。

如果 `numberOfMonths` 选项用于显示多个月份，则使用一些额外的 class：

*   `ui-datepicker-multi`：一个多月份日期选择器的最外层容器。该元素会根据要显示的月份个数另外带有 `ui-datepicker-multi-2`、`ui-datepicker-multi-3` 或 `ui-datepicker-multi-4` class 名称。
    *   `ui-datepicker-group`：分组内单独的选择器。该元素会根据它在分组中的位置另外带有 `ui-datepicker-group-first`、`ui-datepicker-group-middle` 或 `ui-datepicker-group-last` class 名称。

### 依赖

*   UI 核心（UI Core）
*   特效核心（Effects Core）（可选的；当与 `showAnim` 选项一起使用时）

### 其他注意事项：

*   该部件要求一些功能性的 CSS，否则将无法工作。如果您创建了一个自定义的主题，请使用小部件指定的 CSS 文件作为起点。
*   该部件以编程方式操作元素的值，因此当元素的值改变时不会触发原生的 `change` 事件。
*   不支持在 `&lt;input type="date"&gt;` 上创建日期选择器，因为会造成与本地选择器的 UI 冲突。

## Options

### altField**Type:** [Selector](http://api.jquery.com/Types/#Selector) or [jQuery](http://api.jquery.com/Types/#jQuery) or [Element](http://api.jquery.com/Types/#Element)

**Default:** `""`一个 input 元素 ，使用选择器 选择的另一个地方更新 datepicker 选择的日期. 使用 `altFormat` 指定的这一区域设置如下改变格式的日期(使用 input 最直观). 如果没有代替的区域则使用空白.**Code examples:**

初始化带有指定 `altField` 选项的 datepicker：

```
$( ".selector" ).datepicker({ altField: "#actualDate" }); 
```

在初始化后，获取或设置`altField` 选项：

```
// getter
var altField = $( ".selector" ).datepicker( "option", "altField" );

// setter
$( ".selector" ).datepicker( "option", "altField", "#actualDate" ); 
```

### altFormat**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `""``dateFormat` 被 `altField` 项所使用。 它的目的是允许选择一种日期格式显示给用户以供选择，而实际的格式则是来自后台。 对于可能的格式的完整列表，请参阅 `formatDate` 函数。**Code examples:**

初始化带有指定 `altFormat` 选项的 datepicker：

```
$( ".selector" ).datepicker({ altFormat: "yy-mm-dd" }); 
```

在初始化后，获取或设置`altFormat` 选项：

```
// getter
var altFormat = $( ".selector" ).datepicker( "option", "altFormat" );

// setter
$( ".selector" ).datepicker( "option", "altFormat", "yy-mm-dd" ); 
```

### appendText**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `""`显示每个日期字段后面的文本， 例如，以显示所需的格式。**Code examples:**

初始化带有指定 `appendText` 选项的 datepicker：

```
$( ".selector" ).datepicker({ appendText: "(yyyy-mm-dd)" }); 
```

在初始化后，获取或设置`appendText` 选项：

```
// getter
var appendText = $( ".selector" ).datepicker( "option", "appendText" );

// setter
$( ".selector" ).datepicker( "option", "appendText", "(yyyy-mm-dd)" ); 
```

### autoSize**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为`true`，将自动调整输入字段，以适应日期在当前的`dateFormat`。**Code examples:**

初始化带有指定 `autoSize` 选项的 datepicker：

```
$( ".selector" ).datepicker({ autoSize: true }); 
```

在初始化后，获取或设置`autoSize` 选项：

```
// getter
var autoSize = $( ".selector" ).datepicker( "option", "autoSize" );

// setter
$( ".selector" ).datepicker( "option", "autoSize", true ); 
```

### beforeShow**Type:** [Function](http://api.jquery.com/Types/#Function)( [Element](http://api.jquery.com/Types/#Element) input, [Object](http://api.jquery.com/Types/#Object) inst )

**Default:** `null`一个函数，它接受一个输入字段和当前的 datepicker 实例， 并返回一个选项对象来修改 datepicker。只在 datepicker 显示之前被调用。

### beforeShowDay**Type:** [Function](http://api.jquery.com/Types/#Function)( [Date](http://api.jquery.com/Types/#Date) date )

**Default:** `null`一个函数，它接受一个日期作为参数 并且 必须返回一个数组：

*   `[0]`: `true`/`false` 表示这个日期是否可选
*   `[1]`: 一个 CSS class 名 添加到日期的单元格 或默认描述为`""`。
*   `[2]`:一个可选的日期弹出提示

该函数在 datepicker 每一天显示之前被调用。

### buttonImage**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `""`当`showOn`选项设置为`"button"`或`"both"`时， 用于显示 datepicker 的图片 url 地址。 如果设置，`buttonText`选项将成为`alt`值，而不是直接显示。**Code examples:**

初始化带有指定 `buttonImage` 选项的 datepicker：

```
$( ".selector" ).datepicker({ buttonImage: "/images/datepicker.gif" }); 
```

在初始化后，获取或设置`buttonImage` 选项：

```
// getter
var buttonImage = $( ".selector" ).datepicker( "option", "buttonImage" );

// setter
$( ".selector" ).datepicker( "option", "buttonImage", "/images/datepicker.gif" ); 
```

### buttonImageOnly**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`无论是按钮 图像 必须自行提供 而不是 里面一个按钮元素。 此选项仅当`buttonImage`选项也被设置时才起作用。**Code examples:**

初始化带有指定 `buttonImageOnly` 选项的 datepicker：

```
$( ".selector" ).datepicker({ buttonImageOnly: true }); 
```

在初始化后，获取或设置`buttonImageOnly` 选项：

```
// getter
var buttonImageOnly = $( ".selector" ).datepicker( "option", "buttonImageOnly" );

// setter
$( ".selector" ).datepicker( "option", "buttonImageOnly", true ); 
```

### buttonText**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"..."`显示在触发按钮上的文本。和`showOn`设置为 `"button"` 或 `"both"`时结合使用。**Code examples:**

初始化带有指定 `buttonText` 选项的 datepicker：

```
$( ".selector" ).datepicker({ buttonText: "Choose" }); 
```

在初始化后，获取或设置`buttonText` 选项：

```
// getter
var buttonText = $( ".selector" ).datepicker( "option", "buttonText" );

// setter
$( ".selector" ).datepicker( "option", "buttonText", "Choose" ); 
```

### calculateWeek**Type:** [Function](http://api.jquery.com/Types/#Function)()

**Default:** `jQuery.datepicker.iso8601Week`一个函数来计算当前周是一年中的第几周。 默认实现使用 ISO8601 的定义：的定义执行: 每周从周一开始；每年的第一个星期包含这年的第一个星期四。愚人码头注：这意味着今年的第一周中可能会包含去年的 3 天,并且今年的 3 天可能会被包含进去年的最后一周中。**Code examples:**

初始化带有指定 `calculateWeek` 选项的 datepicker：

```
$( ".selector" ).datepicker({ calculateWeek: myWeekCalc }); 
```

在初始化后，获取或设置`calculateWeek` 选项：

```
// getter
var calculateWeek = $( ".selector" ).datepicker( "option", "calculateWeek" );

// setter
$( ".selector" ).datepicker( "option", "calculateWeek", myWeekCalc ); 
```

### changeMonth**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`允许你将月份修改为一个下拉菜单。 你可以将参数设置为 false 来禁用此功能，也就是显示为文字。**Code examples:**

初始化带有指定 `changeMonth` 选项的 datepicker：

```
$( ".selector" ).datepicker({ changeMonth: true }); 
```

在初始化后，获取或设置`changeMonth` 选项：

```
// getter
var changeMonth = $( ".selector" ).datepicker( "option", "changeMonth" );

// setter
$( ".selector" ).datepicker( "option", "changeMonth", true ); 
```

### changeYear**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`允许你将年份修改为一个下拉菜单。 你可以将参数设置为 false 来禁用此功能，也就是显示为文字。使用`yearRange`选项来控制哪些年是可供选择。**Code examples:**

初始化带有指定 `changeYear` 选项的 datepicker：

```
$( ".selector" ).datepicker({ changeYear: true }); 
```

在初始化后，获取或设置`changeYear` 选项：

```
// getter
var changeYear = $( ".selector" ).datepicker( "option", "changeYear" );

// setter
$( ".selector" ).datepicker( "option", "changeYear", true ); 
```

### closeText**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"Done"`关闭连接显示的文字。使用`showButtonPanel`选项以显示此按钮。**Code examples:**

初始化带有指定 `closeText` 选项的 datepicker：

```
$( ".selector" ).datepicker({ closeText: "Close" }); 
```

在初始化后，获取或设置`closeText` 选项：

```
// getter
var closeText = $( ".selector" ).datepicker( "option", "closeText" );

// setter
$( ".selector" ).datepicker( "option", "closeText", "Close" ); 
```

### constrainInput**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `true`当值为`true`时，在输入栏的输入被限制为当前的日期格式`dateFormat`选项允许的字符。**Code examples:**

初始化带有指定 `constrainInput` 选项的 datepicker：

```
$( ".selector" ).datepicker({ constrainInput: false }); 
```

在初始化后，获取或设置`constrainInput` 选项：

```
// getter
var constrainInput = $( ".selector" ).datepicker( "option", "constrainInput" );

// setter
$( ".selector" ).datepicker( "option", "constrainInput", false ); 
```

### currentText**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"Today"`当前日期链接以文本形式显示。使用 `showButtonPanel`选项以显示此按钮。**Code examples:**

初始化带有指定 `currentText` 选项的 datepicker：

```
$( ".selector" ).datepicker({ currentText: "Now" }); 
```

在初始化后，获取或设置`currentText` 选项：

```
// getter
var currentText = $( ".selector" ).datepicker( "option", "currentText" );

// setter
$( ".selector" ).datepicker( "option", "currentText", "Now" ); 
```

### dateFormat**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"mm/dd/yy"`描述和显示日期的格式。 对于可能的格式的完整列表，请参阅``formatDate``函数。**Code examples:**

初始化带有指定 `dateFormat` 选项的 datepicker：

```
$( ".selector" ).datepicker({ dateFormat: "yy-mm-dd" }); 
```

在初始化后，获取或设置`dateFormat` 选项：

```
// getter
var dateFormat = $( ".selector" ).datepicker( "option", "dateFormat" );

// setter
$( ".selector" ).datepicker( "option", "dateFormat", "yy-mm-dd" ); 
```

### dayNames**Type:** [Array](http://api.jquery.com/Types/#Array)

**Default:** `[ "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" ]`日期长的名字的列表，从星期日(Sunday)开始，依照 `dateFormat`的设置进行使用。**Code examples:**

初始化带有指定 `dayNames` 选项的 datepicker：

```
$( ".selector" ).datepicker({ dayNames: [ "Dimanche", "Lundi", "Mardi", "Mercredi", "Jeudi", "Vendredi", "Samedi" ] }); 
```

在初始化后，获取或设置`dayNames` 选项：

```
// getter
var dayNames = $( ".selector" ).datepicker( "option", "dayNames" );

// setter
$( ".selector" ).datepicker( "option", "dayNames", [ "Dimanche", "Lundi", "Mardi", "Mercredi", "Jeudi", "Vendredi", "Samedi" ] ); 
```

### dayNamesMin**Type:** [Array](http://api.jquery.com/Types/#Array)

**Default:** `[ "Su", "Mo", "Tu", "We", "Th", "Fr", "Sa" ]`日期最小化简称的列表, 从周日开始(Sunday), 用在 datepicker 每列的头部.。**Code examples:**

初始化带有指定 `dayNamesMin` 选项的 datepicker：

```
$( ".selector" ).datepicker({ dayNamesMin: [ "Di", "Lu", "Ma", "Me", "Je", "Ve", "Sa" ] }); 
```

在初始化后，获取或设置`dayNamesMin` 选项：

```
// getter
var dayNamesMin = $( ".selector" ).datepicker( "option", "dayNamesMin" );

// setter
$( ".selector" ).datepicker( "option", "dayNamesMin", [ "Di", "Lu", "Ma", "Me", "Je", "Ve", "Sa" ] ); 
```

### dayNamesShort**Type:** [Array](http://api.jquery.com/Types/#Array)

**Default:** `[ "Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat" ]`日期名称的简写的列表, 从周日开始(Sunday), 依照`dateFormat`的设置使用。**Code examples:**

初始化带有指定 `dayNamesShort` 选项的 datepicker：

```
$( ".selector" ).datepicker({ dayNamesShort: [ "Dim", "Lun", "Mar", "Mer", "Jeu", "Ven", "Sam" ] }); 
```

在初始化后，获取或设置`dayNamesShort` 选项：

```
// getter
var dayNamesShort = $( ".selector" ).datepicker( "option", "dayNamesShort" );

// setter
$( ".selector" ).datepicker( "option", "dayNamesShort", [ "Dim", "Lun", "Mar", "Mer", "Jeu", "Ven", "Sam" ] ); 
```

### defaultDate**Type:** [Date](http://api.jquery.com/Types/#Date) or [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)

**Default:** `null`如果该字段为空时设置第一次打开时显示的日期。 通过 Date 对象或字符串在当前 `dateFormat`中指定任何一个实际的日期， 或者一个和今天对比的数字（例如 +7） 或者一个连续的字符串值('y' 表示年, 'm' 表示月, 'w'表示周, 'd'表示日, 例如. '+1m +7d'), 或者为空则是今天.**支持多个类型：**

*   **Date**: 一个包含默认日期的 date 对象。
*   **Number**: 一个和今天对比的数字。例如 `2` 表示从今天开始的第二天，（愚人码头注：即：后天）， `-1` 表示昨天。
*   **String**: 一个由`dateFormat`选项定义格式的字符串 ， 或相对日期。 相对日期必须包含值和期间对; 有效期间为：`"y"`表示几年， `"m"` 表示几月， `"w"`表示几周，和`"d"`表示几天。 例如， `"+1m +7d"`表示从今天开始的一个月加七天。

**Code examples:**

初始化带有指定 `defaultDate` 选项的 datepicker：

```
$( ".selector" ).datepicker({ defaultDate: +7 }); 
```

在初始化后，获取或设置`defaultDate` 选项：

```
// getter
var defaultDate = $( ".selector" ).datepicker( "option", "defaultDate" );

// setter
$( ".selector" ).datepicker( "option", "defaultDate", +7 ); 
```

### duration**Type:** or [String](http://api.jquery.com/Types/#String)

**Default:** `"normal"`设置 datepicker 展开动画的显示时间，可以是一个毫秒值, 也可以使用以下的三种字符值来表示("slow", "normal", "fast"), 或者为 ''则马上显示。**Code examples:**

初始化带有指定 `duration` 选项的 datepicker：

```
$( ".selector" ).datepicker({ duration: "slow" }); 
```

在初始化后，获取或设置`duration` 选项：

```
// getter
var duration = $( ".selector" ).datepicker( "option", "duration" );

// setter
$( ".selector" ).datepicker( "option", "duration", "slow" ); 
```

### firstDay**Type:** [Integer](http://api.jquery.com/Types/#Integer)

**Default:** `0`设置一周中的第一天:周日是 `0`, 周一是 `1`, 以此类推。**Code examples:**

初始化带有指定 `firstDay` 选项的 datepicker：

```
$( ".selector" ).datepicker({ firstDay: 1 }); 
```

在初始化后，获取或设置`firstDay` 选项：

```
// getter
var firstDay = $( ".selector" ).datepicker( "option", "firstDay" );

// setter
$( ".selector" ).datepicker( "option", "firstDay", 1 ); 
```

### gotoCurrent**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为`true`, 当前日的链接将移动到当前选中的日期，而不是今天。**Code examples:**

初始化带有指定 `gotoCurrent` 选项的 datepicker：

```
$( ".selector" ).datepicker({ gotoCurrent: true }); 
```

在初始化后，获取或设置`gotoCurrent` 选项：

```
// getter
var gotoCurrent = $( ".selector" ).datepicker( "option", "gotoCurrent" );

// setter
$( ".selector" ).datepicker( "option", "gotoCurrent", true ); 
```

### hideIfNoPrevNext**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`通常当前一个和下一个链接被禁用时不适用 (参看 `minDate` 和 `maxDate`). 你可以通过设置此属性为`true`完全的隐藏他们.**Code examples:**

初始化带有指定 `hideIfNoPrevNext` 选项的 datepicker：

```
$( ".selector" ).datepicker({ hideIfNoPrevNext: true }); 
```

在初始化后，获取或设置`hideIfNoPrevNext` 选项：

```
// getter
var hideIfNoPrevNext = $( ".selector" ).datepicker( "option", "hideIfNoPrevNext" );

// setter
$( ".selector" ).datepicker( "option", "hideIfNoPrevNext", true ); 
```

### isRTL**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`当前语言描述是否为自右向左的。（愚人码头注：例如阿拉伯语）**Code examples:**

初始化带有指定 `isRTL` 选项的 datepicker：

```
$( ".selector" ).datepicker({ isRTL: true }); 
```

在初始化后，获取或设置`isRTL` 选项：

```
// getter
var isRTL = $( ".selector" ).datepicker( "option", "isRTL" );

// setter
$( ".selector" ).datepicker( "option", "isRTL", true ); 
```

### maxDate**Type:** [Date](http://api.jquery.com/Types/#Date) or [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)

**Default:** `null`最大的可选日期。当设置为`null`时，没有上限。**支持多个类型：**

*   **Date**: 一个包含默认日期的 date 对象。
*   **Number**: 一个和今天对比的数字。例如 `2` 表示从今天开始的第二天，（愚人码头注：即：后天）， `-1` 表示昨天。
*   **String**: 一个由`dateFormat`选项定义格式的字符串 ， 或相对日期。 相对日期必须包含值和期间对; 有效期间为：`"y"`表示几年， `"m"` 表示几月， `"w"`表示几周，和`"d"`表示几天。 例如， `"+1m +7d"`表示从今天开始的一个月加七天。

**Code examples:**

初始化带有指定 `maxDate` 选项的 datepicker：

```
$( ".selector" ).datepicker({ maxDate: "+1m +1w" }); 
```

在初始化后，获取或设置`maxDate` 选项：

```
// getter
var maxDate = $( ".selector" ).datepicker( "option", "maxDate" );

// setter
$( ".selector" ).datepicker( "option", "maxDate", "+1m +1w" ); 
```

### minDate**Type:** [Date](http://api.jquery.com/Types/#Date) or [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)

**Default:** `null`最小的可选日期。当设置为`null`时，没有下限。**支持多个类型：**

*   **Date**: 一个包含默认日期的 date 对象。
*   **Number**: 一个和今天对比的数字。例如 `2` 表示从今天开始的第二天，（愚人码头注：即：后天）， `-1` 表示昨天。
*   **String**: 一个由`dateFormat`选项定义格式的字符串 ， 或相对日期。 相对日期必须包含值和期间对; 有效期间为：`"y"`表示几年， `"m"` 表示几月， `"w"`表示几周，和`"d"`表示几天。 例如， `"+1m +7d"`表示从今天开始的一个月加七天。

**Code examples:**

初始化带有指定 `minDate` 选项的 datepicker：

```
$( ".selector" ).datepicker({ minDate: new Date(2007, 1 - 1, 1) }); 
```

在初始化后，获取或设置`minDate` 选项：

```
// getter
var minDate = $( ".selector" ).datepicker( "option", "minDate" );

// setter
$( ".selector" ).datepicker( "option", "minDate", new Date(2007, 1 - 1, 1) ); 
```

### monthNames**Type:** [Array](http://api.jquery.com/Types/#Array)

**Default:** `[ "January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December" ]`月份的完全名称列表，依照 `dateFormat`的设置进行使用。**Code examples:**

初始化带有指定 `monthNames` 选项的 datepicker：

```
$( ".selector" ).datepicker({ monthNames: [ "Januar", "Februar", "Marts", "April", "Maj", "Juni", "Juli", "August", "September", "Oktober", "November", "December" ] }); 
```

在初始化后，获取或设置`monthNames` 选项：

```
// getter
var monthNames = $( ".selector" ).datepicker( "option", "monthNames" );

// setter
$( ".selector" ).datepicker( "option", "monthNames", [ "Januar", "Februar", "Marts", "April", "Maj", "Juni", "Juli", "August", "September", "Oktober", "November", "December" ] ); 
```

### monthNamesShort**Type:** [Array](http://api.jquery.com/Types/#Array)

**Default:** `[ "Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec" ]`月份简写名称的列表，依照 `dateFormat`的设置进行使用。**Code examples:**

初始化带有指定 `monthNamesShort` 选项的 datepicker：

```
$( ".selector" ).datepicker({ monthNamesShort: [ "Jan", "Feb", "Mar", "Apr", "Maj", "Jun", "Jul", "Aug", "Sep", "Okt", "Nov", "Dec" ] }); 
```

在初始化后，获取或设置`monthNamesShort` 选项：

```
// getter
var monthNamesShort = $( ".selector" ).datepicker( "option", "monthNamesShort" );

// setter
$( ".selector" ).datepicker( "option", "monthNamesShort", [ "Jan", "Feb", "Mar", "Apr", "Maj", "Jun", "Jul", "Aug", "Sep", "Okt", "Nov", "Dec" ] ); 
```

### navigationAsDateFormat**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`确定是`prevText` 和 `nextText`选项是否应该被解析为``formatDate``函数的日期，让他们能够显示目标的月份名称.**Code examples:**

初始化带有指定 `navigationAsDateFormat` 选项的 datepicker：

```
$( ".selector" ).datepicker({ navigationAsDateFormat: true }); 
```

在初始化后，获取或设置`navigationAsDateFormat` 选项：

```
// getter
var navigationAsDateFormat = $( ".selector" ).datepicker( "option", "navigationAsDateFormat" );

// setter
$( ".selector" ).datepicker( "option", "navigationAsDateFormat", true ); 
```

### nextText**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"Next"`下个月链接显示的文字 。使用标准 ThemeRoller 样式， 这个值被替换为一个图标。**Code examples:**

初始化带有指定 `nextText` 选项的 datepicker：

```
$( ".selector" ).datepicker({ nextText: "Later" }); 
```

在初始化后，获取或设置`nextText` 选项：

```
// getter
var nextText = $( ".selector" ).datepicker( "option", "nextText" );

// setter
$( ".selector" ).datepicker( "option", "nextText", "Later" ); 
```

### numberOfMonths**Type:** [Number](http://api.jquery.com/Types/#Number) or [Array](http://api.jquery.com/Types/#Array)

**Default:** `1`设置一次显示几个月.**支持多个类型：**

*   **Number**: 一行显示的月份数
*   **Array**: 一个数组定义的显示行数和列数。

**Code examples:**

初始化带有指定 `numberOfMonths` 选项的 datepicker：

```
$( ".selector" ).datepicker({ numberOfMonths: [ 2, 3 ] }); 
```

在初始化后，获取或设置`numberOfMonths` 选项：

```
// getter
var numberOfMonths = $( ".selector" ).datepicker( "option", "numberOfMonths" );

// setter
$( ".selector" ).datepicker( "option", "numberOfMonths", [ 2, 3 ] ); 
```

### onChangeMonthYear**Type:** [Function](http://api.jquery.com/Types/#Function)( [Integer](http://api.jquery.com/Types/#Integer) year, [Integer](http://api.jquery.com/Types/#Integer) month, [Object](http://api.jquery.com/Types/#Object) inst )

**Default:** `null`当 datepicker 移动到一个新的月份 并/或 年份时调用。 该函数接收选定的年份， 月份（1-12）， 和 datepicker 实例作为参数。 `this`指向相关联的输入域。

### onClose**Type:** [Function](http://api.jquery.com/Types/#Function)( [String](http://api.jquery.com/Types/#String) dateText, [Object](http://api.jquery.com/Types/#Object) inst )

**Default:** `null`当 datepicker 关闭时调用，确定一个日期是否被选中。 该函数接收所选日期的文本（`""`如果没有）和 datepicker 实例作为参数。 `this`指向相关联的输入域。

### onSelect**Type:** [Function](http://api.jquery.com/Types/#Function)( [String](http://api.jquery.com/Types/#String) dateText, [Object](http://api.jquery.com/Types/#Object) inst )

**Default:** `null`当选择 datepicker 调用。 该函数接收所选日期的文本和 datepicker 实例作为参数。`this`指向相关联的输入域。

### prevText**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"Prev"`上个月链接显示的文字 。使用标准 ThemeRoller 样式， 这个值被替换为一个图标。**Code examples:**

初始化带有指定 `prevText` 选项的 datepicker：

```
$( ".selector" ).datepicker({ prevText: "Earlier" }); 
```

在初始化后，获取或设置`prevText` 选项：

```
// getter
var prevText = $( ".selector" ).datepicker( "option", "prevText" );

// setter
$( ".selector" ).datepicker( "option", "prevText", "Earlier" ); 
```

### selectOtherMonths**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`显示在当前月份的之前或之后的日期是否可以被选择。（愚人码头注：比如 2014 年 4 月 1 日是周二，如果`showOtherMonths`选项设置为`true`，那么 2014 年 3 月 31 日，2014 年 3 月 30 日会以灰色的形式显示在 4 月份的面板上，这个选项表示在 4 月份的面板上是否可以选择 2014 年 3 月 31 日，2014 年 3 月 30 日这两个日期。5 月也是一样的。） 这选项仅适用于 如果`showOtherMonths`选项设置为`true`的时候。**Code examples:**

初始化带有指定 `selectOtherMonths` 选项的 datepicker：

```
$( ".selector" ).datepicker({ selectOtherMonths: true }); 
```

在初始化后，获取或设置`selectOtherMonths` 选项：

```
// getter
var selectOtherMonths = $( ".selector" ).datepicker( "option", "selectOtherMonths" );

// setter
$( ".selector" ).datepicker( "option", "selectOtherMonths", true ); 
```

### shortYearCutoff**Type:** [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)

**Default:** `"+10"`设置一个定义日期所处实际的截断年份值(与`dateFormat`中的 'y'共同使用). 如果是一个数值 (0-99)那么将直接使用这些值. 如果提供的是一个字符串值那么它将被转换为数值添加到当前年. 一旦截断年开始计算, 任何输入的日期的年份小于或者等于它的话将被判定为在本世纪,大于他的将被判定为在上个世纪.**支持多个类型：**

*   **Number**: 一个 `0` 到 `99`的值表示截断年份值
*   **String**: 从本年份开始的相对年数，例如, `"+3"` or `"-5"`.

**Code examples:**

初始化带有指定 `shortYearCutoff` 选项的 datepicker：

```
$( ".selector" ).datepicker({ shortYearCutoff: 50 }); 
```

在初始化后，获取或设置`shortYearCutoff` 选项：

```
// getter
var shortYearCutoff = $( ".selector" ).datepicker( "option", "shortYearCutoff" );

// setter
$( ".selector" ).datepicker( "option", "shortYearCutoff", 50 ); 
```

### showAnim**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"show"`设置显示/隐藏 datepicker 的动画名称. 使用 `"show"` (默认), `"slideDown"`， `"fadeIn"`, 或其他任何 jQuery UI effects 的显示/隐藏效果。 设置为空字符串可以禁用动画，即直接显示或者隐藏。**Code examples:**

初始化带有指定 `showAnim` 选项的 datepicker：

```
$( ".selector" ).datepicker({ showAnim: "fold" }); 
```

在初始化后，获取或设置`showAnim` 选项：

```
// getter
var showAnim = $( ".selector" ).datepicker( "option", "showAnim" );

// setter
$( ".selector" ).datepicker( "option", "showAnim", "fold" ); 
```

### showButtonPanel**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`是否显示日历下方的按钮面板。 按钮面板包含两个按钮， 一个今天按钮链接到当前日期， 和一个完成按钮关闭 datepicker。 该按钮的文本可以使用`currentText` 和 `closeText`选项分别进行定制。**Code examples:**

初始化带有指定 `showButtonPanel` 选项的 datepicker：

```
$( ".selector" ).datepicker({ showButtonPanel: true }); 
```

在初始化后，获取或设置`showButtonPanel` 选项：

```
// getter
var showButtonPanel = $( ".selector" ).datepicker( "option", "showButtonPanel" );

// setter
$( ".selector" ).datepicker( "option", "showButtonPanel", true ); 
```

### showCurrentAtPos**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `0`通过`numberOfMonths`选项设置多月份显示的情况下，当前月份显示的位置。（愚人码头注：自顶部/左边开始第 n 位，以 0 开始计数。）**Code examples:**

初始化带有指定 `showCurrentAtPos` 选项的 datepicker：

```
$( ".selector" ).datepicker({ showCurrentAtPos: 3 }); 
```

在初始化后，获取或设置`showCurrentAtPos` 选项：

```
// getter
var showCurrentAtPos = $( ".selector" ).datepicker( "option", "showCurrentAtPos" );

// setter
$( ".selector" ).datepicker( "option", "showCurrentAtPos", 3 ); 
```

### showMonthAfterYear**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`是否在面板的头部年份后面显示月份。**Code examples:**

初始化带有指定 `showMonthAfterYear` 选项的 datepicker：

```
$( ".selector" ).datepicker({ showMonthAfterYear: true }); 
```

在初始化后，获取或设置`showMonthAfterYear` 选项：

```
// getter
var showMonthAfterYear = $( ".selector" ).datepicker( "option", "showMonthAfterYear" );

// setter
$( ".selector" ).datepicker( "option", "showMonthAfterYear", true ); 
```

### showOn**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"focus"`设置触发 datepicker 自动出现的事件名称,是 focus (`"focus"`)还是 clicked (`"button"`)或者任何事件(`"both"`)。**Code examples:**

初始化带有指定 `showOn` 选项的 datepicker：

```
$( ".selector" ).datepicker({ showOn: "both" }); 
```

在初始化后，获取或设置`showOn` 选项：

```
// getter
var showOn = $( ".selector" ).datepicker( "option", "showOn" );

// setter
$( ".selector" ).datepicker( "option", "showOn", "both" ); 
```

### showOptions**Type:** [Object](http://api.jquery.com/Types/#Object)

**Default:** `{}`如果想`showAnim`选项来使用 jQuery UI effects 动画效果, 你可以为动画提供一些额外的设置.**Code examples:**

初始化带有指定 `showOptions` 选项的 datepicker：

```
$( ".selector" ).datepicker({ showOptions: { direction: "up" } }); 
```

在初始化后，获取或设置`showOptions` 选项：

```
// getter
var showOptions = $( ".selector" ).datepicker( "option", "showOptions" );

// setter
$( ".selector" ).datepicker( "option", "showOptions", { direction: "up" } ); 
```

### showOtherMonths**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`是否在当前月份面板显示上、下两个月的一些日期数（不可选）。 想要让这些日期可选，请使用`selectOtherMonths`选项。**Code examples:**

初始化带有指定 `showOtherMonths` 选项的 datepicker：

```
$( ".selector" ).datepicker({ showOtherMonths: true }); 
```

在初始化后，获取或设置`showOtherMonths` 选项：

```
// getter
var showOtherMonths = $( ".selector" ).datepicker( "option", "showOtherMonths" );

// setter
$( ".selector" ).datepicker( "option", "showOtherMonths", true ); 
```

### showWeek**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果为`true`，面板将增加一列，显示一年中的哪一周。 该`calculateWeek`选项决定一年中的哪一周是如何计算的。 您可以改变 `firstDay`选项。**Code examples:**

初始化带有指定 `showWeek` 选项的 datepicker：

```
$( ".selector" ).datepicker({ showWeek: true }); 
```

在初始化后，获取或设置`showWeek` 选项：

```
// getter
var showWeek = $( ".selector" ).datepicker( "option", "showWeek" );

// setter
$( ".selector" ).datepicker( "option", "showWeek", true ); 
```

### stepMonths**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `1`当点击上/下一月链接时，一次翻几个月。**Code examples:**

初始化带有指定 `stepMonths` 选项的 datepicker：

```
$( ".selector" ).datepicker({ stepMonths: 3 }); 
```

在初始化后，获取或设置`stepMonths` 选项：

```
// getter
var stepMonths = $( ".selector" ).datepicker( "option", "stepMonths" );

// setter
$( ".selector" ).datepicker( "option", "stepMonths", 3 ); 
```

### weekHeader**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"Wk"`本年度哪一周 列的标题显示文本。 使用`showWeek`选项以显示此列。**Code examples:**

初始化带有指定 `weekHeader` 选项的 datepicker：

```
$( ".selector" ).datepicker({ weekHeader: "W" }); 
```

在初始化后，获取或设置`weekHeader` 选项：

```
// getter
var weekHeader = $( ".selector" ).datepicker( "option", "weekHeader" );

// setter
$( ".selector" ).datepicker( "option", "weekHeader", "W" ); 
```

### yearRange**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"c-10:c+10"`控制年份的下拉列表中显示的年份数量，可以是相对当前年(-nn:+nn)，相对于选择年份(-nn:+nn)，也可以是绝对值(`"nnnn:nnnn"`)，或这些格式的组合 (`"nnnn:-nn"`)。 请注意，此选项仅影响下拉列表中的显示， 使用`minDate` 和/或 `maxDate`选项限制哪些日期可以选择。**Code examples:**

初始化带有指定 `yearRange` 选项的 datepicker：

```
$( ".selector" ).datepicker({ yearRange: "2002:2012" }); 
```

在初始化后，获取或设置`yearRange` 选项：

```
// getter
var yearRange = $( ".selector" ).datepicker( "option", "yearRange" );

// setter
$( ".selector" ).datepicker( "option", "yearRange", "2002:2012" ); 
```

### yearSuffix**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `""`显示在月份头部中年份后面的文本。**Code examples:**

初始化带有指定 `yearSuffix` 选项的 datepicker：

```
$( ".selector" ).datepicker({ yearSuffix: "CE" }); 
```

在初始化后，获取或设置`yearSuffix` 选项：

```
// getter
var yearSuffix = $( ".selector" ).datepicker( "option", "yearSuffix" );

// setter
$( ".selector" ).datepicker( "option", "yearSuffix", "CE" ); 
```

## Methods

### destroy()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

完全移除 datepicker 功能. 这将使元素返回到之前的初始化状态.

*   该方法不接受任何参数。

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).datepicker( "destroy" ); 
```

### dialog( date [, onSelect ] [, settings ] [, pos ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

在一个"dialog"中打开一个 datepicker。

*   **date**Type: [String](http://api.jquery.com/Types/#String) or [Date](http://api.jquery.com/Types/#Date)初始化的日期。
*   **onSelect**Type: [Function](http://api.jquery.com/Types/#Function)()当一个日期被选中时的回调函数. 这个函数接收日期文本 和 datepicker 实例作为参数。
*   **settings**Type: [Options](http://api.jquery.com/Types/#Options)新的 datepicker 的选项。
*   **pos**Type: [Number[2] or MouseEvent](http://api.jquery.com/Types/#Number%5B2%5D%20or%20MouseEvent)dialog 对话框的 top/left 的`[x, y]`坐标，或者一个鼠标事件`MouseEvent`的坐标。如果不提供此参数 dialog 将显示在屏幕正中。

**Code examples:**

调用 dialog 方法：

```
$( ".selector" ).datepicker( "dialog", "10/12/2012" ); 
```

### getDate()Returns: [Date](http://api.jquery.com/Types/#Date)

返回一个 datepicker 中当前日期, 如果没有日期被选中的话那么返回`null`。

*   该方法不接受任何参数。

**Code examples:**

调用 getDate 方法：

```
var currentDate = $( ".selector" ).datepicker( "getDate" ); 
```

### hide()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

关闭先前打开的 date picker。

*   该方法不接受任何参数。

**Code examples:**

调用 hide 方法：

```
$( ".selector" ).datepicker( "hide" ); 
```

### isDisabled()Returns: [Boolean](http://api.jquery.com/Types/#Boolean)

确定一个 datepicker 是否已禁用.

*   该方法不接受任何参数。

**Code examples:**

调用 isDisabled 方法：

```
var isDisabled = $( ".selector" ).datepicker( "isDisabled" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取当前与指定的 `optionName` 关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项的名称。

**Code examples:**

调用该方法：

```
var isDisabled = $( ".selector" ).datepicker( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含键/值对的对象，键/值对表示当前 datepicker 选项哈希。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
var options = $( ".selector" ).datepicker( "option" ); 
```

### option( optionName, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置与指定的 `optionName` 关联的 datepicker 选项的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的值。

**Code examples:**

调用该方法：

```
$( ".selector" ).datepicker( "option", "disabled", true ); 
```

### option( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

为 datepicker 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的 option-value 对。

**Code examples:**

调用该方法：

```
$( ".selector" ).datepicker( "option", { disabled: true } ); 
```

### refresh()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

在作出一些外部修改后，重绘日期选择器。

*   该方法不接受任何参数。

**Code examples:**

调用 refresh 方法：

```
$( ".selector" ).datepicker( "refresh" ); 
```

### setDate( date )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

为 datepicker 设置日期。 新的日期可能是一个`Date`对象或当前 date format 的字符串（例如，`"01/26/2009"`）， 一个从今天开始的天数（例如，`+7`） 或值和周期的字符串 `"y"` 表示年数, `"m"` 表示月份数, `"w"` 表示周数, `"d"`表示天数,例如， `"+1m +7d"`)， 或者为`null`来清除选定的日期。

*   **date**Type: [String](http://api.jquery.com/Types/#String) or [Date](http://api.jquery.com/Types/#Date)新的日期。

**Code examples:**

调用 setDate 方法：

```
$( ".selector" ).datepicker( "setDate", "10/12/2012" ); 
```

### show()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

显示日期 datepicker 插件。 如果 datepicker 被绑定到 input 元素， 要显示 datepicker 的 input 元素必须是可见的。

*   该方法不接受任何参数。

**Code examples:**

调用 show 方法：

```
$( ".selector" ).datepicker( "show" ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个包含 datepicker 的 `jQuery` 对象。

*   该方法不接受任何参数。

**Code examples:**

调用 widget 方法：

```
var widget = $( ".selector" ).datepicker( "widget" ); 
```

## Example:

#### 一个简单的 jQuery UI Datepicker.

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>datepicker demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<div id="datepicker"></div>

<script>
$( "#datepicker" ).datepicker();
</script>

</body>
</html> 
```

# Dialog Widget

Categories: [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## version added: 1.0

**Description:** 在一个交互覆盖层中打开内容。

## QuickNavExamples

### Options

*   appendTo
*   autoOpen
*   buttons
*   closeOnEscape
*   closeText
*   dialogClass
*   draggable
*   height
*   hide
*   maxHeight
*   maxWidth
*   minHeight
*   minWidth
*   modal
*   position
*   resizable
*   show
*   title
*   width

### Methods

*   close
*   destroy
*   isOpen
*   moveToTop
*   open
*   option
*   widget

### Extension Points

*   _allowInteraction

### Events

*   beforeClose
*   close
*   create
*   drag
*   dragStart
*   dragStop
*   focus
*   open
*   resize
*   resizeStart
*   resizeStop

对话框是一个悬浮窗口，包括一个标题栏和一个内容区域。对话框窗口可以移动，重新调整大小，默认情况下通过 'x' 图标关闭。

如果内容长度超过最大高度，一个滚动条会自动出现。

一个底部按钮栏和一个半透明的模式覆盖层是常见的添加选项。

### 焦点

当打开一个对话框时，焦点会自动移动到满足下面条件的第一个项目：

1.  带有 `autofocus` 属性的对话框内的第一个元素
2.  对话框内容内的第一个 `:tabbable` 元素
3.  对话框按钮面板内的第一个 `:tabbable` 元素
4.  对话框的关闭按钮
5.  对话框本身

当打开时，对话框部件（Dialog Widget）确保通过 tab 切换对话框内元素间的焦点，不包括对话框外的元素。模态对话框防止鼠标用户点击对话框外的元素。

当关闭对话框时，焦点自动返回到之前对话框打开时获得焦点的元素上。

### 隐藏关闭按钮

在一些情况下，您可能想要隐藏关闭按钮，例如，在按钮面板中已经有一个关闭按钮的情况。最好的解决方法是通过 CSS。作为实例，您可以定义一个简单的规则，比如：

```
.no-close .ui-dialog-titlebar-close {
  display: none;
} 
```

然后，您可以添加 `no-close` class 到任意的对话框，用来隐藏关闭按钮：

```
$( "#dialog" ).dialog({
  dialogClass: "no-close",
  buttons: [
    {
      text: "OK",
      click: function() {
        $( this ).dialog( "close" );
      }
    }
  ]
}); 
```

### 主题

对话框部件（Dialog Widget）使用 jQuery UI CSS 框架 来定义它的外观和感观的样式。如果需要使用对话框指定的样式，则可以使用下面的 CSS class 名称：

*   `ui-dialog`：对话框的外层容器。
    *   `ui-dialog-titlebar`：包含对话框标题和关闭按钮的标题栏。
        *   `ui-dialog-title`：对话框文本标题周围的容器。
        *   `ui-dialog-titlebar-close`：对话框的关闭按钮。
    *   `ui-dialog-content`：对话框内容周围的容器。这也是部件被实例化的元素。
    *   `ui-dialog-buttonpane`：包含对话按钮的面板。只有当设置了 `buttons` 选项时才呈现。
        *   `ui-dialog-buttonset`：按钮周围的容器。

此外，当设置了 `modal` 选项时，一个带有 `ui-widget-overlay` class 名称的元素被追加到 `&lt;body&gt;`。

### 依赖

*   UI 核心（UI Core）
*   部件库（Widget Factory）
*   定位（Position）
*   按钮部件（Button Widget）
*   可拖拽小部件（Draggable Widget） （可选的；当与 `draggable` 选项一起使用时）
*   可调整尺寸小部件（Resizable Widget） （可选的；当与 `resizable` 选项一起使用时）
*   特效核心（Effects Core）（可选的；当与 `show` 和 `hide` 选项一起使用时）

### 其他注意事项：

*   该部件要求一些功能性的 CSS，否则将无法工作。如果您创建了一个自定义的主题，请使用小部件指定的 CSS 文件作为起点。

## Options

### appendTo**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `"body"`

dialog（和遮罩层，如果 modal 存在）应该被追加到哪个元素。

**注意:**当 dialog 处于打开状态的时候`appendTo`选项不应该被改变。(version added: 1.10.0)**Code examples:**

初始化带有指定 `appendTo`选项的 dialog：

```
$( ".selector" ).dialog({ appendTo: "#someElem" }); 
```

在初始化后，获取或设置`appendTo` 选项：

```
// getter
var appendTo = $( ".selector" ).dialog( "option", "appendTo" );

// setter
$( ".selector" ).dialog( "option", "appendTo", "#someElem" ); 
```

### autoOpen**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `true`当设置为 `true` 时， dialog 会在初始化时自动打开. 如果为 `false` dialog 将会继续隐藏直到调用`open()`方法 。**Code examples:**

初始化带有指定 `autoOpen`选项的 dialog：

```
$( ".selector" ).dialog({ autoOpen: false }); 
```

在初始化后，获取或设置`autoOpen` 选项：

```
// getter
var autoOpen = $( ".selector" ).dialog( "option", "autoOpen" );

// setter
$( ".selector" ).dialog( "option", "autoOpen", false ); 
```

### buttons**Type:** [Object](http://api.jquery.com/Types/#Object) or [Array](http://api.jquery.com/Types/#Array)

**Default:** `{}`指定哪些按钮应该在 dialog 上显示。 回调的上下文是 dialog 元素（愚人码头注：`this`指向）; 如果你需要访问按钮， 可以利用事件对象的目标元素。**支持多个类型：**

*   **Object**: 键是按钮标签，值是点击相关按钮时执行的回调函数。
*   **Array**: 该数组的每个元素必须是 一个定义特性，属性，和按钮上设置的事件处理程序的对象。

**Code examples:**

初始化带有指定 `buttons`选项的 dialog：

```
$( ".selector" ).dialog({ buttons: [ { text: "Ok", click: function() { $( this ).dialog( "close" ); } } ] }); 
```

在初始化后，获取或设置`buttons` 选项：

```
// getter
var buttons = $( ".selector" ).dialog( "option", "buttons" );

// setter
$( ".selector" ).dialog( "option", "buttons", [ { text: "Ok", click: function() { $( this ).dialog( "close" ); } } ] ); 
```

### closeOnEscape**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `true`指定具有焦点的 dialog，在用户按下退出（ESC）键时，是否应该关闭 。**Code examples:**

初始化带有指定 `closeOnEscape`选项的 dialog：

```
$( ".selector" ).dialog({ closeOnEscape: false }); 
```

在初始化后，获取或设置`closeOnEscape` 选项：

```
// getter
var closeOnEscape = $( ".selector" ).dialog( "option", "closeOnEscape" );

// setter
$( ".selector" ).dialog( "option", "closeOnEscape", false ); 
```

### closeText**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"close"`指定关闭按钮的文本。 注意，关闭文本在使用标准的主题时，是隐藏的（visibly：hidden）。**Code examples:**

初始化带有指定 `closeText`选项的 dialog：

```
$( ".selector" ).dialog({ closeText: "hide" }); 
```

在初始化后，获取或设置`closeText` 选项：

```
// getter
var closeText = $( ".selector" ).dialog( "option", "closeText" );

// setter
$( ".selector" ).dialog( "option", "closeText", "hide" ); 
```

### dialogClass**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `""`在使用额外附加的主题时，指定 dialog 的类名称，这些样式添加到 dialog 上。**Code examples:**

初始化带有指定 `dialogClass`选项的 dialog：

```
$( ".selector" ).dialog({ dialogClass: "alert" }); 
```

在初始化后，获取或设置`dialogClass` 选项：

```
// getter
var dialogClass = $( ".selector" ).dialog( "option", "dialogClass" );

// setter
$( ".selector" ).dialog( "option", "dialogClass", "alert" ); 
```

### draggable**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `true`如果设置为`true`, dialog 将可以使用标题栏实现拖动。需要包含 jQuery UI Draggable 部件。**Code examples:**

初始化带有指定 `draggable`选项的 dialog：

```
$( ".selector" ).dialog({ draggable: false }); 
```

在初始化后，获取或设置`draggable` 选项：

```
// getter
var draggable = $( ".selector" ).dialog( "option", "draggable" );

// setter
$( ".selector" ).dialog( "option", "draggable", false ); 
```

### height**Type:** [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)

**Default:** `"auto"`设置对话框的高度（单位：像素）。**支持多个类型：**

*   **Number**: 高度，单位：像素。
*   **String**: 唯一支持的字符串值为`"auto"`，这将使对话框高度根据其内容进行自动调整。

**Code examples:**

初始化带有指定 `height`选项的 dialog：

```
$( ".selector" ).dialog({ height: 400 }); 
```

在初始化后，获取或设置`height` 选项：

```
// getter
var height = $( ".selector" ).dialog( "option", "height" );

// setter
$( ".selector" ).dialog( "option", "height", 400 ); 
```

### hide**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String) or [Object](http://api.jquery.com/Types/#Object)

**Default:** `null`dialog 关闭（隐藏）时的动画效果。**支持多个类型：**

*   **Boolean**: 当设置为`false`， 将不使用动画效果，该 dialog 会立即被隐藏。 如果设置为`true`， 该 dialog 将会以默认的持续时间和默认的效果淡出。
*   **Number**: 该 dialog 将以指定的时间和默认的效果淡出。
*   **String**: 该 dialog 将使用指定的效果被隐藏。 该值可以是一个 jQuery 内置的动画方法的名称， 如`"slideUp"`， 或一个 jQuery UI 效果的名称， 如`"fold"`。 在这两种情况下，将使用默认持续时间和默认的动画效果。
*   **Object**: 如果该值是一个对象， 那么 `effect`, `delay`, `duration`, 和`easing`可能要提供。 如果 `effect` 属性包含一个 jQuery 方法的名称， 那么该方法将被使用; 否则它被假定为是一个 jQuery UI 的效果的名称。 当使用 jQuery UI 支持额外设置 的效果 ， 你可以在对象中包含那些设置 并且它们将被传递到的效果。如果`duration`持续时间或`easing`属性被省略， 那么默认值将被使用。 如果`effect`被省略， 那么`"fadeOut"` 将被使用。如果`delay`被省略， 那么将不使用延迟。

**Code examples:**

初始化带有指定 `hide`选项的 dialog：

```
$( ".selector" ).dialog({ hide: { effect: "explode", duration: 1000 } }); 
```

在初始化后，获取或设置`hide` 选项：

```
// getter
var hide = $( ".selector" ).dialog( "option", "hide" );

// setter
$( ".selector" ).dialog( "option", "hide", { effect: "explode", duration: 1000 } ); 
```

### maxHeight**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `false`dialog 可以调整的最大高度，以像素为单位。**Code examples:**

初始化带有指定 `maxHeight`选项的 dialog：

```
$( ".selector" ).dialog({ maxHeight: 600 }); 
```

在初始化后，获取或设置`maxHeight` 选项：

```
// getter
var maxHeight = $( ".selector" ).dialog( "option", "maxHeight" );

// setter
$( ".selector" ).dialog( "option", "maxHeight", 600 ); 
```

### maxWidth**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `false`dialog 可以调整的最大宽度，以像素为单位。**Code examples:**

初始化带有指定 `maxWidth`选项的 dialog：

```
$( ".selector" ).dialog({ maxWidth: 600 }); 
```

在初始化后，获取或设置`maxWidth` 选项：

```
// getter
var maxWidth = $( ".selector" ).dialog( "option", "maxWidth" );

// setter
$( ".selector" ).dialog( "option", "maxWidth", 600 ); 
```

### minHeight**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `150`dialog 可以调整的最小高度，以像素为单位。**Code examples:**

初始化带有指定 `minHeight`选项的 dialog：

```
$( ".selector" ).dialog({ minHeight: 200 }); 
```

在初始化后，获取或设置`minHeight` 选项：

```
// getter
var minHeight = $( ".selector" ).dialog( "option", "minHeight" );

// setter
$( ".selector" ).dialog( "option", "minHeight", 200 ); 
```

### minWidth**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `150`dialog 可以调整的最小宽度，以像素为单位。**Code examples:**

初始化带有指定 `minWidth`选项的 dialog：

```
$( ".selector" ).dialog({ minWidth: 200 }); 
```

在初始化后，获取或设置`minWidth` 选项：

```
// getter
var minWidth = $( ".selector" ).dialog( "option", "minWidth" );

// setter
$( ".selector" ).dialog( "option", "minWidth", 200 ); 
```

### modal**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为`true`，该 dialog 将会有遮罩层; 页面上的其他项目将被禁用， 即，不能交互。 遮罩层创建对话框下方，但高于其它页面元素。**Code examples:**

初始化带有指定 `modal`选项的 dialog：

```
$( ".selector" ).dialog({ modal: true }); 
```

在初始化后，获取或设置`modal` 选项：

```
// getter
var modal = $( ".selector" ).dialog( "option", "modal" );

// setter
$( ".selector" ).dialog( "option", "modal", true ); 
```

### position**Type:** [Object](http://api.jquery.com/Types/#Object) or [String](http://api.jquery.com/Types/#String) or [Array](http://api.jquery.com/Types/#Array)

**Default:** `{ my: "center", at: "center", of: window }`

指定 dialog 显示的位置。该 dialog 将会处理冲突 ，使得尽可能多的 dialog 尽可能地可见。

*注意: 不赞成使用 `String` 和 `Array` 格式。*

**支持多个类型：**

*   **Object**: 确定 dialog 打开时的位置。 `of`选项默认为窗口， 但您可以指定其他元素定位。 你可以参考 jQuery UI Position 实用工具，了解各种选项的更多细节。
*   **String**:一个字符串，表示可视区内的位置。可能的值：`"center"`, `"left"`, `"right"`, `"top"`, `"bottom"`.
*   **Array**: 一个包含相对于可见区域左上角*x, y*偏移坐标（单位为像素） 的数组， 或 一个可能值的字符串名称。

**Code examples:**

初始化带有指定 `position`选项的 dialog：

```
$( ".selector" ).dialog({ position: { my: "left top", at: "left bottom", of: button } }); 
```

在初始化后，获取或设置`position` 选项：

```
// getter
var position = $( ".selector" ).dialog( "option", "position" );

// setter
$( ".selector" ).dialog( "option", "position", { my: "left top", at: "left bottom", of: button } ); 
```

### resizable**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `true`如果设置为`true`， 那么 dialog 允许调整大小。需要包含 jQuery UI Resizable widget。**Code examples:**

初始化带有指定 `resizable`选项的 dialog：

```
$( ".selector" ).dialog({ resizable: false }); 
```

在初始化后，获取或设置`resizable` 选项：

```
// getter
var resizable = $( ".selector" ).dialog( "option", "resizable" );

// setter
$( ".selector" ).dialog( "option", "resizable", false ); 
```

### show**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String) or [Object](http://api.jquery.com/Types/#Object)

**Default:** `null`dialog 打开（显示）时的动画效果。**支持多个类型：**

*   **Boolean**: 当设置为`false`， 将不使用动画效果，该 dialog 会立即被隐藏。 如果设置为`true`， 该 dialog 将会以默认的持续时间和默认的效果淡出。
*   **Number**: 该 dialog 将以指定的时间和默认的效果淡出。
*   **String**: 该 dialog 将使用指定的效果被隐藏。 该值可以是一个 jQuery 内置的动画方法的名称， 如`"slideUp"`， 或一个 jQuery UI 效果的名称， 如`"fold"`。 在这两种情况下，将使用默认持续时间和默认的动画效果。
*   **Object**: 如果该值是一个对象， 那么 `effect`, `delay`, `duration`, 和`easing`可能要提供。 如果 `effect` 属性包含一个 jQuery 方法的名称， 那么该方法将被使用; 否则它被假定为是一个 jQuery UI 的效果的名称。 当使用 jQuery UI 支持额外设置 的效果 ， 你可以在对象中包含那些设置 并且它们将被传递到的效果。如果`duration`持续时间或`easing`属性被省略， 那么默认值将被使用。 如果`effect`被省略， 那么`"fadeOut"` 将被使用。如果`delay`被省略， 那么将不使用延迟。

**Code examples:**

初始化带有指定 `show`选项的 dialog：

```
$( ".selector" ).dialog({ show: { effect: "blind", duration: 800 } }); 
```

在初始化后，获取或设置`show` 选项：

```
// getter
var show = $( ".selector" ).dialog( "option", "show" );

// setter
$( ".selector" ).dialog( "option", "show", { effect: "blind", duration: 800 } ); 
```

### title**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `null`指定 dialog 的标题文字。 如果值为`null`,那么该 dialog 元素上的`title`属性将被使用。**Code examples:**

初始化带有指定 `title`选项的 dialog：

```
$( ".selector" ).dialog({ title: "Dialog Title" }); 
```

在初始化后，获取或设置`title` 选项：

```
// getter
var title = $( ".selector" ).dialog( "option", "title" );

// setter
$( ".selector" ).dialog( "option", "title", "Dialog Title" ); 
```

### width**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `300`设置 dialog 的宽度（单位：像素）。**Code examples:**

初始化带有指定 `width`选项的 dialog：

```
$( ".selector" ).dialog({ width: 500 }); 
```

在初始化后，获取或设置`width` 选项：

```
// getter
var width = $( ".selector" ).dialog( "option", "width" );

// setter
$( ".selector" ).dialog( "option", "width", 500 ); 
```

## Methods

### close()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

关闭 dialog.

*   该方法不接受任何参数。

**Code examples:**

调用 close 方法：

```
$( ".selector" ).dialog( "close" ); 
```

### destroy()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

完全移除 dialog 功能. 这将使元素返回到之前的初始化状态.

*   该方法不接受任何参数。

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).dialog( "destroy" ); 
```

### isOpen()Returns: [Boolean](http://api.jquery.com/Types/#Boolean)

确定 dialog 当前是否打开状态。

*   该方法不接受任何参数。

**Code examples:**

调用 isOpen 方法：

```
var isOpen = $( ".selector" ).dialog( "isOpen" ); 
```

### moveToTop()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

移动 dialog 到所有 dialog 堆栈的顶部。（愚人码头注：理解为 z-index 层级最高）

*   该方法不接受任何参数。

**Code examples:**

调用 moveToTop 方法：

```
$( ".selector" ).dialog( "moveToTop" ); 
```

### open()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

打开 dialog。

*   该方法不接受任何参数。

**Code examples:**

调用 open 方法：

```
$( ".selector" ).dialog( "open" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取当前与指定的 `optionName` 关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项的名称。

**Code examples:**

调用该方法：

```
var isDisabled = $( ".selector" ).dialog( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含键/值对的对象，键/值对表示当前 dialog 选项哈希。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
var options = $( ".selector" ).dialog( "option" ); 
```

### option( optionName, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置与指定的 `optionName` 关联的 dialog 选项的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的值。

**Code examples:**

调用该方法：

```
$( ".selector" ).dialog( "option", "disabled", true ); 
```

### option( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

为 dialog 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的 option-value 对。

**Code examples:**

调用该方法：

```
$( ".selector" ).dialog( "option", { disabled: true } ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个包含 生成包裹元素 的 `jQuery` 对象。

*   该方法不接受任何参数。

**Code examples:**

调用 widget 方法：

```
var widget = $( ".selector" ).dialog( "widget" ); 
```

## 扩展点（Extension Points）

dialog 小部件是[widget factory](http://www.css88.com/jquery-ui-api/jQuery.widget/)构建的，并且可以扩展。 当扩展部件时， 你必须覆盖或添加新的行为到现有的方法。 下列方法被提供作为扩展点 用相同的 API 稳定性如上所列的 plugin methods。 有关小部件扩展的更多信息， 请参阅[使用 Widget Factory 扩展小部件](http://learn.jquery.com/jquery-ui/widget-factory/extending-widgets/)。

### _allowInteraction( event )Returns: [Boolean](http://api.jquery.com/Types/#Boolean)

带遮罩的对话框不允许用户与对话框下面元素进行交互。 这可能会对 不属于该 dialog 的子元素那些绝对定位的其他元素产生问题。 `_allowInteraction()`方法确定用户是否应被允许与给定的目标元素进行交互; 因此， 它可用于不属于该 dialog 的子元素白名单中的元素 但你希望用户能够使用。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)

**Code examples:**

允许 Select2 插件在遮罩对话框中使用。 `_super()`调用确保该对话框中的元素仍然可以交互。

```
_allowInteraction: function( event ) {
  return !!$( event.target ).is( ".select2-input" ) || this._super( event );
} 
```

## Events

### beforeClose( event, ui )Type: `dialogbeforeclose`

当 dialog 即将关闭时触发。 如果取消，dialog 将不会关闭。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 beforeClose 回调的 dialog：

```
$( ".selector" ).dialog({
  beforeClose: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 dialogbeforeclose 事件：

```
$( ".selector" ).on( "dialogbeforeclose", function( event, ui ) {} ); 
```

### close( event, ui )Type: `dialogclose`

当 dialog 关闭时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 close 回调的 dialog：

```
$( ".selector" ).dialog({
  close: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 dialogclose 事件：

```
$( ".selector" ).on( "dialogclose", function( event, ui ) {} ); 
```

### create( event, ui )Type: `dialogcreate`

在创建 dialog 时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 create 回调的 dialog：

```
$( ".selector" ).dialog({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 dialogcreate 事件：

```
$( ".selector" ).on( "dialogcreate", function( event, ui ) {} ); 
```

### drag( event, ui )Type: `dialogdrag`

在 dialog 正在被拖动时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)dialog 当前的 CSS position（位置）对象。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)dialog 当前的 offset position（偏移位置）对象。

**Code examples:**

初始化带有指定 drag 回调的 dialog：

```
$( ".selector" ).dialog({
  drag: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 dialogdrag 事件：

```
$( ".selector" ).on( "dialogdrag", function( event, ui ) {} ); 
```

### dragStart( event, ui )Type: `dialogdragstart`

当用户开始拖动 dialog 时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)dialog 当前的 CSS position（位置）对象。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)dialog 当前的 offset position（偏移位置）对象。

**Code examples:**

初始化带有指定 dragStart 回调的 dialog：

```
$( ".selector" ).dialog({
  dragStart: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 dialogdragstart 事件：

```
$( ".selector" ).on( "dialogdragstart", function( event, ui ) {} ); 
```

### dragStop( event, ui )Type: `dialogdragstop`

当 dialog 停止拖动时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)dialog 当前的 CSS position（位置）对象。
    *   **offset**Type: [Object](http://api.jquery.com/Types/#Object)dialog 当前的 offset position（偏移位置）对象。

**Code examples:**

初始化带有指定 dragStop 回调的 dialog：

```
$( ".selector" ).dialog({
  dragStop: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 dialogdragstop 事件：

```
$( ".selector" ).on( "dialogdragstop", function( event, ui ) {} ); 
```

### focus( event, ui )Type: `dialogfocus`

当对话框获取焦点时触发此事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 focus 回调的 dialog：

```
$( ".selector" ).dialog({
  focus: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 dialogfocus 事件：

```
$( ".selector" ).on( "dialogfocus", function( event, ui ) {} ); 
```

### open( event, ui )Type: `dialogopen`

当对话框打开后，触发此事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 open 回调的 dialog：

```
$( ".selector" ).dialog({
  open: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 dialogopen 事件：

```
$( ".selector" ).on( "dialogopen", function( event, ui ) {} ); 
```

### resize( event, ui )Type: `dialogresize`

当对话框大小改变时，触发此事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)对话框被调整大小 之前的 CSS position（位置）对象 。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)对话框当前的 CSS position（位置）对象。
    *   **originalSize**Type: [Object](http://api.jquery.com/Types/#Object)对话框被调整大小 之前的 size（尺寸）对象 。
    *   **size**Type: [Object](http://api.jquery.com/Types/#Object)对话框当前的 size（尺寸）对象。

**Code examples:**

初始化带有指定 resize 回调的 dialog：

```
$( ".selector" ).dialog({
  resize: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 dialogresize 事件：

```
$( ".selector" ).on( "dialogresize", function( event, ui ) {} ); 
```

### resizeStart( event, ui )Type: `dialogresizestart`

当开始改变对话框大小时，触发此事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)对话框被调整大小 之前的 CSS position（位置）对象 。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)对话框当前的 CSS position（位置）对象。
    *   **originalSize**Type: [Object](http://api.jquery.com/Types/#Object)对话框被调整大小 之前的 size（尺寸）对象 。
    *   **size**Type: [Object](http://api.jquery.com/Types/#Object)对话框当前的 size（尺寸）对象。

**Code examples:**

初始化带有指定 resizeStart 回调的 dialog：

```
$( ".selector" ).dialog({
  resizeStart: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 dialogresizestart 事件：

```
$( ".selector" ).on( "dialogresizestart", function( event, ui ) {} ); 
```

### resizeStop( event, ui )Type: `dialogresizestop`

当对话框改变大小后，触发此事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **originalPosition**Type: [Object](http://api.jquery.com/Types/#Object)对话框被调整大小 之前的 CSS position（位置）对象 。
    *   **position**Type: [Object](http://api.jquery.com/Types/#Object)对话框当前的 CSS position（位置）对象。
    *   **originalSize**Type: [Object](http://api.jquery.com/Types/#Object)对话框被调整大小 之前的 size（尺寸）对象 。
    *   **size**Type: [Object](http://api.jquery.com/Types/#Object)对话框当前的 size（尺寸）对象。

**Code examples:**

初始化带有指定 resizeStop 回调的 dialog：

```
$( ".selector" ).dialog({
  resizeStop: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 dialogresizestop 事件：

```
$( ".selector" ).on( "dialogresizestop", function( event, ui ) {} ); 
```

## Example:

#### 一个简单的 jQuery UI 对话框（Dialog）。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>dialog demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<button id="opener">open the dialog</button>
<div id="dialog" title="Dialog Title">I'm a dialog</div>

<script>
$( "#dialog" ).dialog({ autoOpen: false });
$( "#opener" ).click(function() {
  $( "#dialog" ).dialog( "open" );
});
</script>

</body>
</html> 
```

# Menu Widget

Categories: [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## version added: 1.9

**Description:** 带有鼠标和键盘交互的用于导航的可主题化菜单。

## QuickNavExamples

### Options

*   disabled
*   icons
*   menus
*   position
*   role

### Methods

*   blur
*   collapse
*   collapseAll
*   destroy
*   disable
*   enable
*   expand
*   focus
*   isFirstItem
*   isLastItem
*   next
*   nextPage
*   option
*   previous
*   previousPage
*   refresh
*   select
*   widget

### Events

*   blur
*   create
*   focus
*   select

菜单可以用任何有效的标记创建，只要元素有严格的父/子关系且每个条目都有一个锚。最常用的元素是无序列表（`&lt;ul&gt;`）：

```
<ul id="menu">
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a>
    <ul>
      <li><a href="#">Item 3-1</a></li>
      <li><a href="#">Item 3-2</a></li>
      <li><a href="#">Item 3-3</a></li>
      <li><a href="#">Item 3-4</a></li>
      <li><a href="#">Item 3-5</a></li>
    </ul>
  </li>
  <li><a href="#">Item 4</a></li>
  <li><a href="#">Item 5</a></li>
</ul> 
```

如果使用一个非 `&lt;ul&gt;`/`&lt;li&gt;` 的结构，为菜单和菜单条目使用相同的元素，请使用 `menus` 选项来区分两个元素，例如 `menus: "div.menuElement"`。

可通过向元素添加 `ui-state-disabled` class 来禁用任何菜单条目。

### 图标（Icons）

为了向菜单添加图标，请在标记中包含图标：

```
<ul id="menu">
  <li><a href="#"><span class="ui-icon ui-icon-disk"></span>Save</a></li>
</ul> 
```

菜单（Menu）会自动向无图标的条目添加必要的内边距。

### 分隔符（Dividers）

分隔符元素可通过包含未链接的菜单条目来创建，菜单条目只能是空格/破折号：

```
<ul id="menu">
  <li><a href="#">Item 1</a></li>
  <li>-</li>
  <li><a href="#">Item 2</a></li>
</ul> 
```

### 键盘交互（Keyboard interaction）

*   ENTER/SPACE：调用获得焦点的菜单项的动作，可能会打开一个子菜单。
*   UP：移动教导到上一个菜单项。
*   DOWN：移动教导到下一个菜单项。
*   RIGHT：如果可用，则打开子菜单。
*   LEFT：关闭当前子菜单，移动焦点到父菜单项。如果焦点不在子菜单上，则不进行任何操作。
*   ESCAPE：关闭当前子菜单，移动焦点到父菜单项。如果焦点不在子菜单上，则不进行任何操作。

输入一个字母，移动焦点到以该字母开头的第一个条目。重复相同的字符会循环显示匹配的条目。在一个时间内输入更多的字符则匹配所输入的字符。

禁用项可获得键盘焦点，但是不允许任何交互。

### 主题化（Theming）

菜单部件（Menu Widget）使用 jQuery UI CSS 框架 来定义它的外观和感观的样式。如果需要使用菜单指定的样式，则可以使用下面的 CSS class 名称：

*   `ui-menu`：菜单的外层容器。如果菜单包含图标，该元素会另外带有一个 `ui-menu-icons` class。
    *   `ui-menu-item`：单个菜单项的容器。
        *   `ui-menu-icon`：通过 `icons` 选项进行子菜单图标设置。
    *   `ui-menu-divider`：菜单项之间的分隔符元素。

### 依赖（Dependencies）

*   UI 核心（UI Core）
*   部件库（Widget Factory）
*   定位（Position）

### 其他注意事项（Additional Notes:）

*   该部件要求一些功能性的 CSS，否则将无法工作。如果您创建了一个自定义的主题，请使用小部件指定的 CSS 文件作为起点。

## Options

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为 `true`，则禁用该 menu（菜单）。**Code examples:**

初始化带有指定 `disabled`选项的 menu（菜单）

```
$( ".selector" ).menu({ disabled: true }); 
```

在初始化后，获取或设置`disabled` 选项：

```
// getter
var disabled = $( ".selector" ).menu( "option", "disabled" );

// setter
$( ".selector" ).menu( "option", "disabled", true ); 
```

### icons**Type:** [Object](http://api.jquery.com/Types/#Object)

**Default:** `{ submenu: "ui-icon-carat-1-e" }`标题要使用的图标，与 jQuery UI CSS 框架提供的图标（Icons） 匹配。设置为 false 则不显示图标。

*   submenu (string, default: "ui-icon-carat-1-e")

**Code examples:**

初始化带有指定 `icons`选项的 menu（菜单）

```
$( ".selector" ).menu({ icons: { submenu: "ui-icon-circle-triangle-e" } }); 
```

在初始化后，获取或设置`icons` 选项：

```
// getter
var icons = $( ".selector" ).menu( "option", "icons" );

// setter
$( ".selector" ).menu( "option", "icons", { submenu: "ui-icon-circle-triangle-e" } ); 
```

### menus**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"ul"`

作为 menu（菜单）容器的元素的选择器， 包括子菜单。

**注意:** 初始化后 `menus`选项不应该被更改。 现有的子菜单将不会被更新。**Code examples:**

初始化带有指定 `menus`选项的 menu（菜单）

```
$( ".selector" ).menu({ menus: "div" }); 
```

获取 `menus` 选项：

```
// getter
var menus = $( ".selector" ).menu( "option", "menus" ); 
```

### position**Type:** [Object](http://api.jquery.com/Types/#Object)

**Default:** `{ my: "left top", at: "right top" }`标识建议菜单的位置与相关的 input 元素有关系。`of` 选项默认为 input 元素，但是您可以指定另一个定位元素。如需了解各种选项的更多细节，请查看 jQuery UI Position。**Code examples:**

初始化带有指定 `position`选项的 menu（菜单）

```
$( ".selector" ).menu({ position: { my: "left top", at: "right-5 top+5" } }); 
```

在初始化后，获取或设置`position` 选项：

```
// getter
var position = $( ".selector" ).menu( "option", "position" );

// setter
$( ".selector" ).menu( "option", "position", { my: "left top", at: "right-5 top+5" } ); 
```

### role**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"menu"`

自定义用于菜单和菜单项的 ARIA roles（愚人码头注：关于[ARIA roles](http://www.w3.org/TR/wai-aria/roles)）。 在默认情况下菜单项使用`"menuitem"`。 设置`role`选项为了使`"listbox"`使用`"option"`作为菜单项。 如果设置为`null`， 没有 roles 将被设置，如果菜单是由被保持焦点另一个元件控制时候，非常有用。

**注意:** 初始化后`role`选项 不应该被更改。 现有（子）菜单和菜单项将不会被更新。**Code examples:**

初始化带有指定 `role`选项的 menu（菜单）

```
$( ".selector" ).menu({ role: null }); 
```

获取 `role` 选项：

```
// getter
var role = $( ".selector" ).menu( "option", "role" ); 
```

## Methods

### blur( [event ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

从菜单中删除焦点， 重置任何激活样式 和 触发菜单的 `blur` 事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)什么事件触发了菜单失去焦点。

**Code examples:**

调用 blur 方法：

```
$( ".selector" ).menu( "blur" ); 
```

### collapse( [event ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

关闭当前活动的子菜单。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)什么事件触发关闭子菜单

**Code examples:**

调用 collapse 方法：

```
$( ".selector" ).menu( "collapse" ); 
```

### collapseAll( [event ] [, all ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

关闭全部打开的子菜单。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)什么事件触发关闭子菜单。
*   **all**Type: [Boolean](http://api.jquery.com/Types/#Boolean)表示所有子菜单是否应该被关闭 或 只有子菜单中包括的菜单 或 包含触发事件的目标元素。

**Code examples:**

调用 collapseAll 方法：

```
$( ".selector" ).menu( "collapseAll", null, true ); 
```

### destroy()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

完全移除 menu 功能. 这将使元素返回到之前的初始化状态.

*   该方法不接受任何参数。

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).menu( "destroy" ); 
```

### disable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

禁用 menu.

*   该方法不接受任何参数。

**Code examples:**

调用 disable 方法：

```
$( ".selector" ).menu( "disable" ); 
```

### enable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

启用 menu.

*   该方法不接受任何参数。

**Code examples:**

调用 enable 方法：

```
$( ".selector" ).menu( "enable" ); 
```

### expand( [event ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

打开当前活动项目下的子菜单下，如果有的话。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)什么时间触发打开子菜单。

**Code examples:**

调用 expand 方法：

```
$( ".selector" ).menu( "expand" ); 
```

### focus( [event ], item )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

激活一个特定的菜单项， 首先，如果打开存在的任何子菜单，并触发菜单的`focus`事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)什么事件触发了菜单项获得焦点。
*   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)要获取焦点/激活的菜单项

**Code examples:**

调用 focus 方法：

```
$( ".selector" ).menu( "focus", null, menu.find( ".ui-menu-item:last" ) ); 
```

### isFirstItem()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

返回一个布尔值，说明当前活动项目是否菜单的第一项。

*   该方法不接受任何参数。

**Code examples:**

调用 isFirstItem 方法：

```
var firstItem = $( ".selector" ).menu( "isFirstItem" ); 
```

### isLastItem()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

返回一个布尔值，说明当前活动项目是否菜单的最后一项。

*   该方法不接受任何参数。

**Code examples:**

调用 isLastItem 方法：

```
var lastItem = $( ".selector" ).menu( "isLastItem" ); 
```

### next( [event ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

移动激活状态到下一个菜单项。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)什么事件触发焦点转移。

**Code examples:**

调用 next 方法：

```
$( ".selector" ).menu( "next" ); 
```

### nextPage( [event ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

移动激活状态到第一个菜单项下的可滚动菜单的底部，或最后一个项目，如果不可滚动。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)什么事件触发焦点转移。

**Code examples:**

调用 nextPage 方法：

```
$( ".selector" ).menu( "nextPage" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取当前与指定的 `optionName` 关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项的名称。

**Code examples:**

调用该方法：

```
var isDisabled = $( ".selector" ).menu( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含键/值对的对象，键/值对表示当前 menu 选项哈希。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
var options = $( ".selector" ).menu( "option" ); 
```

### option( optionName, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置与指定的 `optionName` 关联的 menu 选项的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的值。

**Code examples:**

调用该方法：

```
$( ".selector" ).menu( "option", "disabled", true ); 
```

### option( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

为 menu 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的 option-value 对。

**Code examples:**

调用该方法：

```
$( ".selector" ).menu( "option", { disabled: true } ); 
```

### previous( [event ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

移动激活状态到上一个菜单项。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)什么事件触发焦点转移。

**Code examples:**

调用 previous 方法：

```
$( ".selector" ).menu( "previous" ); 
```

### previousPage( [event ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

移动激活状态到第一个菜单项下的可滚动菜单的顶部，或第一一个项目，如果不可滚动。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)什么事件触发焦点转移。

**Code examples:**

调用 previousPage 方法：

```
$( ".selector" ).menu( "previousPage" ); 
```

### refresh()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

初始化还没有被初始化的子菜单和菜单项。 新的菜单项， 包括子菜单可以被添加到菜单 或 所有的菜单的内容可以被替换 然后使用`refresh()`方法初始化。

*   该方法不接受任何参数。

**Code examples:**

调用 refresh 方法：

```
$( ".selector" ).menu( "refresh" ); 
```

### select( [event ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

选择当前活动的菜单项， 折叠所有子菜单 并触发菜单中的 `select` 事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)什么事件触发选择。

**Code examples:**

调用 select 方法：

```
$( ".selector" ).menu( "select" ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个包含 button 的 `jQuery` 对象。

*   该方法不接受任何参数。

**Code examples:**

调用 widget 方法：

```
var widget = $( ".selector" ).menu( "widget" ); 
```

## Events

### blur( event, ui )Type: `menublur`

当 menu 失去焦点时触发这个事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)当前激活的菜单项。

**Code examples:**

初始化带有指定 blur 回调的 menu：

```
$( ".selector" ).menu({
  blur: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 menublur 事件：

```
$( ".selector" ).on( "menublur", function( event, ui ) {} ); 
```

### create( event, ui )Type: `menucreate`

当创建 menu 时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 create 回调的 menu：

```
$( ".selector" ).menu({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 menucreate 事件：

```
$( ".selector" ).on( "menucreate", function( event, ui ) {} ); 
```

### focus( event, ui )Type: `menufocus`

当当一个菜单获得焦点或当任意一个菜单项被激活时触发这个事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)当前激活的菜单项。

**Code examples:**

初始化带有指定 focus 回调的 menu：

```
$( ".selector" ).menu({
  focus: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 menufocus 事件：

```
$( ".selector" ).on( "menufocus", function( event, ui ) {} ); 
```

### select( event, ui )Type: `menuselect`

当才安被选中的时候触发该事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **item**Type: [jQuery](http://api.jquery.com/Types/#jQuery)当前激活的菜单项。

**Code examples:**

初始化带有指定 select 回调的 menu：

```
$( ".selector" ).menu({
  select: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 menuselect 事件：

```
$( ".selector" ).on( "menuselect", function( event, ui ) {} ); 
```

## Example:

#### 一个简单的 jQuery UI Menu

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>menu demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <style>
  .ui-menu {
    width: 200px;
  }
  </style>
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<ul id="menu">
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a>
    <ul>
      <li><a href="#">Item 3-1</a></li>
      <li><a href="#">Item 3-2</a></li>
      <li><a href="#">Item 3-3</a></li>
      <li><a href="#">Item 3-4</a></li>
      <li><a href="#">Item 3-5</a></li>
    </ul>
  </li>
  <li><a href="#">Item 4</a></li>
  <li><a href="#">Item 5</a></li>
</ul>

<script>
$( "#menu" ).menu();
</script>

</body>
</html> 
```

# Progressbar Widget

Categories: [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## version added: 1.6

**Description:** 显示一个确定的或不确定的进程状态。

## QuickNavExamples

### Options

*   disabled
*   max
*   value

### Methods

*   destroy
*   disable
*   enable
*   option
*   value
*   widget

### Events

*   change
*   complete
*   create

进度条被设计来显示进度的当前完成百分比。进度条通过 CSS 编码灵活调整大小，默认会缩放到适应父容器的大小。

一个确定的进度条只能在系统可以准确更新当前状态的情况下使用。一个确定的进度条不会从左向右填充，然后循环回到空 - 如果不能计算实际状态，则使用不确定的进度条以便提供用户反馈。

### 主题（Theming）

进度条部件（Progressbar Widget）使用 jQuery UI CSS 框架 来定义它的外观和感观的样式。如果需要使用进度条指定的样式，则可以使用下面的 CSS class 名称：

*   `ui-progressbar`：进度条的外层容器。该元素会为不确定的进度条另外添加一个 `ui-progressbar-indeterminate` class。
    *   `ui-progressbar-value`：该元素代表进度条的填充部分。
        *   `ui-progressbar-overlay`：用于为不确定的进度条显示动画的覆盖层。

### 依赖（Dependencies）

*   UI 核心（UI Core）
*   部件库（Widget Factory）

### 其他注意事项（Additional Notes）:

*   该部件要求一些功能性的 CSS，否则将无法工作。如果您创建了一个自定义的主题，请使用小部件指定的 CSS 文件作为起点。

## Options

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为 `true`，则禁用该 progressbar（进度条）。 **Code examples:**

初始化带有指定`disabled`选项的 progressbar（进度条）：

```
$( ".selector" ).progressbar({ disabled: true }); 
```

在初始化后，获取或设置`disabled` 选项：

```
// getter
var disabled = $( ".selector" ).progressbar( "option", "disabled" );

// setter
$( ".selector" ).progressbar( "option", "disabled", true ); 
```

### max**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `100`progressbar（进度条）的最大值。**Code examples:**

初始化带有指定`max`选项的 progressbar（进度条）：

```
$( ".selector" ).progressbar({ max: 1024 }); 
```

在初始化后，获取或设置`max` 选项：

```
// getter
var max = $( ".selector" ).progressbar( "option", "max" );

// setter
$( ".selector" ).progressbar( "option", "max", 1024 ); 
```

### value**Type:** [Number](http://api.jquery.com/Types/#Number) or [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `0`progressbar（进度条）的进度值.**支持多个类型：**

*   **Number**: `0` 到 `max`之间的值.
*   **Boolean**:值可以设置为`false` 来创建一个不确定的 progressbar（进度条）。

**Code examples:**

初始化带有指定`value`选项的 progressbar（进度条）：

```
$( ".selector" ).progressbar({ value: 25 }); 
```

在初始化后，获取或设置`value` 选项：

```
// getter
var value = $( ".selector" ).progressbar( "option", "value" );

// setter
$( ".selector" ).progressbar( "option", "value", 25 ); 
```

## Methods

### destroy()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

完全移除 progressbar（进度条） 功能。这会把元素返回到它的预初始化状态。

*   该方法不接受任何参数。

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).progressbar( "destroy" ); 
```

### disable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

禁用 progressbar（进度条） 。

*   该方法不接受任何参数。

**Code examples:**

调用 disable 方法：

```
$( ".selector" ).progressbar( "disable" ); 
```

### enable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

启用 progressbar（进度条） 。

*   该方法不接受任何参数。

**Code examples:**

调用 enable 方法：

```
$( ".selector" ).progressbar( "enable" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取当前与指定的 `optionName` 关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项的名称。

**Code examples:**

调用该方法：

```
var isDisabled = $( ".selector" ).progressbar( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含键/值对的对象，键/值对表示当前 progressbar 选项哈希。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
var options = $( ".selector" ).progressbar( "option" ); 
```

### option( optionName, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置与指定的 `optionName` 关联的 progressbar 选项的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的值。

**Code examples:**

调用该方法：

```
$( ".selector" ).progressbar( "option", "disabled", true ); 
```

### option( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

为 progressbar（进度条） 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的 option-value 对。

**Code examples:**

调用该方法：

```
$( ".selector" ).progressbar( "option", { disabled: true } ); 
```

### value()Returns: [Number](http://api.jquery.com/Types/#Number) or [Boolean](http://api.jquery.com/Types/#Boolean)

获取 progressbar（进度条）的当前值。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
var progressSoFar = $( ".selector" ).progressbar( "value" ); 
```

### value( value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置 progressbar（进度条）的当前值。

*   **value**Type: [Number](http://api.jquery.com/Types/#Number) or [Boolean](http://api.jquery.com/Types/#Boolean)用来设置的值。有效值的详细描述查看`value` 选项。

**Code examples:**

调用该方法：

```
$( ".selector" ).progressbar( "value", 50 ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个 progressbar（进度条） 的`jQuery`对象。

*   该方法不接受任何参数。

**Code examples:**

调用 widget 方法：

```
var widget = $( ".selector" ).progressbar( "widget" ); 
```

## Events

### change( event, ui )Type: `progressbarchange`

当 progressbar（进度条） 的值改变的时候触发该事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 change 回调的 progressbar（进度条）：

```
$( ".selector" ).progressbar({
  change: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 progressbarchange 事件：

```
$( ".selector" ).on( "progressbarchange", function( event, ui ) {} ); 
```

### complete( event, ui )Type: `progressbarcomplete`

当 progressbar（进度条）达到最大值时触发该事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 complete 回调的 progressbar（进度条）：

```
$( ".selector" ).progressbar({
  complete: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 progressbarcomplete 事件：

```
$( ".selector" ).on( "progressbarcomplete", function( event, ui ) {} ); 
```

### create( event, ui )Type: `progressbarcreate`

当 progressbar（进度条）被创建时触发该事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 create 回调的 progressbar（进度条）：

```
$( ".selector" ).progressbar({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 progressbarcreate 事件：

```
$( ".selector" ).on( "progressbarcreate", function( event, ui ) {} ); 
```

## Examples:

#### Example: 一个简单的 jQuery UI Progressbar

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>progressbar demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<div id="progressbar"></div>

<script>
$( "#progressbar" ).progressbar({
  value: 37
});
</script>

</body>
</html> 
```

#### Example: 一个简单的 jQuery UI 不确定的进度条（Indeterminate Progressbar）。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>progressbar demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<div id="progressbar"></div>

<script>
$( "#progressbar" ).progressbar({
  value: false
});
</script>

</body>
</html> 
```

# Slider Widget

Categories: [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## version added: 1.5

**Description:** 拖动手柄以选择一个数值。

## QuickNavExamples

### Options

*   animate
*   disabled
*   max
*   min
*   orientation
*   range
*   step
*   value
*   values

### Methods

*   destroy
*   disable
*   enable
*   option
*   value
*   values
*   widget

### Events

*   change
*   create
*   slide
*   start
*   stop

jQuery UI Slider 插件使所选择的元素成为一个滑块(slider). 可以多种选项,例如多个操作手柄和操作范围。 手柄可以被鼠标拖动或者随着方向键移动。

slider 小工具将在初始化的时候根据 `ui-slider-handle`样式名创建手柄元素。您可以在初始化前通过创建和追加的方式，或者在元素上添加`ui-slider-handle` 样式来自定义手柄元素。 这只会创建需要匹配`value`/`values`的手柄数值个数。例如，如果您指定的`值: [ 1, 5, 18 ]`，并创建一个自定义手柄，该插件将创建另外两个。

### 主题(Theming)

slider 小工具使用 jQuery UI CSS framework 样式的外观和感觉。如果滑块具体样式是必须的，你可以用下面的 CSS 类名：

*   `ui-slider`: 滑块控件的轨道。该元素将追加一个`ui-slider-horizontal` 或 `ui-slider-vertical`样式名，这取决于 slider 小工具是横向还是纵向的。另外具有 UI 的滑块水平或 UI 滑块垂直取决于`orientation`参数，表示滑块的取向的类名。
    *   `ui-slider-handle`: 滑块手柄.
    *   `ui-slider-range`: 当设置 选项时使用的已选范围。如果 `range` 选项设置为 `"min"` 或者 `"max"`，则该元素会分别另外带有一个 `ui-slider-range-min` 或 `ui-slider-range-max` 类。

### 依赖

*   UI 核心（UI Core）
*   部件库（Widget Factory）
*   鼠标交互（Mouse Interaction）

### 其他注意事项:

*   该部件要求一些功能性的 CSS，否则将无法工作。如果您创建了一个自定义的主题，请使用小部件指定的 CSS 文件作为起点。

## 选项

### animate**类型:** [Boolean](http://api.jquery.com/Types/#Boolean) or [String](http://api.jquery.com/Types/#String) or [Number](http://api.jquery.com/Types/#Number)

**默认值:** `false`当用户单击滑块轨道时是否平稳地滑动手柄。 也可以接受任何有效的动画持续时间。**多种类型支持：**

*   **Boolean**: 当设置为 `true`时, 滑动手柄将以默认的持续时间执行动画。
*   **String**: 速度的名称, 比如 `"fast"` 或 `"slow"`。
*   **Number**: 动画持续时间, 以毫秒为单位。

**代码示例:**

使用指定`animate`选项初始化滑块：

```
$( ".selector" ).slider({ animate: "fast" }); 
```

初始化后，获取或者设置`animate`选项:

```
// getter
var animate = $( ".selector" ).slider( "option", "animate" );

// setter
$( ".selector" ).slider( "option", "animate", "fast" ); 
```

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为`true`，则禁用滑块。**Code examples:**

使用`disabled`选项初始化滑块组件：

```
$( ".selector" ).slider({ disabled: true }); 
```

在组件初始化之后，读取或设置 `disabled` 选项：

```
// getter
var disabled = $( ".selector" ).slider( "option", "disabled" );

// setter
$( ".selector" ).slider( "option", "disabled", true ); 
```

### max**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `100`滑块的最大值。**Code examples:**

使用`max`选项初始化滑块组件：

```
$( ".selector" ).slider({ max: 50 }); 
```

在组件初始化之后，读取或设置 `max` 选项：

```
// getter
var max = $( ".selector" ).slider( "option", "max" );

// setter
$( ".selector" ).slider( "option", "max", 50 ); 
```

### min**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `0`滑块的最小值**Code examples:**

使用`min`选项初始化滑块组件：

```
$( ".selector" ).slider({ min: 10 }); 
```

在组件初始化之后，读取或设置 `min` 选项：

```
// getter
var min = $( ".selector" ).slider( "option", "min" );

// setter
$( ".selector" ).slider( "option", "min", 10 ); 
```

### orientation**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"horizontal"`确定滑块手柄 将 水平（最小在左，最大在右）或垂直（最小在底部，最大在顶部）移动。（愚人码头注：就是滑块的方向，横向或纵向）可能的值：`"horizontal"`（横向）, `"vertical"`（纵向）。**Code examples:**

使用`orientation`选项初始化滑块组件：

```
$( ".selector" ).slider({ orientation: "vertical" }); 
```

在组件初始化之后，读取或设置 `orientation` 选项：

```
// getter
var orientation = $( ".selector" ).slider( "option", "orientation" );

// setter
$( ".selector" ).slider( "option", "orientation", "vertical" ); 
```

### range**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [String](http://api.jquery.com/Types/#String)

**Default:** `false`滑块是否表现为一个范围。**多种类型支持：**

*   **Boolean**: 如果设置为`true`,如果你有两个手柄，slider 将会感应到他们之间各种可能的范围要素。
*   **String**: 或者他们是`"min"` 或者 `"max"`值。最小的范围将从 slider 的最小值传递给操作柄。最大的范围将从 slider 的最大值传递给操作柄

**Code examples:**

使用`range`选项初始化滑块组件：

```
$( ".selector" ).slider({ range: true }); 
```

在组件初始化之后，读取或设置 `range` 选项：

```
// getter
var range = $( ".selector" ).slider( "option", "range" );

// setter
$( ".selector" ).slider( "option", "range", true ); 
```

### step**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `1`定义 slider 从最小值移动到最大值的单位步长。在这个指定范围(最小值到最大值)内的值需要能被范围整除。**Code examples:**

使用`step`选项初始化滑块组件：

```
$( ".selector" ).slider({ step: 5 }); 
```

在组件初始化之后，读取或设置 `step` 选项：

```
// getter
var step = $( ".selector" ).slider( "option", "step" );

// setter
$( ".selector" ).slider( "option", "step", 5 ); 
```

### value**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `0`如果只有一个手柄则是指定 slider 的 value 值。 如果有多余一个的操作柄, 则是定义第一个操作柄的 value 值。**Code examples:**

使用`value`选项初始化滑块组件：

```
$( ".selector" ).slider({ value: 10 }); 
```

在组件初始化之后，读取或设置 `value` 选项：

```
// getter
var value = $( ".selector" ).slider( "option", "value" );

// setter
$( ".selector" ).slider( "option", "value", 10 ); 
```

### values**Type:** [Array](http://api.jquery.com/Types/#Array)

**Default:** `null`这个选项可以用来为多个操作柄设定 value 值. 如果 `range` 设置为 `true`, 'values' 的长度最少应为 2。**Code examples:**

使用`values`选项初始化滑块组件：

```
$( ".selector" ).slider({ values: [ 10, 25 ] }); 
```

在组件初始化之后，读取或设置 `values` 选项：

```
// getter
var values = $( ".selector" ).slider( "option", "values" );

// setter
$( ".selector" ).slider( "option", "values", [ 10, 25 ] ); 
```

## Methods

### destroy()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

完全销毁滑块组件的功能，这将使元素返回它的初始状态。

*   这个方法不接收任何参数

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).slider( "destroy" ); 
```

### disable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

禁用滑块组件。

*   这个方法不接收任何参数

**Code examples:**

调用 disable 方法：

```
$( ".selector" ).slider( "disable" ); 
```

### enable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

启用滑块组件。

*   这个方法不接收任何参数

**Code examples:**

调用 enable 方法：

```
$( ".selector" ).slider( "enable" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取与`optionName`对应的选项值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取的值所对应的选项的名称。

**Code examples:**

调用这个方法：

```
var isDisabled = $( ".selector" ).slider( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含有描述当前滑块组件选项哈希值的键/值对。

*   这个方法不接收任何参数

**Code examples:**

调用这个方法：

```
var options = $( ".selector" ).slider( "option" ); 
```

### option( optionName, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置滑块组件`optionName`参数指定的选项的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的参数值。

**Code examples:**

调用这个方法：

```
$( ".selector" ).slider( "option", "disabled", true ); 
```

### option( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置一个或多个滑块组件的选项值。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的选项名与值之间的映射关系。

**Code examples:**

调用这个方法：

```
$( ".selector" ).slider( "option", { disabled: true } ); 
```

### value()Returns: [Number](http://api.jquery.com/Types/#Number)

获取滑块组件的值。

*   这个方法不接收任何参数

**Code examples:**

调用这个方法：

```
var selection = $( ".selector" ).slider( "value" ); 
```

### value( value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置滑块组件的值。

*   **value**Type: [Number](http://api.jquery.com/Types/#Number)用来设置的值

**Code examples:**

调用这个方法：

```
$( ".selector" ).slider( "value", 55 ); 
```

### values()Returns: [Array](http://api.jquery.com/Types/#Array)

获取所有手柄的值.（愚人码头注：适用于多手柄的滑块）

*   这个方法不接收任何参数

**Code examples:**

调用这个方法：

```
var values = $( ".selector" ).slider( "values" ); 
```

### values( index )Returns: [Number](http://api.jquery.com/Types/#Number)

获取指定手柄的值。（愚人码头注：适用于多手柄的滑块）

*   **index**Type: [Integer](http://api.jquery.com/Types/#Integer)从 0 开始计数的手柄索引值。

**Code examples:**

调用这个方法：

```
var value = $( ".selector" ).slider( "values", 0 ); 
```

### values( index, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置指定手柄的值。（愚人码头注：适用于多手柄的滑块）

*   **index**Type: [Integer](http://api.jquery.com/Types/#Integer)从 0 开始计数的手柄索引值。
*   **value**Type: [Number](http://api.jquery.com/Types/#Number)要设置的值

**Code examples:**

调用这个方法：

```
$( ".selector" ).slider( "values", 0, 55 ); 
```

### values( values )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置所有手柄的值。（愚人码头注：适用于多手柄的滑块）

*   **values**Type: [Array](http://api.jquery.com/Types/#Array)要设置的值。

**Code examples:**

调用这个方法：

```
$( ".selector" ).slider( "values", [ 55, 105 ] ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个滑块元素的`jQuery`对象。

*   这个方法不接收任何参数

**Code examples:**

调用 widget 方法：

```
var widget = $( ".selector" ).slider( "widget" ); 
```

## Events

### change( event, ui )Type: `slidechange`

当用户滑动一个手柄后，如果滑块的值改变了，就会触发这个事件；或者通过`value`方法改变手柄值。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **handle**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象，表示被改变的手柄
    *   **value**Type: [Number](http://api.jquery.com/Types/#Number)当前滑块的值。

**Code examples:**

使用 change 回调函数指定事件:

```
$( ".selector" ).slider({
  change: function( event, ui ) {}
}); 
```

绑定事件侦听器到 slidechange 事件：

```
$( ".selector" ).on( "slidechange", function( event, ui ) {} ); 
```

### create( event, ui )Type: `slidecreate`

当滑块组件被创建时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意: `ui`对象是空的，但是为了与其它元素保持一直，它总是被包含。*

**Code examples:**

使用 create 回调函数指定事件:

```
$( ".selector" ).slider({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 slidecreate 事件:

```
$( ".selector" ).on( "slidecreate", function( event, ui ) {} ); 
```

### slide( event, ui )Type: `slide`

这个事件鼠标滑动滑块时触发。`ui.value`作为提供给事件的价值，表示将作为该当前移动手柄的结果值。 取消该事件会阻止手柄移动和手柄将继续其先前的值。取消该事件会阻止手柄移动并且手柄将继续其先前的值。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **handle**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象，表示当前移动的手柄
    *   **value**Type: [Number](http://api.jquery.com/Types/#Number)如果事件没有被取消，该手柄将移动到值 。
    *   **values**Type: [Array](http://api.jquery.com/Types/#Array)一个 多手柄滑块 当前值的数组。

**Code examples:**

使用 slide 回调函数指定事件:

```
$( ".selector" ).slider({
  slide: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 slide 事件:

```
$( ".selector" ).on( "slide", function( event, ui ) {} ); 
```

### start( event, ui )Type: `slidestart`

当用户开始滑动滑块时触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **handle**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象，表示当前移动的手柄
    *   **value**Type: [Number](http://api.jquery.com/Types/#Number)滑块的当前值

**Code examples:**

使用 start 回调函数指定事件:

```
$( ".selector" ).slider({
  start: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 slidestart 事件:

```
$( ".selector" ).on( "slidestart", function( event, ui ) {} ); 
```

### stop( event, ui )Type: `slidestop`

当用户滑动滑块后触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **handle**Type: [jQuery](http://api.jquery.com/Types/#jQuery)一个 jQuery 对象，表示移动后手柄。
    *   **value**Type: [Number](http://api.jquery.com/Types/#Number)滑块的当前值

**Code examples:**

使用 stop 回调函数指定事件:

```
$( ".selector" ).slider({
  stop: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 slidestop 事件:

```
$( ".selector" ).on( "slidestop", function( event, ui ) {} ); 
```

## Example:

#### 一个简单的 jQuery UI 滑块（Slider）。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>slider demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <style>#slider { margin: 10px; } </style>
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<div id="slider"></div>

<script>
$( "#slider" ).slider();
</script>

</body>
</html> 
```

# Spinner Widget

Categories: [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## version added: 1.9

**Description:** 通过向上/向下按钮和箭头按键操作，增强文本输入框的数值输入功能。

## QuickNavExamples

### Options

*   culture
*   disabled
*   icons
*   incremental
*   max
*   min
*   numberFormat
*   page
*   step

### Methods

*   destroy
*   disable
*   enable
*   option
*   pageDown
*   pageUp
*   stepDown
*   stepUp
*   value
*   widget

### Extension Points

*   _buttonHtml
*   _uiSpinnerHtml

### Events

*   change
*   create
*   spin
*   start
*   stop

spinner（微调组件），或数步进控件（number stepper widget），是用于处理各种数字输入的完美控件。它允许用户直接输入一个值，或通过键盘、鼠标、滚轮微调改变一个已有的值。当与全球化（Globalize）结合时，您甚至可以微调显示不同地区的货币和日期。

spinner（微调组件）使用两个按钮将文本输入覆盖为当前值的递增值和递减值。spinner（微调组件）增加了按键事件，以便可以用键盘完成相同的递增和递减。spinner（微调组件）代表 [全球化（Globalize）](https://github.com/jquery/globalize)的数字格式和解析。

### 键盘交互（Keyboard interaction）

*   UP：对值增加一步。
*   DOWN：对值减少一步。
*   PAGE UP：对值增加一页。
*   PAGE DOWN：对值减少一页。

用鼠标点击微调按钮后，焦点仍停留在文本域中。

当 spinner（微调组件）不是只读（`&lt;input readonly&gt;`）时，用户可以输入值，这可能会产生无效的值（小于最小值，大于最大值，增减错配，非数字输入）。当增减时，不管通过编程方式还是微调按钮方式，值都会被强制为一个有效值（如需了解详情，请查看 `stepUp()` 和 `stepDown()` 的描述。

### 主题（Theming）

spinner（微调组件）使用 jQuery UI CSS 框架 来定义它的外观和感观的样式。如果需要使用 spinner（微调组件）指定的样式，则可以使用下面的 CSS class 名称：

*   `ui-spinner`：spinner（微调组件）的外层容器。
    *   `ui-spinner-input`：spinner（微调组件）实例化的 `&lt;input&gt;` 元素。
    *   `ui-spinner-button`：用于递增或递减 spinner（微调组件）值的按钮控件。向上按钮会另外带有一个 `ui-spinner-up` class，向下按钮会另外带有一个 `ui-spinner-down` class。

### 依赖（Dependencies）

*   UI 核心（UI Core）
*   部件库（Widget Factory）
*   按钮部件（Button Widget）
*   [全球化（Globalize）](https://github.com/jquery/globalize)（外部的，可选的；当与 `culture` 和 `numberFormat` 选项一起使用时）

### Additional Notes:

*   该部件要求一些功能性的 CSS，否则将无法工作。如果您创建了一个自定义的主题，请使用小部件指定的 CSS 文件作为起点。
*   该部件以编程方式操作元素的值，因此当元素的值改变时不会触发原生的 `change` 事件。
*   不支持在 `&lt;input type="number"&gt;` 上创建选择器，因为会造成与本地 spinner（微调组件）的 UI 冲突。

## Options

### culture**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `null`设置`culture`选项 用于解析和格式化值。 如果为`null`，在`Globalize`下当前设置的 culture 将被使用， 可供的`culture`，请查看[Globalize 文档](https://github.com/jquery/globalize)。 只有当`numberFormat`选项设置了，才会有关联。 需要引用[Globalize](https://github.com/jquery/globalize)。**Code examples:**

初始化带有指定 `culture`选项的 spinner：

```
$( ".selector" ).spinner({ culture: "fr" }); 
```

在初始化后，获取或设置`culture` 选项：

```
// getter
var culture = $( ".selector" ).spinner( "option", "culture" );

// setter
$( ".selector" ).spinner( "option", "culture", "fr" ); 
```

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为 `true`，则禁用该 spinner（微调组件）。**Code examples:**

初始化带有指定 `disabled`选项的 spinner：

```
$( ".selector" ).spinner({ disabled: true }); 
```

在初始化后，获取或设置`disabled` 选项：

```
// getter
var disabled = $( ".selector" ).spinner( "option", "disabled" );

// setter
$( ".selector" ).spinner( "option", "disabled", true ); 
```

### icons**Type:** [Object](http://api.jquery.com/Types/#Object)

**Default:** `{ down: "ui-icon-triangle-1-s", up: "ui-icon-triangle-1-n" }`标题要使用的图标，与 jQuery UI CSS 框架提供的图标（Icons） 匹配。设置为 false 则不显示图标。

*   up (string, default: "ui-icon-triangle-1-n")
*   down (string, default: "ui-icon-triangle-1-s")

**Code examples:**

初始化带有指定 `icons`选项的 spinner：

```
$( ".selector" ).spinner({ icons: { down: "custom-down-icon", up: "custom-up-icon" } }); 
```

在初始化后，获取或设置`icons` 选项：

```
// getter
var icons = $( ".selector" ).spinner( "option", "icons" );

// setter
$( ".selector" ).spinner( "option", "icons", { down: "custom-down-icon", up: "custom-up-icon" } ); 
```

### incremental**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Function](http://api.jquery.com/Types/#Function)( [Integer](http://api.jquery.com/Types/#Integer) count )

**Default:** `true`当按住 spinner（微调组件）按钮不放时，控制的步数。**支持多个类型：**

*   **Boolean**:如果设置为`true`，当按住 spinner（微调组件）按钮不放时，数值会根据`step`选项的值不断的增加或减少。 当设置为`false`时，所有步骤都是相等的，（由`step`选项所定义）（愚人码头注：点一下，数值会根据`step`选项的值增加或减少一步）。
*   **Function**: 接收一个参数： 已发生的自旋数。 必须返回在当前发生的微调的步数。

**Code examples:**

初始化带有指定 `incremental`选项的 spinner：

```
$( ".selector" ).spinner({ incremental: false }); 
```

在初始化后，获取或设置`incremental` 选项：

```
// getter
var incremental = $( ".selector" ).spinner( "option", "incremental" );

// setter
$( ".selector" ).spinner( "option", "incremental", false ); 
```

### max**Type:** [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)

**Default:** `null`允许的最大值。 如果元素的`max`属性存在，该选项未明确设置，那么该元素的`max`属性就被用作该选项的值。 如果为`null`，表示没有上限。**支持多个类型：**

*   **Number**: 最大值。
*   **String**: 如果应用包含了[Globalize](https://github.com/jquery/globalize)， `max`选项可以传递可以被 `numberFormat`和`culture`选项解析的 字符串。 否则求助原生的`parseFloat()`将方法。

**Code examples:**

初始化带有指定 `max`选项的 spinner：

```
$( ".selector" ).spinner({ max: 50 }); 
```

在初始化后，获取或设置`max` 选项：

```
// getter
var max = $( ".selector" ).spinner( "option", "max" );

// setter
$( ".selector" ).spinner( "option", "max", 50 ); 
```

### min**Type:** [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)

**Default:** `null`允许的最小值。 如果元素的`min`属性存在，该选项未明确设置，那么该元素的`min`属性就被用作该选项的值。 如果为`null`，表示没有下限。**支持多个类型：**

*   **Number**: 最小值。
*   **String**: 如果应用包含了[Globalize](https://github.com/jquery/globalize)， `max`选项可以传递可以被 `numberFormat`和`culture`选项解析的 字符串。 否则使用原生的`parseFloat()`方法解析。

**Code examples:**

初始化带有指定 `min`选项的 spinner：

```
$( ".selector" ).spinner({ min: 0 }); 
```

在初始化后，获取或设置`min` 选项：

```
// getter
var min = $( ".selector" ).spinner( "option", "min" );

// setter
$( ".selector" ).spinner( "option", "min", 0 ); 
```

### numberFormat**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `null`通过[`Globalize`](https://github.com/jquery/globalize)格式化数字， 如果有效的话。 最常见的用于`"n"`用作十进制数 和`"C"`用作货币值。 也看到了`culture`选择。**Code examples:**

初始化带有指定 `numberFormat`选项的 spinner：

```
$( ".selector" ).spinner({ numberFormat: "n" }); 
```

在初始化后，获取或设置`numberFormat` 选项：

```
// getter
var numberFormat = $( ".selector" ).spinner( "option", "numberFormat" );

// setter
$( ".selector" ).spinner( "option", "numberFormat", "n" ); 
```

### page**Type:** [Number](http://api.jquery.com/Types/#Number)

**Default:** `10`当通过`pageUp`/`pageDown`的方法进行分页时，采取的步数。**Code examples:**

初始化带有指定 `page`选项的 spinner：

```
$( ".selector" ).spinner({ page: 5 }); 
```

在初始化后，获取或设置`page` 选项：

```
// getter
var page = $( ".selector" ).spinner( "option", "page" );

// setter
$( ".selector" ).spinner( "option", "page", 5 ); 
```

### step**Type:** [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)

**Default:** `1`通过按钮或`stepUp()`/`stepDown()`方法微调时，采取的步数。 如果元素的`step`属性存在，并且该选项未明确设置，那么元素的`step`属性值将作为该选项的值使用。**支持多个类型：**

*   **Number**: 步数
*   **String**: 如果应用包含了[Globalize](https://github.com/jquery/globalize)， `max`选项可以传递可以被 `numberFormat`和`culture`选项解析的 字符串。 否则使用原生的`parseFloat()`方法解析。

**Code examples:**

初始化带有指定 `step`选项的 spinner：

```
$( ".selector" ).spinner({ step: 2 }); 
```

在初始化后，获取或设置`step` 选项：

```
// getter
var step = $( ".selector" ).spinner( "option", "step" );

// setter
$( ".selector" ).spinner( "option", "step", 2 ); 
```

## Methods

### destroy()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

完全移除 spinner 功能。这会把元素返回到它的预初始化状态。

*   该方法不接受任何参数。

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).spinner( "destroy" ); 
```

### disable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

禁用 spinner.

*   该方法不接受任何参数。

**Code examples:**

调用 disable 方法：

```
$( ".selector" ).spinner( "disable" ); 
```

### enable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

启用 spinner.

*   该方法不接受任何参数。

**Code examples:**

调用 enable 方法：

```
$( ".selector" ).spinner( "enable" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取当前与指定的 `optionName` 关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项的名称。

**Code examples:**

调用该方法：

```
var isDisabled = $( ".selector" ).spinner( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含键/值对的对象，键/值对表示当前 spinner 选项哈希。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
var options = $( ".selector" ).spinner( "option" ); 
```

### option( optionName, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置与指定的 `optionName` 关联的 spinner 选项的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的值。

**Code examples:**

调用该方法：

```
$( ".selector" ).spinner( "option", "disabled", true ); 
```

### option( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

为 spinner 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的 option-value 对。

**Code examples:**

调用该方法：

```
$( ".selector" ).spinner( "option", { disabled: true } ); 
```

### pageDown( [pages ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

通过指定页数递减值， 页数由`page`选项定义。 如果没有参数， 单页递减。

如果返回值大于`max`选项定义的值，小于`min`选项定义的值，或返回的结果步数不匹配， 那么该值将被调整到最接近的有效值。

调用`pageDown()`将引起`start`, `spin`, 和 `stop` 事件被触发。

*   **pages**Type: [Number](http://api.jquery.com/Types/#Number)递减的页数，默认是 1.

**Code examples:**

调用 pageDown 方法：

```
$( ".selector" ).spinner( "pageDown" ); 
```

### pageUp( [pages ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

通过指定页数递增值， 页数由`page`选项定义。 如果没有参数， 单页递增。

如果返回值大于`max`选项定义的值，小于`min`选项定义的值，或返回的结果步数不匹配， 那么该值将被调整到最接近的有效值。

调用`pageUp()`将引起`start`, `spin`, 和 `stop` 事件被触发。

*   **pages**Type: [Number](http://api.jquery.com/Types/#Number)递增的页数，默认是 1.

**Code examples:**

调用 pageUp 方法：

```
$( ".selector" ).spinner( "pageUp", 10 ); 
```

### stepDown( [steps ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

通过指定步数递减值， 步数由`step`选项定义。 如果没有参数， 单步递减。

如果返回值大于`max`选项定义的值，小于`min`选项定义的值，或返回的结果步数不匹配， 那么该值将被调整到最接近的有效值。

调用`stepDown()`将引起`start`, `spin`, 和 `stop` 事件被触发。

*   **steps**Type: [Number](http://api.jquery.com/Types/#Number)递减的步数，默认是 1.

**Code examples:**

调用 stepDown 方法：

```
$( ".selector" ).spinner( "stepDown" ); 
```

### stepUp( [steps ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

通过指定步数递增值， 步数由`step`选项定义。 如果没有参数， 单步递增。

如果返回值大于`max`选项定义的值，小于`min`选项定义的值，或返回的结果步数不匹配， 那么该值将被调整到最接近的有效值。

调用`pageUp()`将引起`start`, `spin`, 和 `stop` 事件被触发。

*   **steps**Type: [Number](http://api.jquery.com/Types/#Number)递增的步数，默认是 1.

**Code examples:**

调用 stepUp 方法：

```
$( ".selector" ).spinner( "stepUp", 5 ); 
```

### value()Returns: [Number](http://api.jquery.com/Types/#Number)

获取当前数值，这个值是基于`numberFormat` 和 `culture`选项解析的。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
var value = $( ".selector" ).spinner( "value" ); 
```

### value( value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置当前值

*   **value**Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)用来设置的值。 如果传递的是一个字符串，那么 这个值是基于`numberFormat` 和 `culture`选项解析的。

**Code examples:**

调用该方法：

```
$( ".selector" ).spinner( "value", 50 ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回包含生成组件包裹元素 的一个`jQuery`对象。

*   该方法不接受任何参数。

**Code examples:**

调用 widget 方法：

```
var widget = $( ".selector" ).spinner( "widget" ); 
```

## 扩展点（Extension Points）

spinner（微调组件）是[widget factory](http://www.css88.com/jquery-ui-api/jQuery.widget/)构建的，并且可以扩展。 当扩展部件时， 你必须覆盖或添加新的行为到现有的方法。 下列方法被提供作为扩展点 用相同的 API 稳定性如上所列的 plugin methods。 有关小部件扩展的更多信息， 请参阅[使用 Widget Factory 扩展小部件](http://learn.jquery.com/jquery-ui/widget-factory/extending-widgets/)。

### _buttonHtml()Returns: [String](http://api.jquery.com/Types/#String)

这个方法返回的 HTML 用于 spinner（微调组件）的递增和递减按钮。 每个按钮都必须给定一个`ui-spinner-button`的类名 用于相关联的事件工作。

*   该方法不接受任何参数。

**Code examples:**

使用`&lt;button&gt;`元素 作为递增和递减按钮。

```
_buttonHtml: function() {
  return "" +
    "<button class='ui-spinner-button ui-spinner-up'>" +
      "<span class='ui-icon " + this.options.icons.up + "'>&#9650;</span>" +
    "</button>" +
    "<button class='ui-spinner-button ui-spinner-down'>" +
      "<span class='ui-icon " + this.options.icons.down + "'>&#9660;</span>" +
    "</button>";
} 
```

### _uiSpinnerHtml()Returns: [String](http://api.jquery.com/Types/#String)

这个方法返回的 HTML 用于包裹 spinner（微调组件）`<input>`元素。

*   该方法不接受任何参数。

**Code examples:**

用没有圆角的`&lt;div&gt;` 包裹 spinner（微调组件）。

```
_uiSpinnerHtml: function() {
  return "<div class='ui-spinner ui-widget ui-widget-content'></div>";
} 
```

## Events

### change( event, ui )Type: `spinchange`

当 spinner 微调器的值改变并且输入元素（input）失去焦点时，该事件触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 change 回调的 spinner（微调器）：

```
$( ".selector" ).spinner({
  change: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 spinchange 事件：

```
$( ".selector" ).on( "spinchange", function( event, ui ) {} ); 
```

### create( event, ui )Type: `spincreate`

当 spinner 微调器创建的时候，该时间触发。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 create 回调的 spinner（微调器）：

```
$( ".selector" ).spinner({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 spincreate 事件：

```
$( ".selector" ).on( "spincreate", function( event, ui ) {} ); 
```

### spin( event, ui )Type: `spin`

在递增/递减的时候，该事件触发（用 当前值和`ui.value`比较来 确定的微调的方向）。

可以取消，以防止被更新值。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **value**Type: [Number](http://api.jquery.com/Types/#Number)要设置的新值，除非该事件被取消。/div>

**Code examples:**

初始化带有指定 spin 回调的 spinner（微调器）：

```
$( ".selector" ).spinner({
  spin: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 spin 事件：

```
$( ".selector" ).on( "spin", function( event, ui ) {} ); 
```

### start( event, ui )Type: `spinstart`

微调开始之前，触发该事件。可以取消，以防止微调。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 start 回调的 spinner（微调器）：

```
$( ".selector" ).spinner({
  start: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 spinstart 事件：

```
$( ".selector" ).on( "spinstart", function( event, ui ) {} ); 
```

### stop( event, ui )Type: `spinstop`

微调结束后，触发该事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 stop 回调的 spinner（微调器）：

```
$( ".selector" ).spinner({
  stop: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 spinstop 事件：

```
$( ".selector" ).on( "spinstop", function( event, ui ) {} ); 
```

## Example:

#### 普通的数字微调器。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>spinner demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<input id="spinner">

<script>
$( "#spinner" ).spinner();
</script>

</body>
</html> 
```

# Tabs Widget

Categories: [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## version added: 1.0

**Description:** 一种多 panel（面板）的单内容区，每个 panel（面板）与列表中的标题相关。

## QuickNavExamples

### Options

*   active
*   collapsible
*   disabled
*   event
*   heightStyle
*   hide
*   show

### Methods

*   destroy
*   disable
*   enable
*   load
*   option
*   refresh
*   widget

### Events

*   activate
*   beforeActivate
*   beforeLoad
*   create
*   load

选项卡（Tabs）通常用于把内容分成多个部分，以便节省空间，就像折叠面板（accordion）一样。

选项卡（Tabs）有一组必须使用的特定标记，以便选项卡能正常工作：

*   选项卡（Tabs）必须在一个有序的（`&lt;ol&gt;`）或无序的（`&lt;ul&gt;`）列表中
*   每个选项卡的 "title" 必须在一个列表项（`&lt;li&gt;`）的内部，且必须用一个带有 `href` 属性的锚（`&lt;a&gt;`）包裹。
*   每个选项卡 panel（面板）可以是任意有效的元素，但是它必须带有一个 id，该 id 与相关选项卡的锚中的哈希相对应。

每个选项卡 panel（面板）的内容可以在页面中定义好，或者可以通过 Ajax 加载。这两种方式都是基于与选项卡相关的锚的 `href` 上自动处理的。默认情况下，选项卡在点击时激活，但是通过 `event` 选项可以改变或覆盖事件。

下面是一些样品标记：

```
<div id="tabs">
  <ul>
    <li><a href="#fragment-1">One</a></li>
    <li><a href="#fragment-2">Two</a></li>
    <li><a href="#fragment-3">Three</a></li>
  </ul>
  <div id="fragment-1">
    Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
  </div>
  <div id="fragment-2">
    Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
  </div>
  <div id="fragment-3">
    Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
  </div>
</div> 
```

### 键盘交互（Keyboard interaction）

当焦点在选项卡上时，下面的键盘命令可用：

*   UP/LEFT：移动焦点到上一个选项卡。如果在第一个选项卡上，则移动焦点到最后一个选项卡。在一个短暂的延迟后激活获得焦点的选项卡。
*   DOWN/RIGHT：移动焦点到下一个选项卡。如果在最后一个选项卡上，则移动焦点到第一个选项卡。在一个短暂的延迟后激活获得焦点的选项卡。
*   HOME：移动焦点到第一个选项卡。在一个短暂的延迟后激活获得焦点的选项卡。
*   END：移动焦点到最后一个选项卡。在一个短暂的延迟后激活获得焦点的选项卡。
*   SPACE：激活与获得焦点的选项卡相关的 panel（面板）。
*   ENTER：激活或切换与获得焦点的选项卡相关的 panel（面板）。
*   ALT+PAGE UP：移动焦点到上一个选项卡，并立即激活。
*   ALT+PAGE DOWN：移动焦点到下一个选项卡，并立即激活。

当焦点在 panel（面板）上时，下面的键盘命令可用：

*   CTRL+UP：移动焦点到相关的选项卡。
*   ALT+PAGE UP：移动焦点到上一个选项卡，并立即激活。
*   ALT+PAGE DOWN：移动焦点到下一个选项卡，并立即激活。

### 主题（Theming）

选项卡部件（Tabs Widget）使用 jQuery UI CSS 框架 来定义它的外观和感观的样式。如果需要使用选项卡指定的样式，则可以使用下面的 CSS class 名称：

*   `ui-tabs`：选项卡的外层容器。当设置了 `collapsible` 选项时，该元素会另外带有一个 `ui-tabs-collapsible` class。
    *   `ui-tabs-nav`：选项卡列表。
        *   导航中激活的列表项会带有一个 `ui-tabs-active` class。内容通过 Ajax 调用加载的列表项会带有一个 `ui-tabs-loading` class。
            *   `ui-tabs-anchor`：用于切换 panel（面板）的锚。
    *   `ui-tabs-panel`：与选项卡相关的 panel（面板）。只有与其对应的选项卡激活时才可见。

### 依赖（Dependencies）

*   UI 核心（UI Core）
*   部件库（Widget Factory）
*   特效核心（Effects Core）（可选的；当与 `show` 和 `hide` 选项一起使用时）

### Additional Notes:

*   该部件要求一些功能性的 CSS，否则将无法工作。如果您创建了一个自定义的主题，请使用小部件指定的 CSS 文件作为起点。

## Options

### active**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Integer](http://api.jquery.com/Types/#Integer)

**Default:** `0`当前打开哪一个 panel（面板）。**支持多个类型：**

*   **Boolean**:设置 `active` 为 `false` 将折叠所有的 panel（面板）。这要求 `collapsible` 选项必须为 `true`。
*   **Integer**: 激活打开的 panel（面板）索引，以零为基础。负值则表示从最后一个 panel（面板）后退选择 panel（面板）。

**Code examples:**

初始化带有指定 `active`选项的 Tab（选项卡）：

```
$( ".selector" ).tabs({ active: 1 }); 
```

在初始化后，获取或设置`active` 选项：

```
// getter
var active = $( ".selector" ).tabs( "option", "active" );

// setter
$( ".selector" ).tabs( "option", "active", 1 ); 
```

### collapsible**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`当设置为 `true`时，激活的 panel（面板）可以被关闭。**Code examples:**

初始化带有指定 `collapsible`选项的 Tab（选项卡）：

```
$( ".selector" ).tabs({ collapsible: true }); 
```

在初始化后，获取或设置`collapsible` 选项：

```
// getter
var collapsible = $( ".selector" ).tabs( "option", "collapsible" );

// setter
$( ".selector" ).tabs( "option", "collapsible", true ); 
```

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Array](http://api.jquery.com/Types/#Array)

**Default:** `false`哪些标签被禁用。**支持多个类型：**

*   **Boolean**: 启用或禁用所有选项卡。
*   **Array**: 一个数组。包含从零开始计数的应该禁用选项卡的索引，例如，`[ 0, 2 ]`将禁用第一和第三个选项卡。

**Code examples:**

初始化带有指定 `disabled`选项的 Tab（选项卡）：

```
$( ".selector" ).tabs({ disabled: [ 0, 2 ] }); 
```

在初始化后，获取或设置`disabled` 选项：

```
// getter
var disabled = $( ".selector" ).tabs( "option", "disabled" );

// setter
$( ".selector" ).tabs( "option", "disabled", [ 0, 2 ] ); 
```

### event**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"click"`激活选项卡的事件类型。 要悬停（hover）激活选项卡，用`"mouseover"`。**Code examples:**

初始化带有指定 `event`选项的 Tab（选项卡）：

```
$( ".selector" ).tabs({ event: "mouseover" }); 
```

在初始化后，获取或设置`event` 选项：

```
// getter
var event = $( ".selector" ).tabs( "option", "event" );

// setter
$( ".selector" ).tabs( "option", "event", "mouseover" ); 
```

### heightStyle**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `"content"`控制 Tab（选项卡）部件和每个 panel（面板）的高度。 可能的值：

*   `"auto"`: 所有的 panel（面板）将会被设置为最高的 panel（面板）的高度。
*   `"fill"`: 基于 tabs 的父元素的高度，扩展到可用的高度。
*   `"content"`: 每个 panel（面板）的高度取决于它的内容。

**Code examples:**

初始化带有指定 `heightStyle`选项的 Tab（选项卡）：

```
$( ".selector" ).tabs({ heightStyle: "fill" }); 
```

在初始化后，获取或设置`heightStyle` 选项：

```
// getter
var heightStyle = $( ".selector" ).tabs( "option", "heightStyle" );

// setter
$( ".selector" ).tabs( "option", "heightStyle", "fill" ); 
```

### hide**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String) or [Object](http://api.jquery.com/Types/#Object)

**Default:** `null`panel（面板）隐藏时的动画效果。**支持多个类型：**

*   **Boolean**: 当设置为`false`， 将不使用动画效果，该 panel（面板）会立即被隐藏。 如果设置为`true`， 该 panel（面板）将会以默认的持续时间和默认的效果淡出。
*   **Number**: 该 panel（面板）将以指定的时间和默认的效果淡出。
*   **String**: 该 panel（面板）将使用指定的效果被隐藏。 该值可以是一个 jQuery 内置的动画方法的名称， 如`"slideUp"`， 或一个 jQuery UI 效果的名称， 如`"fold"`。 在这两种情况下，将使用默认持续时间和默认的动画效果。
*   **Object**: 如果该值是一个对象， 那么 `effect`, `delay`, `duration`, 和`easing`可能要提供。 如果 `effect` 属性包含一个 jQuery 方法的名称， 那么该方法将被使用; 否则它被假定为是一个 jQuery UI 的效果的名称。 当使用 jQuery UI 支持额外设置 的效果 ， 你可以在对象中包含那些设置 并且它们将被传递到的效果。如果`duration`持续时间或`easing`属性被省略， 那么默认值将被使用。 如果`effect`被省略， 那么`"fadeOut"` 将被使用。如果`delay`被省略， 那么将不使用延迟。

**Code examples:**

初始化带有指定 `hide`选项的 Tab（选项卡）：

```
$( ".selector" ).tabs({ hide: { effect: "explode", duration: 1000 } }); 
```

在初始化后，获取或设置`hide` 选项：

```
// getter
var hide = $( ".selector" ).tabs( "option", "hide" );

// setter
$( ".selector" ).tabs( "option", "hide", { effect: "explode", duration: 1000 } ); 
```

### show**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String) or [Object](http://api.jquery.com/Types/#Object)

**Default:** `null`panel（面板）显示时的动画效果。**支持多个类型：**

*   **Boolean**: 当设置为`false`， 将不使用动画效果，该 panel（面板）会立即被隐藏。 如果设置为`true`， 该 panel（面板）将会以默认的持续时间和默认的效果淡出。
*   **Number**: 该 panel（面板）将以指定的时间和默认的效果淡出。
*   **String**: 该 panel（面板）将使用指定的效果被隐藏。 该值可以是一个 jQuery 内置的动画方法的名称， 如`"slideUp"`， 或一个 jQuery UI 效果的名称， 如`"fold"`。 在这两种情况下，将使用默认持续时间和默认的动画效果。
*   **Object**: 如果该值是一个对象， 那么 `effect`, `delay`, `duration`, 和`easing`可能要提供。 如果 `effect` 属性包含一个 jQuery 方法的名称， 那么该方法将被使用; 否则它被假定为是一个 jQuery UI 的效果的名称。 当使用 jQuery UI 支持额外设置 的效果 ， 你可以在对象中包含那些设置 并且它们将被传递到的效果。如果`duration`持续时间或`easing`属性被省略， 那么默认值将被使用。 如果`effect`被省略， 那么`"fadeOut"` 将被使用。如果`delay`被省略， 那么将不使用延迟。

**Code examples:**

初始化带有指定 `show`选项的 Tab（选项卡）：

```
$( ".selector" ).tabs({ show: { effect: "blind", duration: 800 } }); 
```

在初始化后，获取或设置`show` 选项：

```
// getter
var show = $( ".selector" ).tabs( "option", "show" );

// setter
$( ".selector" ).tabs( "option", "show", { effect: "blind", duration: 800 } ); 
```

## Methods

### destroy()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

完全移除 Tab（选项卡） 功能. 这将使元素返回到之前的初始化状态。

*   该方法不接受任何参数。

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).tabs( "destroy" ); 
```

### disable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

禁用全部的 tabs（选项卡）。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
$( ".selector" ).tabs( "disable" ); 
```

### disable( index )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

禁用某个 tabs（选项卡）。选定的选项卡不能被禁用。 要一次禁用多个选项卡， 设置`disabled` 选项： `$( "#tabs" ).tabs( "option", "disabled", [ 1, 2, 3 ] )`.

*   **index**Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)哪个 tabs（选项卡）被禁用。

**Code examples:**

调用该方法：

```
$( ".selector" ).tabs( "disable", 1 ); 
```

### enable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

启用全部的 tabs（选项卡）。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
$( ".selector" ).tabs( "enable" ); 
```

### enable( index )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

启用某个 tabs（选项卡）。 要一次要启多个选项卡，可以重置 disabled 属性，如： `$( "#example" ).tabs( "option", "disabled", [] );`.

*   **index**Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)Which tab to enable.

**Code examples:**

调用该方法：

```
$( ".selector" ).tabs( "enable", 1 ); 
```

### load( index )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

加载远程选项卡的面板内容。

*   **index**Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)哪个 tabs 需要加载

**Code examples:**

调用 load 方法：

```
$( ".selector" ).tabs( "load", 1 ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取当前与指定的 `optionName` 关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项的名称。

**Code examples:**

调用该方法：

```
var isDisabled = $( ".selector" ).tabs( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含键/值对的对象，键/值对表示当前 tabs 选项哈希。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
var options = $( ".selector" ).tabs( "option" ); 
```

### option( optionName, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置与指定的 `optionName` 关联的 tabs 选项的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的值。

**Code examples:**

调用该方法：

```
$( ".selector" ).tabs( "option", "disabled", true ); 
```

### option( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

为 tabs（选项卡） 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的 option-value 对。

**Code examples:**

调用该方法：

```
$( ".selector" ).tabs( "option", { disabled: true } ); 
```

### refresh()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

处理任何在 DOM 中直接添加或移除的标题和面板，并重新计算 tabs（选项卡） 的高度。结果取决于内容和 `heightStyle` 选项。

*   该方法不接受任何参数。

**Code examples:**

调用 refresh 方法：

```
$( ".selector" ).tabs( "refresh" ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个包含 tabs（选项卡） 的 `jQuery` 对象。

*   该方法不接受任何参数。

**Code examples:**

调用 widget 方法：

```
var widget = $( ".selector" ).tabs( "widget" ); 
```

## Events

### activate( event, ui )Type: `tabsactivate`

面板被激活后触发（在动画完成之后）。如果 tabs（选项卡） 之前是关闭的，则 `ui.oldTab` 和 `ui.oldPanel` 将是空的 jQuery 对象。如果 tabs（选项卡） 正在折叠，则 `ui.newTab` 和 `ui.newPanel` 将是空的 jQuery 对象。

**注意：** 由于 `activate` 事件只有在面板激活时才能触发，当创建 tabs（选项卡） 部件时，最初的面板不会触发该事件。如果您需要一个用于部件创建的钩，请使用 `create` 事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **newTab**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚被激活的选项卡。
    *   **oldTab**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚被取消激活的选项卡。
    *   **newPanel**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚被激活的面板。
    *   **oldPanel**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚被取消激活的面板。

**Code examples:**

初始化带有指定 activate 回调的 Tab（选项卡面板）：

```
$( ".selector" ).tabs({
  activate: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 tabsactivate 事件：

```
$( ".selector" ).on( "tabsactivate", function( event, ui ) {} ); 
```

### beforeActivate( event, ui )Type: `tabsbeforeactivate`

tabs（选项卡）被激活前直接触发。可以取消以防止 tabs（选项卡）被激活。如果 tabs（选项卡） 当前是关闭的，则 `ui.oldTab` 和 `ui.oldPanel` 将是空的 jQuery 对象。如果 accordion 正在折叠，则 `ui.newTab` 和 `ui.newPanel` 将是空的 jQuery 对象。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **newTab**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚被激活的选项卡。
    *   **oldTab**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚被取消激活的选项卡。
    *   **newPanel**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚被激活的面板。
    *   **oldPanel**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚被取消激活的面板。

**Code examples:**

初始化带有指定 beforeActivate 回调的 Tab（选项卡面板）：

```
$( ".selector" ).tabs({
  beforeActivate: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 tabsbeforeactivate 事件：

```
$( ".selector" ).on( "tabsbeforeactivate", function( event, ui ) {} ); 
```

### beforeLoad( event, ui )Type: `tabsbeforeload`

在一个远程选项卡被加载之前，`beforeActivate`事件之后，触发该事件。可以取消，以防止 tabs（选项卡）面板加载内容;虽然面板仍然会被激活。 该事件被触发 Ajax 请求发送之前，这样可以使用`ui.jqXHR` 和 `ui.ajaxSettings`修改。

*注意： 虽然`ui.ajaxSettings`被提供，并且可以被修改， 其中的一些设置已经通过 jQuery 处理。 例如，prefilters 已经被应用，`data`已被处理，还有`type`已经确定。 ， 因为`beforeSend`作为`jQuery.ajax()`的回调，`beforeLoad` 事件同时是发生的，因此具有相同的限制。*

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **tab**Type: [jQuery](http://api.jquery.com/Types/#jQuery)正在加载的选项卡。
    *   **panel**Type: [jQuery](http://api.jquery.com/Types/#jQuery)将 Ajax 响应填充的面板。
    *   **jqXHR**Type: [jqXHR](http://api.jquery.com/Types/#jqXHR)被请求内容的 `jqXHR` 对象。
    *   **ajaxSettings**Type: [Object](http://api.jquery.com/Types/#Object)用于由`jQuery.ajax`请求内容的设置。

**Code examples:**

初始化带有指定 beforeLoad 回调的 Tab（选项卡面板）：

```
$( ".selector" ).tabs({
  beforeLoad: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 tabsbeforeload 事件：

```
$( ".selector" ).on( "tabsbeforeload", function( event, ui ) {} ); 
```

### create( event, ui )Type: `tabscreate`

当创建 tabs（选项卡) 时触发。如果 tabs（选项卡) 是关闭的，`ui.tab` 和 `ui.panel` 将是空的 jQuery 对象。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **tab**Type: [jQuery](http://api.jquery.com/Types/#jQuery)激活的选项卡
    *   **panel**Type: [jQuery](http://api.jquery.com/Types/#jQuery)激活的面板。

**Code examples:**

初始化带有指定 create 回调的 Tab（选项卡面板）：

```
$( ".selector" ).tabs({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 tabscreate 事件：

```
$( ".selector" ).on( "tabscreate", function( event, ui ) {} ); 
```

### load( event, ui )Type: `tabsload`

远程选项卡加载后触发该事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **tab**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚加载的选项卡。
    *   **panel**Type: [jQuery](http://api.jquery.com/Types/#jQuery)刚刚填充的 Ajax 响应的面板。

**Code examples:**

初始化带有指定 load 回调的 Tab（选项卡面板）：

```
$( ".selector" ).tabs({
  load: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 tabsload 事件：

```
$( ".selector" ).on( "tabsload", function( event, ui ) {} ); 
```

## Example:

#### 一个简单的 jQuery UI 选项卡（Tabs）。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>tabs demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<div id="tabs">
  <ul>
    <li><a href="#fragment-1"><span>One</span></a></li>
    <li><a href="#fragment-2"><span>Two</span></a></li>
    <li><a href="#fragment-3"><span>Three</span></a></li>
  </ul>
  <div id="fragment-1">
    <p>First tab is active by default:</p>
    <pre><code>$( "#tabs" ).tabs(); </code></pre>
  </div>
  <div id="fragment-2">
    Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
    Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
  </div>
  <div id="fragment-3">
    Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
    Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
    Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
  </div>
</div>

<script>
$( "#tabs" ).tabs();
</script>

</body>
</html> 
```

# Tooltip Widget

Categories: [Widgets](http://www.css88.com/jquery-ui-api/category/widgets/ "View all posts in Widgets")

## version added: 1.9

**Description:** 可自定义的、可主题化的工具提示框，替代原生的工具提示框。

## QuickNavExamples

### Options

*   content
*   disabled
*   hide
*   items
*   position
*   show
*   tooltipClass
*   track

### Methods

*   close
*   destroy
*   disable
*   enable
*   open
*   option
*   widget

### Events

*   close
*   create
*   open

工具提示框（Tooltip）取代了原生的工具提示框，让它们可主题化，也允许进行各种自定义：

*   显示不仅仅是标题的其他内容，就如内联的脚注或通过 Ajax 检索的额外内容。
*   自定义定位，例如，在元素上居中工具提示框。
*   添加额外的样式来定制警告或错误区域的外观。

默认使用一个渐变的动画来显示和隐藏工具提示框，这种外观与简单的切换可见度相比更具灵性。这可以通过 `show` 和 `hide` 选项进行定制。

*   `items` 和 `content` 选项需要保持同步。如果您改变了其中一个，您需要同时改变另一个。

在一般情况下，禁用的元素不会触发任何 DOM 事件。因此，适当地控制禁用元素的工具提示框是不可能的，因为我们需要监听事件来决定何时显示和隐藏工具提示框。这就导致 jQuery UI 不能保证对附加到禁用元素上的工具提示框任何层次上的支持。这意味着如果您需要在禁用元素上进行提示，您可能需要使用一个原生的提示框和 jQuery UI 工具提示框的混合物。

### 主题（Theming）

工具提示框部件（Tooltip Widget）使用 jQuery UI CSS 框架 来定义它的外观和感观的样式。如果需要使用工具提示框指定的样式，则可以使用下面的 CSS class 名称：

*   `ui-tooltip`: 工具提示框的外层容器。
    *   `ui-tooltip-content`: 工具提示框的内容。

### 依赖（Dependencies）

*   UI 核心（UI Core）
*   部件库（Widget Factory）
*   定位（Position）
*   特效核心（Effects Core）（可选的；当与 `show` 和 `hide` 选项一起使用时）

### 其他注意事项（Additional Notes）:

*   该部件要求一些功能性的 CSS，否则将无法工作。如果您创建了一个自定义的主题，请使用小部件指定的 CSS 文件作为起点。

## Options

### content**Type:** [Function](http://api.jquery.com/Types/#Function)() or [String](http://api.jquery.com/Types/#String)

**Default:** `function returning the title attribute`

tooltip(工具提示框)的内容。

*当改变这个选项时，你可能还需要更改 `items`选项。*

**支持多个类型：**

*   **Function**: 一个回调可以是直接返回的内容， 或通过在内容，调用第一个参数，例如，对于 Ajax 内容。
*   **String**: 一个 HTML 字符串作为 tooltip(工具提示框)的内容。

**Code examples:**

初始化带有指定 `content` 选项的 tooltip(工具提示框)：

```
$( ".selector" ).tooltip({ content: "Awesome title!" }); 
```

在初始化后，获取或设置`content` 选项：

```
// getter
var content = $( ".selector" ).tooltip( "option", "content" );

// setter
$( ".selector" ).tooltip( "option", "content", "Awesome title!" ); 
```

### disabled**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`如果设置为 `true`，则禁用该 tooltip（工具提示框）。**Code examples:**

初始化带有指定 `disabled` 选项的 tooltip(工具提示框)：

```
$( ".selector" ).tooltip({ disabled: true }); 
```

在初始化后，获取或设置`disabled` 选项：

```
// getter
var disabled = $( ".selector" ).tooltip( "option", "disabled" );

// setter
$( ".selector" ).tooltip( "option", "disabled", true ); 
```

### hide**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String) or [Object](http://api.jquery.com/Types/#Object)

**Default:** `true`tooltip(工具提示框)关闭（隐藏）时的动画效果。**支持多个类型：**

*   **Boolean**: 当设置为`false`， 将不使用动画效果，该 tooltip(工具提示框) 会立即被隐藏。 如果设置为`true`， 该 tooltip(工具提示框) 将会以默认的持续时间和默认的效果淡出。
*   **Number**: 该 tooltip(工具提示框) 将以指定的时间和默认的效果淡出。
*   **String**: 该 tooltip(工具提示框) 将使用指定的效果被隐藏。 该值可以是一个 jQuery 内置的动画方法的名称， 如`"slideUp"`， 或一个 jQuery UI 效果的名称， 如`"fold"`。 在这两种情况下，将使用默认持续时间和默认的动画效果。
*   **Object**: 如果该值是一个对象， 那么 `effect`, `delay`, `duration`, 和`easing`可能要提供。 如果 `effect` 属性包含一个 jQuery 方法的名称， 那么该方法将被使用; 否则它被假定为是一个 jQuery UI 的效果的名称。 当使用 jQuery UI 支持额外设置 的效果 ， 你可以在对象中包含那些设置 并且它们将被传递到的效果。如果`duration`持续时间或`easing`属性被省略， 那么默认值将被使用。 如果`effect`被省略， 那么`"fadeOut"` 将被使用。如果`delay`被省略， 那么将不使用延迟。

**Code examples:**

初始化带有指定 `hide` 选项的 tooltip(工具提示框)：

```
$( ".selector" ).tooltip({ hide: { effect: "explode", duration: 1000 } }); 
```

在初始化后，获取或设置`hide` 选项：

```
// getter
var hide = $( ".selector" ).tooltip( "option", "hide" );

// setter
$( ".selector" ).tooltip( "option", "hide", { effect: "explode", duration: 1000 } ); 
```

### items**Type:** [Selector](http://api.jquery.com/Types/#Selector)

**Default:** `[title]`

一个选择器表示哪些项目应该显示 tooltip(工具提示框)。 如果您使用其他的东西自定义，那么 title 属性将作为 tooltip(工具提示框)的内容， 或者你需要一个不同的选择来事件委托。

*当改变这个选项时，你可能还需要改变的 `content` 选项。*

**Code examples:**

初始化带有指定 `items` 选项的 tooltip(工具提示框)：

```
$( ".selector" ).tooltip({ items: "img[alt]" }); 
```

在初始化后，获取或设置`items` 选项：

```
// getter
var items = $( ".selector" ).tooltip( "option", "items" );

// setter
$( ".selector" ).tooltip( "option", "items", "img[alt]" ); 
```

### position**Type:** [Object](http://api.jquery.com/Types/#Object)

**Default:** `{ my: "left top+15", at: "left bottom", collision: "flipfit" }`

确定 tooltip(工具提示框) 相对于 相关目标元素的位置。 `of`选项默认为目标元素， 但您可以指定其他元素来定位。 有关各个选项的更多细节， 你可以参考 jQuery UI Position 实用工具。

**Code examples:**

初始化带有指定 `position` 选项的 tooltip(工具提示框)：

```
$( ".selector" ).tooltip({ position: { my: "left+15 center", at: "right center" } }); 
```

在初始化后，获取或设置`position` 选项：

```
// getter
var position = $( ".selector" ).tooltip( "option", "position" );

// setter
$( ".selector" ).tooltip( "option", "position", { my: "left+15 center", at: "right center" } ); 
```

### show**Type:** [Boolean](http://api.jquery.com/Types/#Boolean) or [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String) or [Object](http://api.jquery.com/Types/#Object)

**Default:** `true`tooltip(工具提示框) 打开（显示）时的动画效果。**支持多个类型：**

*   **Boolean**: 当设置为`false`， 将不使用动画效果，该 tooltip(工具提示框) 会立即被隐藏。 如果设置为`true`， 该 tooltip(工具提示框) 将会以默认的持续时间和默认的效果淡出。
*   **Number**: 该 tooltip(工具提示框) 将以指定的时间和默认的效果淡出。
*   **String**: 该 tooltip(工具提示框) 将使用指定的效果被隐藏。 该值可以是一个 jQuery 内置的动画方法的名称， 如`"slideUp"`， 或一个 jQuery UI 效果的名称， 如`"fold"`。 在这两种情况下，将使用默认持续时间和默认的动画效果。
*   **Object**: 如果该值是一个对象， 那么 `effect`, `delay`, `duration`, 和`easing`可能要提供。 如果 `effect` 属性包含一个 jQuery 方法的名称， 那么该方法将被使用; 否则它被假定为是一个 jQuery UI 的效果的名称。 当使用 jQuery UI 支持额外设置 的效果 ， 你可以在对象中包含那些设置 并且它们将被传递到的效果。如果`duration`持续时间或`easing`属性被省略， 那么默认值将被使用。 如果`effect`被省略， 那么`"fadeOut"` 将被使用。如果`delay`被省略， 那么将不使用延迟。

**Code examples:**

初始化带有指定 `show` 选项的 tooltip(工具提示框)：

```
$( ".selector" ).tooltip({ show: { effect: "blind", duration: 800 } }); 
```

在初始化后，获取或设置`show` 选项：

```
// getter
var show = $( ".selector" ).tooltip( "option", "show" );

// setter
$( ".selector" ).tooltip( "option", "show", { effect: "blind", duration: 800 } ); 
```

### tooltipClass**Type:** [String](http://api.jquery.com/Types/#String)

**Default:** `null`一个 CSS 样式类名 添加到 tooltip(工具提示框)小部件， 可用于显示各种提示类型， 像警告或错误。

这可能会被[classes option](http://bugs.jqueryui.com/ticket/7053)取代。

**Code examples:**

初始化带有指定 `tooltipClass` 选项的 tooltip(工具提示框)：

```
$( ".selector" ).tooltip({ tooltipClass: "custom-tooltip-styling" }); 
```

在初始化后，获取或设置`tooltipClass` 选项：

```
// getter
var tooltipClass = $( ".selector" ).tooltip( "option", "tooltipClass" );

// setter
$( ".selector" ).tooltip( "option", "tooltipClass", "custom-tooltip-styling" ); 
```

### track**Type:** [Boolean](http://api.jquery.com/Types/#Boolean)

**Default:** `false`tooltip(工具提示框)是否应该跟踪（跟随）鼠标。**Code examples:**

初始化带有指定 `track` 选项的 tooltip(工具提示框)：

```
$( ".selector" ).tooltip({ track: true }); 
```

在初始化后，获取或设置`track` 选项：

```
// getter
var track = $( ".selector" ).tooltip( "option", "track" );

// setter
$( ".selector" ).tooltip( "option", "track", true ); 
```

## Methods

### close()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

关闭 tooltip(工具提示框) 。这仅供非委派的 tooltip(工具提示框) 调用。

*   该方法不接受任何参数。

**Code examples:**

调用 close 方法：

```
$( ".selector" ).tooltip( "close" ); 
```

### destroy()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

完全移除 tooltip(工具提示框) 功能. 这将使元素返回到之前的初始化状态.

*   该方法不接受任何参数。

**Code examples:**

调用 destroy 方法：

```
$( ".selector" ).tooltip( "destroy" ); 
```

### disable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

禁用 tooltip(工具提示框)。

*   该方法不接受任何参数。

**Code examples:**

调用 disable 方法：

```
$( ".selector" ).tooltip( "disable" ); 
```

### enable()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

启用 tooltip(工具提示框)。

*   该方法不接受任何参数。

**Code examples:**

调用 enable 方法：

```
$( ".selector" ).tooltip( "enable" ); 
```

### open()Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

以编程方式打开一个 tooltip(工具提示框) 。这仅供非委派的 tooltip(工具提示框) 调用。

*   该方法不接受任何参数。

**Code examples:**

调用 open 方法：

```
$( ".selector" ).tooltip( "open" ); 
```

### option( optionName )Returns: [Object](http://api.jquery.com/Types/#Object)

获取当前与指定的 `optionName` 关联的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要获取值的选项的名称。

**Code examples:**

调用该方法：

```
var isDisabled = $( ".selector" ).tooltip( "option", "disabled" ); 
```

### option()Returns: [PlainObject](http://api.jquery.com/Types/#PlainObject)

获取一个包含键/值对的对象，键/值对表示当前 tooltip(工具提示框) 选项哈希。

*   该方法不接受任何参数。

**Code examples:**

调用该方法：

```
var options = $( ".selector" ).tooltip( "option" ); 
```

### option( optionName, value )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

设置与指定的 `optionName` 关联的 tooltip(工具提示框) 选项的值。

*   **optionName**Type: [String](http://api.jquery.com/Types/#String)要设置的选项的名称。
*   **value**Type: [Object](http://api.jquery.com/Types/#Object)要为选项设置的值。

**Code examples:**

调用该方法：

```
$( ".selector" ).tooltip( "option", "disabled", true ); 
```

### option( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery) ([plugin only](http://learn.jquery.com/jquery-ui/widget-factory/widget-method-invocation/))

为 tooltip(工具提示框) 设置一个或多个选项。

*   **options**Type: [Object](http://api.jquery.com/Types/#Object)要设置的 option-value 对。

**Code examples:**

调用该方法：

```
$( ".selector" ).tooltip( "option", { disabled: true } ); 
```

### widget()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

返回一个包含 生成包裹元素 的 `jQuery` 对象。

*   该方法不接受任何参数。

**Code examples:**

调用 widget 方法：

```
var widget = $( ".selector" ).tooltip( "widget" ); 
```

## Events

### close( event, ui )Type: `tooltipclose`

当 tooltip(工具提示框) 关闭时触发，触发事件为`focusout` 或 `mouseleave`。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **tooltip**Type: [jQuery](http://api.jquery.com/Types/#jQuery)生成 tooltip(工具提示框) 的元素。

**Code examples:**

初始化带有指定 close 回调的 tooltip(工具提示框)：

```
$( ".selector" ).tooltip({
  close: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 tooltipclose 事件：

```
$( ".selector" ).on( "tooltipclose", function( event, ui ) {} ); 
```

### create( event, ui )Type: `tooltipcreate`

在创建 tooltip(工具提示框)时触发该事件。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)

*注意：`ui` 对象是空的，这里包含它是为了与其他事件保持一致性。*

**Code examples:**

初始化带有指定 create 回调的 tooltip(工具提示框)：

```
$( ".selector" ).tooltip({
  create: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 tooltipcreate 事件：

```
$( ".selector" ).on( "tooltipcreate", function( event, ui ) {} ); 
```

### open( event, ui )Type: `tooltipopen`

当 tooltip(工具提示框)打开，显示时，触发此事件，触发的事件为`focusin` 或 `mouseover`。

*   **event**Type: [Event](http://api.jquery.com/Types/#Event)
*   **ui**Type: [Object](http://api.jquery.com/Types/#Object)
    *   **tooltip**Type: [jQuery](http://api.jquery.com/Types/#jQuery)生成 tooltip(工具提示框) 的元素。

**Code examples:**

初始化带有指定 open 回调的 tooltip(工具提示框)：

```
$( ".selector" ).tooltip({
  open: function( event, ui ) {}
}); 
```

绑定一个事件监听器到 tooltipopen 事件：

```
$( ".selector" ).on( "tooltipopen", function( event, ui ) {} ); 
```

## Example:

#### 使用带有 title 属性的所有元素的事件代理，在文档上创建一个工具提示框（Tooltip）。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>tooltip demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<p>
  <a href="#" title="Anchor description">Anchor text</a>
  <input title="Input help">
</p>
<script>
  $( document ).tooltip();
</script>

</body>
</html> 
```