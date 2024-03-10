# API

# 默认配置

## 与 Jquery Mobile 自动初始化共同协作 Working with Jquery Mobile's Auto-initialization

不像其他的 Jq 项目，比如 jq 和 jq ui，Jquery Mobile 会在加载到增强特性时马上应用它（远早于 document.ready 事件发生时）。这些特性会基于 Jquery Mobile 的默认配置应用，是针对默认的情形设计的，他可能符合你的需求，也可能不符合。幸运的是，它很容易设置

**mobileinit 事件**

当 Jquery Mobile 开始执行时，他就会在 document 对象上触发 mobileinit 事件，所以你可以绑定别的行为来覆盖默认配置

```js
$(document).bind("mobileinit", function(){
//覆盖的代码
}); 
```

因为 mobileinit 事件是在加载后马上触发，所以你需要在 Jquery Mobile 加载之前绑定你的事件处理函数，所以我建议你如下安排你的 js 引用顺序

```js
<script src="Jquery.js"></script> 
<script src="custom-scripting.js"></script> 
<script src="Jquery-mobile.js"></script> 
```

在事件绑定内部，你可以设置你的默认配置，或者是使用 jq?.extend 方法扩展 $.mobile 对象

```js
$(document).bind("mobileinit", function(){
　$.extend( $.mobile , {
　foo: bar
　});
}); 
```

**或者单独设置它**

```js
$(document).bind("mobileinit", function(){
　$.mobile.foo = bar;
}); 
```

## 设置选项

以下的默认配置可以通过$.mobile 对象重新配置

```js
ns (_ 字符 _, 默认: ""): 
```

按照 data-属性格式安排的命名空间，例如：data-role,可以设置为任何东西，默认为空字符串。如果你包含一个面包屑的话用起来会比较明晰，比如 mynamespace-",会映射到 data-mynamespace-foo="...".

```js
subPageUrlKey (_ 字符串，_ 默认: "ui-page"): 
```

url 参数用来指向组件产生的子页面（比如生成的嵌套的列表）。会被转义为*example.html&ui-page=subpageIdentifier*.Jquery Mobile 会把 &ui-page=之前的部分用来向子页面的 url 地址发出 ajax 请求

```js
nonHistorySelectors (_ 字符串 _, 默认: "dialog"): 
```

