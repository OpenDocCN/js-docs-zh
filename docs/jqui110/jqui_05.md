# Method Overrides

jQuery UI 重载了几个内置的 jQuery 方法，以提供额外的功能。当使用这些重载时，确保加载 jQuery UI 是很重要的。如果 jQuery UI 未加载，方法依然存在，但预期的功能将不可用，这会导致难以追踪的错误。

Also in: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core")

## .addClass()

当动画样式改变时，为匹配的元素集合内的每个元素添加指定的 Class。

Also in: [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods") | [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .focus()

异步聚焦到一个元素。

Also in: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods")

## .hide()

使用自定义效果来隐藏匹配的元素。

Also in: [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods") | [Utilities](http://www.css88.com/jquery-ui-api/category/utilities/ "View all posts in Utilities")

## .position()

相对另一个元素定位一个元素。

Also in: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core")

## .removeClass()

当动画样式改变时，为匹配的元素集合内的每个元素移除指定的 Class。

Also in: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods")

## .show()

使用自定义效果来显示匹配的元素。

Also in: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods")

## .toggle()

使用自定义效果来显示或隐藏匹配的元素。

Also in: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core")

## .toggleClass()

当动画样式改变时，根据 Class 是否存在以及 switch 参数的值，为匹配的元素集合内的每个元素添加或移除一个或多个 Class。

# .focus()

Categories: [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods") | [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .focus( delay [, callback ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 异步聚焦到一个元素。

*   #### [.focus( delay [, callback ] )](#focus-delay-callback)

    *   **delay**Type: [Integer](http://api.jquery.com/Types/#Integer)聚焦前等待的毫秒数。
    *   **callback**Type: [Function](http://api.jquery.com/Types/#Function)()元素被聚焦后要调用的函数。

该插件扩展自 jQuery 内置的 `.focus()` 方法。如果 jQuery UI 未加载，调用 `.focus()` 方法不会直接失败，因为该方法在 jQuery 中存在。但是不会发生预期的行为。

# .position()

Categories: [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods") | [Utilities](http://www.css88.com/jquery-ui-api/category/utilities/ "View all posts in Utilities")

## .position( options )Returns: [jQuery](http://api.jquery.com/Types/#jQuery)version added: 1.8

**Description:** 相对另一个元素定位一个元素。

*   #### .position( options )

    *   **options**Type: [Object](http://api.jquery.com/Types/#Object)
        *   **my**（默认值：`"center"`） 类型：String 描述：定义**被定位元素上**对准目标元素的位置："horizontal vertical" 对齐方式。一个单一的值，比如 "right" 将规范为 "right center"，"top" 将规范为 "center top"（下面的 CSS 公约）。可接受的水平值："left"、"center"、"right"。可接受的垂直值："top"、"center"、"bottom"。例如，"left top" 或 "center center"。每个纬度也可以包含偏移，以像素计或以百分比计，例如 "right+10 top-25%"。百分比偏移是相对于被定位的元素。
        *   **at**（默认值：`"center"`） 类型：String 描述：定义**目标元素上**对准被定位元素的位置： "horizontal vertical" 对齐方式。如需了解更多细节请查看 my 选项上的可能值。百分比偏移是相对于目标元素。
        *   **of**（默认值：`null`） 类型：Selector 或 Element 或 jQuery 或 Event 描述：要定位的元素。如果您提供一个选择器（Selector）或 jQuery 对象，将使用第一个匹配元素。如果您提供一个事件（Event）对象，将使用 pageX 和 pageY 属性，例如 "#top-menu"。
        *   **collision**（默认值：`"flip"`） 类型：String 描述：当被定位元素在某些方向上溢出窗口，则移动它到另一个位置。与 my 和 at 选项相似，该选项会接受一个单一的值或一对 horizontal/vertical 值。例如："flip"、"fit"、"fit flip"、"fit none"。
            *   "flip"：翻转元素到目标的相对一边，再次运行 collision 检测一遍查看元素是否适合。无论哪一边允许更多的元素可见，则使用那一边。
            *   "fit"：把元素从窗口的边缘移开。
            *   "flipfit"：首先应用 flip 逻辑，把元素放置在允许更多元素可见的那一边。然后应用 fit 逻辑，确保尽可能多的元素可见。
            *   "none"：不应用任何 collision 检测。
        *   **using**（默认值：`null`） 类型：Function() 描述：当指定了该选项，实际属性设置则委托给该回调。接受两个参数：第一个是位置 top 和 left 值的哈希，可被转发到 .css() 或 .animate()；第二个提供了关于两个元素的位置和尺寸的反馈，同时也计算它们的相对位置。target 和 element 都有下列属性：element、left、top、width、height。另外，还有 horizontal、vertical 和 important，提供了十二个可能的方向，如 { horizontal: "center", vertical: "left", important: "horizontal" }。
        *   **within**（默认值：`window`） 类型：Selector 或 Element 或 jQuery 描述：元素定位为 within，会影响 collision 检测。如果您提供了一个选择器（Selector）或 jQuery 对象，则使用第一个匹配的元素。

jQuery UI `.position()` 方法允许您相对窗体（window）、文档、另一个元素或指针（cursor）/鼠标（mouse）来定位一个元素，无需考虑相对父元素的偏移（offset）。

注释：jQuery UI 不支持定位隐藏元素。

这是一个独立的 jQuery 插件，且对其他 jQuery UI 组件没有依赖关系。

该插件扩展自 jQuery 内置的 .position() 方法。如果 jQuery UI 未加载，调用 `.position()` 方法不会直接失败，因为该方法在 jQuery 中存在。但是不会发生预期的行为。

## Example:

#### 一个简单的 jQuery UI 定位（Position）实例。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>position demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <style>
  .positionDiv {
    position: absolute;
    width: 75px;
    height: 75px;
    background: green;
  }
  </style>
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<div id="targetElement">
  <div class="positionDiv" id="position1"></div>
  <div class="positionDiv" id="position2"></div>
  <div class="positionDiv" id="position3"></div>
  <div class="positionDiv" id="position4"></div>
</div>

<script>
$( "#position1" ).position({
  my: "center",
  at: "center",
  of: "#targetElement"
});

$( "#position2" ).position({
  my: "left top",
  at: "left top",
  of: "#targetElement"
});

$( "#position3" ).position({
  my: "right center",
  at: "right bottom",
  of: "#targetElement"
});

$( document ).mousemove(function( event ) {
  $( "#position4" ).position({
    my: "left+3 bottom-3",
    of: event,
    collision: "fit"
  });
});
</script>

</body>
</html> 
```