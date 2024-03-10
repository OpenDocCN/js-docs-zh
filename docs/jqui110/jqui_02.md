# Effects

jQuery UI 在 jQuery 内置的特效上添加了一些功能。jQuery UI 支持颜色动画和 Class 转换，同时也提供了一些额外的 Easings。另外，提供了一套完整的定制特效，供显示和隐藏元素时或者只是添加一些视觉显示时使用。

Also in: [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides")

## .addClass()

当动画样式改变时，为匹配的元素集合内的每个元素添加指定的 Class。

## Blind Effect

百叶窗特效（Blind Effect）通过将元素包裹在一个容器内，采用"拉百叶窗"效果来隐藏或显示元素。

## Bounce Effect

反弹特效（Bounce Effect）反弹一个元素。当与隐藏或显示一起使用时，最后一次或第一次反弹会呈现淡入/淡出效果。

## Clip Effect

剪辑特效（Clip Effect）通过垂直或水平方向夹剪元素来隐藏或显示一个元素。

## Color Animation

使用 .animate() 实现颜色动画效果。

## Drop Effect

降落特效（Drop Effect）通过单个方向滑动的淡入淡出来隐藏或显示一个元素。

## Easings

Easing 函数指定动画在不同点上的行进速度。

Also in: [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods")

## .effect()

对一个元素应用动画特效。

## Explode Effect

爆炸特效（Explode Effect）通过把元素裂成碎片来隐藏或显示一个元素。

## Fade Effect

淡入淡出特效（Fade Effect）通过淡入淡出元素来隐藏或显示一个元素。

## Fold Effect

折叠特效（Fold Effect）通过折叠元素来隐藏或显示一个元素。

Also in: [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods")

## .hide()

使用自定义效果来隐藏匹配的元素。

## Highlight Effect

突出特效（Highlight Effect）通过首先改变背景颜色来隐藏或显示一个元素。

## Puff Effect

通过在缩放元素的同时隐藏元素来创建膨胀特效（Puff Effect）。

## Pulsate Effect

跳动特效（Pulsate Effect）通过跳动来隐藏或显示一个元素。

Also in: [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides")

## .removeClass()

当动画样式改变时，为匹配的元素集合内的每个元素移除指定的 Class。

## Scale Effect

按照某个百分比缩放元素。

## Shake Effect

垂直或水平方向多次震动元素。

Also in: [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods")

## .show()

使用自定义效果来显示匹配的元素。

## Size Effect

调整元素尺寸到指定宽度和高度。

## Slide Effect

把元素滑动出视区。

Blind EffectAlso in: [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core")

## .switchClass()

当动画样式改变时，为匹配的元素集合内的每个元素添加和移除指定的 Class。

Also in: [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods")

## .toggle()

使用自定义效果来显示或隐藏匹配的元素。

Also in: [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides")

## .toggleClass()

当动画样式改变时，根据 Class 是否存在以及 switch 参数的值，为匹配的元素集合内的每个元素添加或移除一个或多个 Class。

## Transfer Effect

把一个元素的轮廓转移到另一个元素。

# .addClass()

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides")

## .addClass( className [, duration ] [, easing ] [, complete ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**描述:** 为每个匹配的元素添加指定的样式类名，而且所有改变的样式以动画的形式展示

*   #### [.addClass( className [, duration ] [, easing ] [, complete ] )](#addClass-className-duration-easing-complete)

    *   **className**Type: [String](http://api.jquery.com/Types/#String)为每个匹配元素的 class 属性增加一个或多个样式名（空格隔开）。
    *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（愚人码头注：默认值: "normal"， 三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
    *   **easing** (default: `swing`)Type: [String](http://api.jquery.com/Types/#String)一个字符串，表示过渡使用哪种缓动 函数。
    *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
*   #### [.addClass( className [, options ] )](#addClass-className-options)

    *   **className**Type: [String](http://api.jquery.com/Types/#String)为每个匹配元素的 class 属性增加一个或多个样式名（空格隔开）。
    *   **options**Type: [Object](http://api.jquery.com/Types/#Object)一组包含动画选项的值的集合。 支持的选项:
        *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（译者注：默认值: "normal"， 三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
        *   **easing** (default: `swing`)Type: [String](http://api.jquery.com/Types/#String)一个字符串，表示过渡使用哪种缓动 函数。
        *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
        *   **children** (default: `false`)Type: [Boolean](http://api.jquery.com/Types/#Boolean)动画是否应用到所有匹配的元素的后代元素。应慎使用此功能。 因为要确定哪些后代元素要应用动画可能会非常好性能，而且 后代元素的数量是线性增长的。
        *   **queue** (default: `true`)Type: [Boolean](http://api.jquery.com/Types/#Boolean) or [String](http://api.jquery.com/Types/#String)一个布尔值，指示是否将动画放置在效果队列中。如果为 false 时，将立即开始动画。 **从 jQuery1.7 开始**，队列选项也可以接受一个字符串，在这种情况下， 在动画被添加到由该字符串表示的队列中。

类似原生 CSS transitions（过渡）， jQuery UI 的样式动画提供了一个从一个状态到另一个状态平滑过渡， 同时让你 保持那些 CSS 样式改版的所有细节，和你的 javaScript 分离。所有样式动画的方法，包括 `.addClass()` 支持自定义的持续时间（durations）和缓冲函数（easing），以及在动画完成时提供一个回调。

并非所有的样式都可以设置动画。 例如，没有办法让背景图像应用动画。不能进行动画的样式，将在动画结束时被改变。

这个插件扩展了 jQuery 中的[`.addClass()`](http://api.jquery.com/addClass)方法。 如果没有加载 jQuery UI，调用`.addClass()`方法可能不会失败，因为方法仍然存在。 然而，预期的行为（愚人码头注：指平滑过渡动画效果）将不会发生。

## Example:

#### 匹配的元素上添加"big-blue"样式。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>addClass demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  div {
    width: 100px;
    height: 100px;
    background-color: #ccc;
  }
  .big-blue {
    width: 200px;
    height: 200px;
    background-color: #00f;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<div></div>

<script>
$( "div" ).click(function() {
  $( this ).addClass( "big-blue", 1000, "easeOutBounce" );
});
</script>

</body>
</html> 
```

# Blind Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** 百叶窗效果隐藏或者显示一个包装在一个容器中的元素时候具有“拉百叶窗”的效果

*   #### blind

    *   **direction** (default: `"up"`)Type: [String](http://api.jquery.com/Types/#String)

        direction 参数是表示百叶窗效果向哪个方向隐藏元素，或者从哪个方向开始显示元素。

        可选值: `up`, `down`, `left`, `right`, `vertical`, `horizontal`.

容器元素的应用了 `overflow: hidden`属性，所以高度的变化将影响其可见性。

## Example:

#### 使用百叶窗效果切换隐藏显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>blind demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to toggle the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).toggle( "blind" );
});
</script>

</body>
</html> 
```

# Bounce Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** 反弹特效上下反弹一个元素。当反弹特效和隐藏或显示配合使用时，最后一个或第一个反弹也将呈现淡入或淡出效果。

*   #### bounce

    *   **distance** (default: `20`)Type: [Number](http://api.jquery.com/Types/#Number)反弹的最大距离，单位为像素。
    *   **times** (default: `5`)Type: [Integer](http://api.jquery.com/Types/#Integer)元素将会反弹的次数。当和隐藏或显示搭配使用时，淡入淡出时会有额外的“半”反弹效果。

## Example:

#### 使用反弹特效来切换显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>bounce demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to toggle the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).toggle( "bounce", { times: 3 }, "slow" );
});
</script>

</body>
</html> 
```

# Clip Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** 剪辑效果通过垂直或水平剪辑一个元素来显示或隐藏它，并且它是从元素的两端同时进行的。

*   #### clip

    *   **direction** (default: `"up"`)Type: [String](http://api.jquery.com/Types/#String)

        剪辑效果将隐藏或显示其中元素的平面。

        `vertical` 值将剪辑顶部和底部边缘, while `horizontal` 值将剪辑左部和右部边缘

## Example:

#### 使用剪辑特效切换显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>clip demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to toggle the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).toggle( "clip" );
});
</script>

</body>
</html> 
```

# Color Animation

jQuery UI 特效内核使用`rgb()`， `rgba()`，16 进制值，甚至颜色名称比如`"aqua"`给颜色增加了动画新特性。只需要包含 jQuery UI 特效内核文件和[`.animate()`](http://api.jquery.com/animate/)就可以获得对各种颜色的支持。

支持以下属性:

*   `backgroundColor`
*   `borderBottomColor`
*   `borderLeftColor`
*   `borderRightColor`
*   `borderTopColor`
*   `color`
*   `columnRuleColor`
*   `outlineColor`
*   `textDecorationColor`
*   `textEmphasisColor`

对颜色动画的技术支持来自 [jQuery Color plugin](https://github.com/jquery/jquery-color)。颜色插件提供了多个函数来处理各种颜色。 查看完整文档，请访问[jQuery Color documentation](https://github.com/jquery/jquery-color#readme)。

## Class Animations（与动画关联的 CSS 类）

当为单独的颜色属性直接呈现动画效果时，将样式包含在 css 类中是一个很好的处理方式。 jQuery UI 提供了一系列方法，这些方法可以根据新增的 CSS 类来呈现动画，还可以删除任何 CSS 类。 这些方法包含`.addClass()`, `.removeClass()`, `.toggleClass()`和 `.switchClass()`。 这些方法将自动决定哪些属性需要被改变并且对其应用适当的动画。

## Example

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Color Animation Demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #elem {
    color: #006;
    background-color: #aaa;
    font-size: 25px;
    padding: 1em;
    text-align: center;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<div id="elem">color animations</div>
<button id="toggle">animate colors</button>

<script>
$( "#toggle" ).click(function() {
  $( "#elem" ).animate({
    color: "green",
    backgroundColor: "rgb( 20, 20, 20 )"
  });
});
</script>

</body>
</html> 
```

# Drop Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** 拉拽特效隐藏或显示一个元素，并使用通过淡入或淡出效果使它向一个方向滑动。

*   #### drop

    *   **direction** (default: `"left"`)Type: [String](http://api.jquery.com/Types/#String)

        direction 参数表示将向哪个方向隐藏这个元素，或从哪个方向开始显示这个元素。

        可选值: `up`, `down`, `left`, `right`.

## Example:

#### 使用拉拽特效切换显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>drop demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to toggle the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).toggle( "drop" );
});
</script>

</body>
</html> 
```

# Easings

动画缓冲函数可以确定在动画过程中不同时刻的动画速度。 jQuery 内核自带有 2 种动画渐变: `linear`，整个动画在一个恒定的速度中进行（匀速） ，和`swing` (jQuery 内核的默认渐变效果)，此效果开始和结束的速度要比中间过程的速度要慢。 jQuery UI 还提供了其它一些额外的渐变函数，这些函数会在 `swing`效果中搜索变量来自定义其它效果，比如 bouncing（反弹）。

一些缓冲函数在动画过程中会产生负数值。呈现动画效果的属性不同， 某些属性的实际值可能会在为 0 时被锁定。例如，你可以将`left`值渐变为一个负数，但是你不能将`height`或者`opacity`的值缓冲为一个负数。

理解动画缓冲如何影响动画最好的方式就是查看对应的函数图像。下面列出了 jQuery UI 中所有动画的函数图像。

# .effect()

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods")

## .effect( effect [, options ] [, duration ] [, complete ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 在一个元素上应用一个动画特效。

*   #### [.effect( effect [, options ] [, duration ] [, complete ] )](#effect-effect-options-duration-complete)

    *   **effect**Type: [String](http://api.jquery.com/Types/#String)一个字符串，指示哪个特效被使用。
    *   **options**Type: [Object](http://api.jquery.com/Types/#Object)特效选项和缓冲函数。
    *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（愚人码头注：三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
    *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
*   #### .effect( options )

    *   **options**Type: [Object](http://api.jquery.com/Types/#Object)全部动画选项。 只有一个必须设置的属性`effect`。
        *   **effect**Type: [String](http://api.jquery.com/Types/#String)一个字符串，指示哪个特效被使用。
        *   **easing** (default: `"swing"`)Type: [String](http://api.jquery.com/Types/#String)一个字符串，表示过渡使用哪种 缓动 函数。
        *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（愚人码头注：三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
        *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
        *   **queue** (default: `true`)Type: [Boolean](http://api.jquery.com/Types/#Boolean) or [String](http://api.jquery.com/Types/#String)一个布尔值，指示是否将动画放置在效果队列中。如果为 false 时，将立即开始动画。 **从 jQuery1.7 开始**，队列选项也可以接受一个字符串，在这种情况下， 在动画被添加到由该字符串表示的队列中。

`.effect()`方法将对一个元素应用一个特效。 许多特效同时也具有显示和隐藏效果， 你可以搭配使用`.show()`, `.hide()`, 和`.toggle()`方法来实现。

## Example:

#### 一个 div 应用反弹特效。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>effect demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  div {
    width: 100px;
    height: 100px;
    background: #ccc;
    border: 1px solid #000;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to apply the effect.</p>
<div></div>

<script>
$( document ).click(function() {
  $( "div" ).effect( "bounce", "slow" );
});
</script>

</body>
</html> 
```

# Explode Effect

分类: 特效

**描述:** 爆炸特效通过将元素分拆成若干片来隐藏或显示一个元素。

*   #### explode

    *   **pieces** (默认值: `9`)类型: [整型](http://api.jquery.com/Types/#Integer)要分裂的数量， 应该是一个完全平方数,任何其它值都会被四舍五入转换为最接近的完全平方数。

## 例子:

#### 使用分裂特效切换显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>explode demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>点击任何区域来切换显示 div。</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).toggle( "explode" );
});
</script>

</body>
</html> 
```

# Fade Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** 淡入淡出的隐藏或显示一个元素。.

*   #### fade

## Example:

#### 使用淡入淡出特效切换显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>fade demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to toggle the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).toggle( "fade" );
});
</script>

</body>
</html> 
```

# Fold Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** 通过折叠形式来隐藏或显示一个元素。

*   #### fold

    *   **size** (default: `15`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)折叠元素的尺寸。
    *   **horizFirst** (default: `false`)Type: [Boolean](http://api.jquery.com/Types/#Boolean)当先从水平方向开始隐藏时，记住，当显示时，方向是和隐藏时相反的。（愚人码头注：即如果隐藏时为从右至左，那么显示时为从左至右。）

## Example:

#### 使用折叠特效切换显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>fold demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to toggle the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).toggle( "fold" );
});
</script>

</body>
</html> 
```

# .hide()

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods")

## .hide( effect [, options ] [, duration ] [, complete ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 使用自定义的效果隐藏匹配的元素。

*   #### [.hide( effect [, options ] [, duration ] [, complete ] )](#hide-effect-options-duration-complete)

    *   **effect**Type: [String](http://api.jquery.com/Types/#String)一个字符串，指示哪个特效被使用。
    *   **options**Type: [Object](http://api.jquery.com/Types/#Object)特效选项和缓冲函数。
    *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（愚人码头注：三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
    *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
*   #### .hide( options )

    *   **options**Type: [Object](http://api.jquery.com/Types/#Object)全部动画选项。 只有一个必须设置的属性`effect`。
        *   **effect**Type: [String](http://api.jquery.com/Types/#String)一个字符串，指示哪个特效被使用。
        *   **easing** (default: `"swing"`)Type: [String](http://api.jquery.com/Types/#String)一个字符串，表示过渡使用哪种 缓动 函数。
        *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（愚人码头注：三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
        *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
        *   **queue** (default: `true`)Type: [Boolean](http://api.jquery.com/Types/#Boolean) or [String](http://api.jquery.com/Types/#String)一个布尔值，指示是否将动画放置在效果队列中。如果为 false 时，将立即开始动画。 **从 jQuery1.7 开始**，队列选项也可以接受一个字符串，在这种情况下， 在动画被添加到由该字符串表示的队列中。

这个插件扩展了 jQuery 中的[`.hide()`](http://api.jquery.com/hide)方法。 如果没有加载 jQuery UI，调用`.hide()`方法可能不会失败，因为方法仍然存在。 然而，预期的行为（愚人码头注：指平滑过渡动画效果）将不会发生。

## Example:

#### 使用拖动特效切换显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>hide demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  div {
    width: 100px;
    height: 100px;
    background: #ccc;
    border: 1px solid #000;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<button>hide the div</button>
<div></div>

<script>
$( "button" ).click(function() {
  $( "div" ).hide( "drop", { direction: "down" }, "slow" );
});
</script>

</body>
</html> 
```

# Highlight Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** 高亮特效通过先动画呈现元素的背景颜色来隐藏或显示一个元素。

*   #### highlight

    *   **color** (default: `"#ffff99"`)Type: [String](http://api.jquery.com/Types/#String)动画执行时的背景颜色。

## Example:

#### 使用高亮特效切换显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>highlight demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to toggle the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).toggle( "highlight" );
});
</script>

</body>
</html> 
```

# Puff Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** 创建拉伸的效果，缩放元素的同时隐藏或显示元素。

*   #### puff

    *   **percent** (default: `150`)Type: [Number](http://api.jquery.com/Types/#Number)元素放大的百分比。

## Example:

#### 使用拉伸特效来切换显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>puff demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to toggle the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).toggle( "puff" );
});
</script>

</body>
</html> 
```

# Pulsate Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** 闪烁效果通过脉冲闪烁隐藏或显示元素。

*   #### pulsate

    *   **times** (default: `5`)Type: [Integer](http://api.jquery.com/Types/#Integer)元素闪烁的次数，在隐藏或显示时会额外增加一个半闪烁效果。

## Example:

#### 使用闪烁特效来切换显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>pulsate demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to toggle the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).toggle( "pulsate" );
});
</script>

</body>
</html> 
```

# .removeClass()

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides")

## .removeClass( className [, duration ] [, easing ] [, complete ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 为每个匹配的元素移除指定的样式类名，而且所有改变的样式以动画的形式展示

*   #### [.removeClass( className [, duration ] [, easing ] [, complete ] )](#removeClass-className-duration-easing-complete)

    *   **className**Type: [String](http://api.jquery.com/Types/#String)为每个匹配元素的 class 属性移除一个或多个样式名（空格隔开）。
    *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（愚人码头注：默认值: "normal"， 三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
    *   **easing** (default: `swing`)Type: [String](http://api.jquery.com/Types/#String)一个字符串，表示过渡使用哪种缓动 函数。
    *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
*   #### [.removeClass( className [, options ] )](#removeClass-className-options)

    *   **className**Type: [String](http://api.jquery.com/Types/#String)为每个匹配元素的 class 属性移除一个或多个样式名（空格隔开）。
    *   **options**Type: [Object](http://api.jquery.com/Types/#Object)一组包含动画选项的值的集合。 支持的选项:
        *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（译者注：默认值: "normal"， 三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
        *   **easing** (default: `swing`)Type: [String](http://api.jquery.com/Types/#String)一个字符串，表示过渡使用哪种缓动 函数。
        *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
        *   **children** (default: `false`)Type: [Boolean](http://api.jquery.com/Types/#Boolean)动画是否应用到所有匹配的元素的后代元素。应慎使用此功能。 因为要确定哪些后代元素要应用动画可能会非常好性能，而且 后代元素的数量是线性增长的。
        *   **queue** (default: `true`)Type: [Boolean](http://api.jquery.com/Types/#Boolean) or [String](http://api.jquery.com/Types/#String)一个布尔值，指示是否将动画放置在效果队列中。如果为 false 时，将立即开始动画。 **从 jQuery1.7 开始**，队列选项也可以接受一个字符串，在这种情况下， 在动画被添加到由该字符串表示的队列中。

类似原生 CSS transitions（过渡）， jQuery UI 的样式动画提供了一个从一个状态到另一个状态平滑过渡， 同时让你 保持那些 CSS 样式改版的所有细节，和你的 javaScript 分离。所有样式动画的方法，包括 `.removeClass()` 支持自定义的持续时间（durations）和缓冲函数（easing），以及在动画完成时提供一个回调。

并非所有的样式都可以设置动画。 例如，没有办法让背景图像应用动画。不能进行动画的样式，将在动画结束时被改变。

这个插件扩展了 jQuery 中的[`.removeClass()`](http://api.jquery.com/removeClass)方法。 如果没有加载 jQuery UI，调用`.removeClass()`方法可能不会失败，因为方法仍然存在。 然而，预期的行为（愚人码头注：指平滑过渡动画效果）将不会发生。

## Example:

#### 匹配的元素上移除"big-blue"样式。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>removeClass demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  div {
    width: 100px;
    height: 100px;
    background-color: #ccc;
  }
  .big-blue {
    width: 200px;
    height: 200px;
    background-color: #00f;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<div class="big-blue"></div>

<script>
$( "div" ).click(function() {
  $( this ).removeClass( "big-blue", 1000, "easeInBack" );
});
</script>

</body>
</html> 
```

# Scale Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** 按百分比缩小或放大一个元素。

*   #### scale

    *   **direction** (default: `"both"`)Type: [String](http://api.jquery.com/Types/#String)效果的方向。 可选值: `"both"`, `"vertical"` or `"horizontal"`.
    *   **origin** (default: `[ "middle", "center" ]`)Type: [Array](http://api.jquery.com/Types/#Array)消失点。
    *   **percent**Type: [Number](http://api.jquery.com/Types/#Number)缩放百分比。
    *   **scale** (default: `"both"`)Type: [String](http://api.jquery.com/Types/#String)确定元素的哪个区域将被缩放: `"both"`, `"box"`, `"content"`。 Box 值缩放元素的 border 和 padding; content 值缩放元素内部的所有内容。

## Examples:

#### Example: 使用缩放特效切换显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>scale demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to toggle the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).toggle( "scale" );
});
</script>

</body>
</html> 
```

#### Example: 使用缩放特效，但只朝一个方向切换显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>scale demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to toggle the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).toggle({ effect: "scale", direction: "horizontal" });
});
</script>

</body>
</html> 
```

# Shake Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** 在垂直或水平方向上多次抖动一个元素。

*   #### shake

    *   **direction** (default: `"left"`)Type: [String](http://api.jquery.com/Types/#String)一个"left"或"right"值将使元素在水平方向抖动， "up"或"down"值将使元素在垂直方向抖动。 该值指定元素这个效果应沿轴线移动的第一步的方向。
    *   **distance** (default: `20`)Type: [Number](http://api.jquery.com/Types/#Number)抖动距离。
    *   **times** (default: `3`)Type: [Integer](http://api.jquery.com/Types/#Integer)抖动次数。

## Example:

#### 抖动一个 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>shake demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to shake the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).effect( "shake" );
});
</script>

</body>
</html> 
```

# .show()

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods")

## .show( effect [, options ] [, duration ] [, complete ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 使用自定义特效显示匹配的元素。

*   #### [.show( effect [, options ] [, duration ] [, complete ] )](#show-effect-options-duration-complete)

    *   **effect**Type: [String](http://api.jquery.com/Types/#String)一个字符串，指示哪个特效被使用。
    *   **options**Type: [Object](http://api.jquery.com/Types/#Object)特效选项和缓冲函数。
    *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（愚人码头注：三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
    *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
*   #### .show( options )

    *   **options**Type: [Object](http://api.jquery.com/Types/#Object)全部动画选项。 只有一个必须设置的属性`effect`。
        *   **effect**Type: [String](http://api.jquery.com/Types/#String)一个字符串，指示哪个特效被使用。
        *   **easing** (default: `"swing"`)Type: [String](http://api.jquery.com/Types/#String)一个字符串，表示过渡使用哪种 缓动 函数。
        *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（愚人码头注：三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
        *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
        *   **queue** (default: `true`)Type: [Boolean](http://api.jquery.com/Types/#Boolean) or [String](http://api.jquery.com/Types/#String)一个布尔值，指示是否将动画放置在效果队列中。如果为 false 时，将立即开始动画。 **从 jQuery1.7 开始**，队列选项也可以接受一个字符串，在这种情况下， 在动画被添加到由该字符串表示的队列中。

这个插件扩展了 jQuery 中的[`.show()`](http://api.jquery.com/show)方法。 如果没有加载 jQuery UI，调用`.show()`方法可能不会失败，因为方法仍然存在。 然而，预期的行为（愚人码头注：指平滑过渡动画效果）将不会发生。

## Example:

#### 使用折叠特效显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>show demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  div {
    display: none;
    width: 100px;
    height: 100px;
    background: #ccc;
    border: 1px solid #000;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<button>show the div</button>
<div></div>

<script>
$( "button" ).click(function() {
  $( "div" ).show( "fold", 1000 );
});
</script>

</body>
</html> 
```

# Size Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** 将元素的尺寸设置到一个指定的宽度和高度。

*   #### size

    *   **to**Type: [Object](http://api.jquery.com/Types/#Object)改变后高和宽。
    *   **origin** (default: `[ "top", "left" ]`)Type: [Array](http://api.jquery.com/Types/#Array)特效起始的方向。
    *   **scale** (default: `"both"`)Type: [String](http://api.jquery.com/Types/#String)确定元素的哪个区域将被缩放: `"both"`, `"box"`, `"content"`。Box 值缩放元素的 border 和 padding; content 值缩放元素内部的所有内容。

## Example:

#### 使用尺寸特效来改变 div 的尺寸。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>size demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to resize the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).effect( "size", {
    to: { width: 200, height: 60 }
  }, 1000 );
});
</script>

</body>
</html> 
```

# Slide Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** 将元素滑动到可视区域之外。

*   #### slide

    *   **direction** (default: `"both"`)Type: [String](http://api.jquery.com/Types/#String)特效的执行方向。可选值: `"left"`, `"right"`, `"up"`, `"down"`。
    *   **distance** (default: `element's outerWidth`（元素的外边缘宽）)Type: [Number](http://api.jquery.com/Types/#Number)特效执行的距离。 默认值为元素的高或宽,取决于 `direction` 参数的值来决定（愚人码头注：水平方向为宽，垂直方向为高）。 可以被设置为任何小于元素宽/高的整数。

## Example:

#### 使用滑动特效切换显示 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>slide demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  #toggle {
    width: 100px;
    height: 100px;
    background: #ccc;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<p>Click anywhere to toggle the box.</p>
<div id="toggle"></div>

<script>
$( document ).click(function() {
  $( "#toggle" ).toggle( "slide" );
});
</script>

</body>
</html> 
```

# .switchClass()

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core")

## .switchClass( removeClassName, addClassName [, duration ] [, easing ] [, complete ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 为每一组匹配的元素添加或移除指定的样式类，而且所有改变的样式以动画的形式展示

*   #### [.switchClass( removeClassName, addClassName [, duration ] [, easing ] [, complete ] )](#switchClass-removeClassName-addClassName-duration-easing-complete)

    *   **removeClassName**Type: [String](http://api.jquery.com/Types/#String)将要被从匹配的元素移除的 class 属性的一个或多个名称(以空格分开) 。
    *   **addClassName**Type: [String](http://api.jquery.com/Types/#String)将要被添加到匹配的元素的 class 属性的一个或多个名称(以空格分开) 。
    *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（译者注：默认值: "normal"， 三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
    *   **easing** (default: `swing`)Type: [String](http://api.jquery.com/Types/#String)一个字符串，表示过渡使用哪种缓动 函数。
    *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
*   #### [.switchClass( removeClassName, addClassName [, options ] )](#switchClass-removeClassName-addClassName-options)

    *   **removeClassName**Type: [String](http://api.jquery.com/Types/#String)将要被从匹配的元素移除的 class 属性的一个或多个名称(以空格分开) 。
    *   **addClassName**Type: [String](http://api.jquery.com/Types/#String)将要被添加到匹配的元素的 class 属性的一个或多个名称(以空格分开) 。
    *   **options**Type: [Object](http://api.jquery.com/Types/#Object)一组包含动画选项的值的集合。所有属性是可选择的。
        *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（译者注：默认值: "normal"， 三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
        *   **easing** (default: `swing`)Type: [String](http://api.jquery.com/Types/#String)一个字符串，表示过渡使用哪种缓动 函数。
        *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
        *   **children** (default: `false`)Type: [Boolean](http://api.jquery.com/Types/#Boolean)动画是否应用到所有匹配的元素的后代元素。应慎使用此功能。 因为要确定哪些后代元素要应用动画可能会非常好性能，而且 后代元素的数量是线性增长的。
        *   **queue** (default: `true`)Type: [Boolean](http://api.jquery.com/Types/#Boolean) or [String](http://api.jquery.com/Types/#String)一个布尔值，指示是否将动画放置在效果队列中。如果为 false 时，将立即开始动画。 **从 jQuery1.7 开始**，队列选项也可以接受一个字符串，在这种情况下， 在动画被添加到由该字符串表示的队列中。

`.switchClass()`方法允许你在展现动画的同时添加或移除样式类。

类似原生 CSS transitions（过渡）， jQuery UI 的样式动画提供了一个从一个状态到另一个状态平滑过渡， 同时让你 保持那些 CSS 样式改版的所有细节，和你的 javaScript 分离。 所有样式动画的方法，包括 `.switchClass()` 支持自定义的持续时间（durations）和缓冲函数（easing），以及在动画完成时提供一个回调。

并非所有的样式都可以设置动画。 例如，没有办法让背景图像应用动画。不能进行动画的样式，将在动画结束时被改变。

这个插件扩展了 jQuery 中的[`.switchClass()`](http://api.jquery.com/switchClass)方法。 如果没有加载 jQuery UI，调用`.switchClass()`方法可能不会失败，因为方法仍然存在。 然而，预期的行为（愚人码头注：指平滑过渡动画效果）将不会发生。

## Example:

#### 向匹配的元素添加样式类"blue"，并且移除样式类"big"。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>switchClass demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  div {
    width: 100px;
    height: 100px;
    background-color: #ccc;
  }
  .big {
    width: 200px;
    height: 200px;
  }
  .blue {
    background-color: #00f;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<div class="big"></div>

<script>
$( "div" ).click(function() {
  $( this ).switchClass( "big", "blue", 1000, "easeInOutQuad" );
});
</script>

</body>
</html> 
```

# .toggle()

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides") | [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods")

## .toggle( effect [, options ] [, duration ] [, complete ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 使用自定义特效显示或隐藏匹配的元素。

*   #### [.toggle( effect [, options ] [, duration ] [, complete ] )](#toggle-effect-options-duration-complete)

    *   **effect**Type: [String](http://api.jquery.com/Types/#String)一个字符串，指示哪个特效被使用。
    *   **options**Type: [Object](http://api.jquery.com/Types/#Object)特效选项和缓冲函数。
    *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（愚人码头注：三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
    *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
*   #### .toggle( options )

    *   **options**Type: [Object](http://api.jquery.com/Types/#Object)全部动画选项。 只有一个必须设置的属性`effect`。
        *   **effect**Type: [String](http://api.jquery.com/Types/#String)一个字符串，指示哪个特效被使用。
        *   **easing** (default: `"swing"`)Type: [String](http://api.jquery.com/Types/#String)一个字符串，表示过渡使用哪种 缓动 函数。
        *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（愚人码头注：三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
        *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
        *   **queue** (default: `true`)Type: [Boolean](http://api.jquery.com/Types/#Boolean) or [String](http://api.jquery.com/Types/#String)一个布尔值，指示是否将动画放置在效果队列中。如果为 false 时，将立即开始动画。 **从 jQuery1.7 开始**，队列选项也可以接受一个字符串，在这种情况下， 在动画被添加到由该字符串表示的队列中。

这个插件扩展了 jQuery 中的[`.toggle()`](http://api.jquery.com/toggle)方法。 如果没有加载 jQuery UI，调用`.toggle()`方法可能不会失败，因为方法仍然存在。 然而，预期的行为（愚人码头注：指平滑过渡动画效果）将不会发生。

## Example:

#### 使用折叠特效来切换显示一个 div。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>toggle demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  div {
    width: 100px;
    height: 100px;
    background: #ccc;
    border: 1px solid #000;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<button>toggle the div</button>
<div></div>

<script>
$( "button" ).click(function() {
  $( "div" ).toggle( "fold", 1000 );
});
</script>

</body>
</html> 
```

# .toggleClass()

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides")

## .toggleClass( className [, switch ] [, duration ] [, easing ] [, complete ] )Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 为每一组匹配的元素添加或移除一个或多个样式类，取决于当前元素是否存在该样式类和 switch 参数。，而且所有改变的样式以动画的形式展示

*   #### [.toggleClass( className [, switch ] [, duration ] [, easing ] [, complete ] )](#toggleClass-className-switch-duration-easing-complete)

    *   **className**Type: [String](http://api.jquery.com/Types/#String)将要被添加到匹配的元素的 class 属性的一个或多个名称(以空格分开) 。
    *   **switch**Type: [Boolean](http://api.jquery.com/Types/#Boolean)一个决定是否添加或移除某 css 类的布尔值。
    *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（愚人码头注：三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
    *   **easing** (default: `swing`)Type: [String](http://api.jquery.com/Types/#String)一个字符串，表示过渡使用哪种 缓动 函数。
    *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
*   #### [.toggleClass( className [, switch ] [, options ] )](#toggleClass-className-switch-options)

    *   **className**Type: [String](http://api.jquery.com/Types/#String)将要被添加到匹配的元素的 class 属性的一个或多个名称(以空格分开) 。
    *   **switch**Type: [Boolean](http://api.jquery.com/Types/#Boolean)一个决定是否添加或移除某 css 类的布尔值。
    *   **options**Type: [Object](http://api.jquery.com/Types/#Object)一组包含动画选项的值的集合。所有属性是可选择的。
        *   **duration** (default: `400`)Type: [Number](http://api.jquery.com/Types/#Number) or [String](http://api.jquery.com/Types/#String)一个字符串或者数字决定动画将运行多久。（译者注：默认值: "normal"， 三种预定速度的字符串("slow", "normal", 或 "fast")或表示动画时长的毫秒数值(如：1000) ）
        *   **easing** (default: `swing`)Type: [String](http://api.jquery.com/Types/#String)一个字符串，表示过渡使用哪种缓动 函数。
        *   **complete**Type: [Function](http://api.jquery.com/Types/#Function)()在动画完成时执行的函数。
        *   **children** (default: `false`)Type: [Boolean](http://api.jquery.com/Types/#Boolean)动画是否应用到所有匹配的元素的后代元素。应慎使用此功能。 因为要确定哪些后代元素要应用动画可能会非常好性能，而且 后代元素的数量是线性增长的。
        *   **queue** (default: `true`)Type: [Boolean](http://api.jquery.com/Types/#Boolean) or [String](http://api.jquery.com/Types/#String)一个布尔值，指示是否将动画放置在效果队列中。如果为 false 时，将立即开始动画。 **从 jQuery1.7 开始**，队列选项也可以接受一个字符串，在这种情况下， 在动画被添加到由该字符串表示的队列中。

类似原生 CSS transitions（过渡）， jQuery UI 的样式动画提供了一个从一个状态到另一个状态平滑过渡， 同时让你 保持那些 CSS 样式改版的所有细节，和你的 javaScript 分离。 所有样式动画的方法，包括 `.toggleClass()` 支持自定义的持续时间（durations）和缓冲函数（easing），以及在动画完成时提供一个回调。

并非所有的样式都可以设置动画。 例如，没有办法让背景图像应用动画。不能进行动画的样式，将在动画结束时被改变。

这个插件扩展了 jQuery 中的[`.toggleClass()`](http://api.jquery.com/toggleClass)方法。 如果没有加载 jQuery UI，调用`.toggleClass()`方法可能不会失败，因为方法仍然存在。 然而，预期的行为（愚人码头注：指平滑过渡动画效果）将不会发生。

## Example:

#### 把类"big-blue"添加到匹配的元素

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>toggleClass demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  div {
    width: 100px;
    height: 100px;
    background-color: #ccc;
  }
  .big-blue {
    width: 200px;
    height: 200px;
    background-color: #00f;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<div></div>

<script>
$( "div" ).click(function() {
  $( this ).toggleClass( "big-blue", 1000, "easeOutSine" );
});
</script>

</body>
</html> 
```

# Transfer Effect

Categories: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects")

**Description:** Transfers the outline of an element to another element

*   #### transfer

    *   **className**Type: [String](http://api.jquery.com/Types/#String)传递给目标元素的样式类名。
    *   **to**Type: [String](http://api.jquery.com/Types/#String)jQuery 选择器, 要转移到的目标元素。

当试图在两个元素之间呈现互动效果时，该特效非常有用。

被转移元素自己有一个样式类`ui-effects-transfer`，但此类需要开发者自己配置，例如添加背景颜色或边框。

## Example:

#### 点击绿色元素将其轮廓转移到另一个元素上。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>transfer demo</title>
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.10.3/themes/smoothness/jquery-ui.css">
  <style>
  div.green {
    width: 100px;
    height: 80px;
    background: green;
    border: 1px solid black;
    position: relative;
  }
  div.red {
    margin-top: 10px;
    width: 50px;
    height: 30px;
    background: red;
    border: 1px solid black;
    position: relative;
  }
  .ui-effects-transfer {
    border: 1px dotted black;
  }
  </style>
  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>
</head>
<body>

<div class="green"></div>
<div class="red"></div>

<script>
$( "div" ).click(function() {
  var i = 1 - $( "div" ).index( this );
  $( this ).effect( "transfer", { to: $( "div" ).eq( i ) }, 1000 );
});
</script>

</body>
</html> 
```