对于带有 data-rel 属性的链接，或? data-role 属性的页面，如果选择器与之匹配，则他们不会在历史记录中被追踪 (即它们不会在 location.hash 中被更新，也不能加入到收藏夹?.

```js
activePageClass (**_ 字符 _ 串**, 默认: "ui-page-active"): 
```

给当前页面(包括转场中的) 分配 class

```js
activeBtnClass (_ 字符串 _, 默认: "ui-page-active"): 
```

给活动状态的按钮分配 class 值，该 class 值必须在 css 框架中存

```js
ajaxEnabled (_ 布尔值 _, 默认: true): 
```

Jquery Mobile 会自动通过 ajax 处理链接点击以及表单提交?如果无法处理，url hash 监听将会被禁用，url 也会像常规那样发出 HTTP 请求.

```js
ajaxLinksEnabled (_ 布尔值 _, 默认: true): 
```

可行时，Jquery Mobile 就会自动通过 ajax 处理链接的点击

```js
ajaxFormsEnabled (_ 布尔值 _, 默认: true): 
```

可行时，Jquery Mobile 就会自动通过 ajax 处理表单的提交

```js
hashListeningEnabled (_ 布尔值 _, 默认: true): 
```

Jquery Mobile 会自动监听与处理 location.hash 的改变。禁用它会防止 Jquery Mobile 处理 location.hash 的改?使你可以自己处理他们，或者在文档中用完整的链接地址指到一个特定的 id 值上

```js
defaultTransition (_ 字符串 _, 默认: 'slide'): 
```

设置默认的页面之间的转场效果。默认的对话框的转场效果为”pop?设为 none,则无转场效果

```js
loadingMessage (_ 字符串 _, 默认: "loading"): 
```

设置页面加载时显示的文本. 如果设置为 false 将不会显示任何文字

```js
pageLoadErrorMessage (_ 字符串 _, 默认: "Error Loading Page"): 
```

通过 ajax 加载页面失败时出现的文本

```js
gradeA (_ 返回一个布尔值 _, 默认: 返回$.support.mediaquery 的值: 
```

浏览器必须符合所有支持的条件才会返回 true.

# 事件

Jquery Mobile 提供了一些建于本地事件的自定义事件以用来创建一些有用的钩子. 要注意这些事件是建立于各种已存在的触摸事件之上，比如 鼠标和窗口事件，所以你可以通过使用 live() 或者 bind()将他们绑定到其他的 Jquery 事件

## 触摸事件 Touch events

**tap(轻击)：一次快速完整的轻击后触**

**taphold（轻击不放）：轻击并不放（大约一秒）后触**

**swipe(划动)：一秒内水平拖拽大于 30PX，同时纵向拖曳小?0px 的事件发生时触发**

**swipeleft（左划）：划动事件为向左的方向时触发**

**swiperight（右划）：划动事件为向右的方向时触发**

## 设备方向变化事件 Orientation change event

**orientationchange**

当设备的方向变化（设备横向持或纵向持）此事件被触发。绑定此事件时，你的回调函数可以加入第二个参数，作用为描述设备横或纵向的属性，"portrait"?quot;landscape"。这些值也会作为 class 值加入到 html 的元素中，使你可以通过 css 中的选择器改变他们的样式。注意当浏览器不支持 orientationChange 事件的时候可以通过 resize 事件绑定

## 滚屏事件 Scroll events

**scrollstart**

当屏幕滚动开始的时候触发。苹果的设备会在滚屏时冻结 DOM 的操作，当滚屏结束时按队列执行这些 dom 操作，我们现在正在研究方法让苹果的设备在滚屏开始前执行 dom 操作

**scrollstop**

滚屏结束时触发

## 滚屏事件 Scroll events

**scrollstart**

当屏幕滚动开始的时候触发。苹果的设备会在滚屏时冻结 DOM 的操作，当滚屏结束时按队列执行这些 dom 操作，我们现在正在研究方法让苹果的设备在滚屏开始前执行 dom 操作

**scrollstop**

滚屏结束时触发

## 页面显示/隐藏事件 Page show/hide events

在 Jquery Mobile 中，无论页面显示或是隐藏，都在该页面触发两个事件。哪个事件被触发取决于页面被显示还是隐藏，所以当页面转场发生时，实际?个事件被触发了，每个页面有两个：

pagebeforeshow：转场之前，页面被显示时触发

pagebeforehide：转场之前，页面被隐藏时触发

pageshow：转场之后，页面被显示时触发

pagehide：转场之后，页面被隐藏时触发

请注意这 4 个事件都引用了”上一页“，或”下一页“，这取决于哪一页被显示或者隐藏，以及”上一页“或者”下一页“是否存在。（第一个被显示的 page 并没?quot;上一?quot;可以引用，但是同样会引用一个空的 Jquery 对象 ），你可以通过将第二个参数作为一个绑定的回调函数访问这一引用

```js
$('div').live('pageshow',function(event, ui){
　alert('This page was just hidden: '+ ui.prevPage);
});

$('div').live('pagehide',function(event, ui){
　alert('This page was just shown: '+ ui.nextPage);
}); 
```

而且，务必在 Jquery Mobile 执行前绑定这些函数，以使 他们在初始化页面加载时被调用。在 mobileinit 事件的处理函数中使用它们既可，详情参?a href="globalconfig.html">global config

## 页面初始化事件 Page initialization events

Jquery Mobile 会自动基于 page"内的增强的约定自动初始化一些插件?例如：给一个 input 输入框约定了 type=range 属性会自动生成一个自定义滑动条

这些自动初始化的行为是受"page"插件控制的，它在执行前后部署部署事件，允许你在初始化前后操作页面，或者甚至自己提供初始化行为，禁止自动初始化。注以下的页面初始化事件在每个“page”只被触发一次，而显?隐藏 事件则不同，在页面显示或者隐藏的每次，它们都会被触发

pagebeforecreate：页面初始化时，初始化之前触

pagecreate：页面初始化时，初始化之后触

```js
$('#aboutPage').live('pagebeforecreate',function(event){
alert('This page was just inserted into the dom!');
});

$('#aboutPage').live('pagecreate',function(event){
alert('This page was just enhanced by Jquery Mobile!');
}); 
```

注意：通过绑定 pagebeforecreate 然后 return false，你禁止页面插件自己的操作

而且，务必在 Jquery Mobile 执行前绑定这些函数，以使 他们在初始化页面加载时被调用。在 mobileinit 事件的处理函数中使用它们既可，详情参?a href="globalconfig.html">global config

## 动画事件 Animation Events

Jquery Mobile 提供了 animationComplete 插件，你可以用来添加或删除一个 class 来应用 CSS 转场效果

# 方法

Jquery Mobile.mobile 对象提供了几种方法供你在应用中使用

## $.mobile.changePage (method)

通过程序跳转一个页面到另一个页面 ，以点击一个链接或者提交表单的形式出现(当那些特性被启用时）.

**参数**

**to**

字符串类 ，欲转到的页面的 url 地址，例如 ("about/us.html")

*   Jquery 对象 (`$("#about")`)

*   一个指定了两个页面引用的数组`[from，to]` ，用以在已知的 page 进行跳转. From 是当前所能看到的页面( 或者是 `$.mobile.activePage` ).

*   发送表单数据的对象. `{url: url, data: 序列化的表单数据 type: "get" or "post"}`

**transition** (字符串类型，例如 "pop", "slide"," "none")

**reverse**(字符串类型，默认: false). 设置为 true 时将导致一个反方向的转场

**changeHash**(布尔，默认: true). 页面改变完成时更新页面 url 的哈希值

**实例**

```js
//使用 slideup(上滑)的转场效果转到 about/us.html 页面 
　$.mobile.changePage("about/us.html", "slideup");

//转到 searchresults 页面，使用来自 id 为 search 的表单数
　$.mobile.changePage({
　　url: "searchresults.php", 
　　type: "get", 
　　data: $("form#search").serialize()
　}); 

//使用 pop 的转场效果转?./alerts/confirm.html 页面，不记录进历史记录当
　$.mobile.changePage("../alerts/confirm.html", "pop", false, false); 
```

## jqmData(), jqmRemoveData(), and jqmHasData() (method)

在 Jquery Mobile 中，jqmData,jqmRemoveData 应该用在 Jquery 核心的 data 和 removeData 方法?请注意这也包?$.fn.data, $.fn.removeData,?.data, $.removeData,以及$.hasData 方法)，因为他们会自动获取，设置命名空间的属性（即使当前没有命名空间被使用的情况下。）

**参数**

参见 Jquery 的 data 方法和 renovedata 方法

**并且**

当通过 Jquery 的 data 属性寻找元素时，请使用自定义的选择? jqmData() ，因为他在查询元素时会自动合并命名空间的 data 属性。例如，你应该使 `$("div:jqmData(role='page')")` ，而不是使`$("div[data-role='page']")`选择元素，因为前者会自动映射`$("div[data-"+ $.mobile.ns +"role='page']")`，你不需要把命名手动的连接成选择器

## $.mobile.pageLoading (*method*)

显示或隐藏页面加载消息，该消息由.mobile.loadingMessage 进行配置.

**参数**

```js
Done (_ 布尔 _, 默认为 false, 意味着加载已经开始. 设为 True 会隐藏 loading 消息 
```

**示例**

```js
// 显示页面加载消息
$.mobile.pageLoading(); 

// 隐藏页面加载消息
$.mobile.pageLoading(true); 
```

## $.mobile.path (methods, properties)

用来取得，设置，操作 url 地址

## mobile.base (methods, properties)

用来生成的根元素

## $.mobile.silentScroll (*method*)

不会触发任何事件，静默滚屏到特定的文档的 Y 值处

**参数**

```js
yPos (数字，默认为 0). 
```

**示例**

```js
//滚屏到 y 100px 处
$.mobile.silentScroll(100); 
```

## $.mobile.addResolutionBreakpoints (*method*)

值（数字或数组）。给分辨率 class 类添加任意的数字或数字数组。详细信息请参见 Orientation & resolution targeting.

**示例**

```js
//添加 400px 的分辨率断点
$.mobile.addResolutionBreakpoints(400);

//添加 2 个分辨率断点 
$.mobile.addResolutionBreakpoints([600,800]); 
```

**示例**

```js
//滚屏到 y 100px 处
$.mobile.silentScroll(100); 
```

## $.mobile.activePage (*property*)

引用当前活动的断

# 有响应的布局助手

## 媒体查询助手类 Media Query Helper Classes

Jquery Mobile 给 html 元素增加了用来模拟浏览器的水平竖直方向以及常用的最?最大宽度 css 媒介查询 class.这些 class 会在加载，调整大小以及方向变化时更新，使你能够在 css 中切断这些 class，以创建有响应的布局，即使在不支持媒介查询的浏览器中也可以实现

## 方向类 Orientation Classes

取决于浏览器或者设备的方向，HTML 元素总是会有"portrait"(竖屏) "landscape"(横屏) class. 你可以在 css 中如下使用它们:

```js
.portrait {
/* 垂直方向的变化的代码 */
}
.landscape {
/* 水平方向的变化的代码 */
} 
```

## 最小/最大宽度折断点 Class Min/Max Width Breakpoint Classes

默认情况下， 我们为如下宽度创建了折断： 320，80，68，024\. 这些宽度对应着如同这样的 class:"min-width-320px"，"max-width-480px"这意味着这些 class 可以应用在 替换(或附加) 它们模拟的等值的媒介查询

```js
.myelement { 
　float: none;
} 
.min-width-480px .myelement {
　float: left;
} 
```

Jquery Mobile 中的许多插件都利用了这些宽度折断点.例如，当浏览器宽度在 480 以上时，表单元素会浮动在 label 的旁边. 约束表单文本框的 CSS 在支持这样的行为时看起来像这样:

```js
label.ui-input-text { 
　display: block; 
}
.min-width-480px label.ui-input-text { 
　display: inline-block; 
} 
```

## 添加宽度折断点 Adding Width Breakpoints

要利用你自己的宽度折断点。Jquery Mobile 公开$.mobile.addResolutionBreakpoints 函数，该函数接受一个数字或者数字的数组，这些值无论何时在函数被应用到时会被添加到 min/max 折断点中.

```js
//添加一个 1200 像素的最大/最小折断点
$.mobile.addResolutionBreakpoints(1200);

///添加一个 1200 像素和 1400 像素 2 个最大/最小折断点
$.mobile.addResolutionBreakpoints([1200,1440]); 
```

## Running Media Queries 运行媒介查询

Jquery Mobile 提供一个函数允许你来测试是否有特殊的 css 媒介查询生效，只需调用 $.mobile.media()然后传递一个 media type 或 query 即可.如果浏览器支持你传递的那种 type 或 query，它会立即生效，函数会返回 true，否则会返回 false.

```js
//测试屏幕媒体类型
$.mobile.media("screen");

//测试最小宽度的媒介查询
$.mobile.media("screen and (min-width: 480px)");

//测试是否为苹果 4 代手机的屏幕（视网膜）
$.mobile.media("screen and (-webkit-min-device-pixel-ratio: 2)"); 
```

# 主题

## 主题样式综述 Theming overview

Jquery Mobile 中每一个布局和组件都被设计为一个全新的面向对象的 css 框架，使我们能够给站点和应用程序适用完全统一的视觉设计主题。Jquery Mobile 的主题样式系统与 Jquery UI 的 ThemeRoller 系统很类似，但是做出了几点重要的改进.他使用的**css3**来显示圆角，文字和盒阴影和颜色渐变，而不是图片，使得主题文件非常轻量级，减轻了服务器的负担主体框架包含了几套**颜色色板**。每一套都包含了可以自由混搭和匹配的头部栏，body，按钮状态。用来构建视觉纹理，创建丰富的设计**开放的主题框架**允许你创建最多 6 套主题样式，给设计增加近乎无限的多样性一套简化的图标集，包含了移动设备上大部分需要使用的图标，并且 sprite 到一张图片里减少了图片大小

## 主题与色板 Themes & swatches

主题系统的关键在于把针对颜色与材质的规则，和针对布局结构的规则（例如 padding 和尺寸）的定义相分离。这使得主体的颜色和材质在样式表中只需要定义一次，就可以在站点中混合，匹配以及结合，得到广泛的使用?每一套主题样式包括几项全局设置，包括字体阴影，按钮和盒模型的圆角值。另外，主题也包括几套颜色色板，每一个都定义了工具栏，内容区块，按钮和列表项的颜色以及字体的阴影 Jquery Mobile 默认内建了 5 套主题样式，用（a,b,c,d,e）引用。为了使我们的颜色主题能够保持一直地映射到我们的组件中，我们遵从的规约是：a 主题是视觉上最高级别的主题（黑色），b 主题为次级用主题（蓝色），c 主题为基准主题，在很多情况下是默认使用的，主题 d 为备用的次级内容用主题，主题 e 为强调用主题。 你也可以手动添加主题用于强调，或者是特殊的场合。例如：你可以手动添加新的主题“i",用于制作红色的工具栏或者按钮，用于错误提示全新的 ThemeRoller 工具会在 2011 年 Jquery Mobile 1.0 release 版本时发布。在这之前，也很容易手动编辑默认的基准样式而且/或者编辑 css 文件增加主题：拷贝主题样式那一段 css，将它用新的字母重命名，然后更换颜色

## Bars

默认的主题包含了一下的 5 种 bar 的样

![](img/Theming%20overview_1.png)默认情况下，Jquery Mobile 给所有的头部栏和尾部栏分配的是 a 主题，因为他们在应用中是视觉优先级最高的。如果要给 bar 设置一个不同的主题，只需要给头部栏和尾部栏容器增加 data-theme 属性，然后设定一个主题样式字母即可，例如 b,d 等? 更多参见工具栏主题样式

## 内容 Content Blocks

默认主题也包含了用于内容的颜色样式，使得在设计上与头部栏的颜色相匹配

![](img/Theming%20overview_2.png)如果没有特别指定的话，Jquery Mobile 会默认给 content 分配主题 c，使得在视觉上与头部栏区分开来![](img/Theming%20overview_3.png)

## 列表和按钮 Lists & Buttons

每一套主题也包含了针对交互元素，比如说列表项和按钮的默认样式

![](img/Theming%20overview_4.png)默认情况下，所有放置在一个 bar 里的按钮都会被自动分配一个和它所在的 bar 或者 box 的主题样式所匹配的主题，用以 在视觉上形成一个整体，像变色龙。![](img/Theming%20overview_6.png)这样的默认行为可以使你很容易地通过设置父容器的主题样式改变整个页面的主题，因为你知道按钮在不同主题的视觉配重都是一样的。而因为表单元素用按钮的样式，他们也会适配他们的父容器如果你要给按钮在视觉上进行强调，来帮助他从工具栏中凸现出来，可以给链接增加 data-theme="a"属性。给按钮在标记中设置了不同的主题后，父容器主题更改时框架不会覆盖其颜色，因为你决定了要设置它![](img/Theming%20overview_7.png)更过参见。。

## 全局“活动”状态 Global "Active" state

Jquery Mobile 框架用一个单独的主题叫做"active"(蓝色)，用来总是指示被选中的状态，无视该组件的主题. 我们给导航与表单元素应用了这样的"活动"主题，不管是否有指示被选中的状态的需要。因为这一个主题样式是设计用来给用户清晰的，一致的反馈的，所以不能通过标记来覆盖，在主题中该项只要设置一次，，Jquery Mobile 会在不管被选中或者活动状态需要时都应用他。该样式在样式表中的 ui-btn-active 规则来设置

“活动”状态用来给可切换的元素标记“on”状态

![](img/Theming%20overview_8.png)

## 图标 Icons

Jquery Mobile 包含了一套标准的图标，可以分配给按钮。为了尽量减小核心图标的文件大小，Jquery Mobile 只包含了图标白色的图案，然后在图标背后自动添加了半透明的黑色圆形背景，使得图标在所有背景色下都可以看的明晰