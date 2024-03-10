# 综述

# 综述

# Jquery mobile 介绍 Jquery Mobile Overview

# Jquery mobile 介绍 Jquery Mobile Overview

Jquery Mobile 的策略可以很容易的概括：创建一个顶级的 javascript 库，在不同的智能手机和桌面电脑的 web 浏览器上,形成统一的用户 ui.

要达到这个目标最关键的就是通过 Jquery Mobile 解决移动平台的多样性。我们一直致力于使 Jquery 支持所有的性能足够的和在市场占有一定份额的移动设备浏览器.所以 我们将手机网页浏览器和桌面浏览器的 Jquery 开发做同等重要的对待。

为了使设备设备浏览器能够广泛地支持，应用 Jquery Mobile 的项目的所有页面都必须**是干净的系统化的 html 页面**，来保证良好的兼容性， 在这些设备中 解析 css 和 javascript 的过程中，Jquery Mobile 应用**渐进增强技术**将语义化的页面转化成富媒体的浏览体验。而可访问性的问题，比如 WAI-ARIA，已经通过通过框架已经紧密集成进来，以给屏幕阅读器或者其他辅助设备（主要指手持设备）提供支持。

![](img/ipad-palm.jpg)

# 关键特性： Key features:

# 关键特性： Key features:

1**构建于 Jquery 的核心之上**。使之兼容于 jq 的语法，对于开发人员有最易的开发曲线

**2 兼容于所有的主流移动设备**:iOS, Android, Blackberry, Palm WebOS, Nokia/Symbian, Windows Mobile, bada, MeeGo .

**3 轻量级** 压缩后只 12k，对图片的依赖程度非常低，保证了速度

4 页面和行为均**基于 html5 标记的驱动进行配**，开发效率高，对脚本的需求小

**5 渐进增强**使所有的移动设备，平板电脑和 pc 电脑都支持核心的内容和方法。而对于新的移动平台，则可以展现像安装在设备中的应用程序一样出色的富媒体和交互的浏览体验

**6 自动初始化** 通过页面的 html 标签的 data-role 属性，Jquery Mobile 可以自动初始化相应的插件

**7 优秀的可访问性** 一些特性比如 WAI-ARIA 也包含在内，以确保页面也可以在一些屏幕阅读器(比如苹果的 VoiceOver)或者其他手持设备中正常工作.

**8 新的事件**增加了触摸屏设备支持的触摸，鼠标，和基于光标的输入方法的 API

9 增加了本地控制的优化触摸体验和主题样式的**新的插件**

**9 强大的主题样式框**和主题编辑器能很容易的进行高度个性化和品牌化的的界面定制

# 可访问性 Accessibility

# 可访问性 Accessibility

Jquery Mobile 是基于标准的，系统化的 html 构建的，使得页面能够在最广范围的设备上得到支持。对于 A 级的浏览器，许多 Jquery Mobile 组件，比"焦点管理","键盘导航"等都能支持，其他可以详细参加 W3C 的 WAI-ARIA 说明.

通过运用这些技术，我致力于使得通过 Jquery Mobile 开发的 web 产品拥有最好的可访问性，对于伤残人士，例如盲人，也可以用读屏软件，例如 iphone 的 voiceover,使用。

我们现在正在改进可访问性，我们的目标是在 1.0 版本的时候，使 Jquery mobile 的所有控件都拥有全部的可访问性。

# a4 版本支持的平台 Supported platforms in Alpha 4

# a4 版本支持的平台 Supported platforms in Alpha 4

在 A4 版本中，以下平台和浏览器会支持全部的功能，页面的渲染也是无误的。现在 WP7 也支持了

• Apple iOS (3.1-4.2): iPhone, iPod Touch, iPad 测试通过

• Android (1.6-2.3): 所有设备均支持，在 HTC Incredible, Motorola Droid, Google G1 and Nook Color 测试通过

• Blackberry 6: 触摸操作和样式已测试通过

• Windows Phone 7: HTC 手机上已通过

• Palm WebOS (1.4): tested on Pre, Pixi

• Opera Mobile (10.1): 安卓

• Opera Mini (5.02): iOS, 安卓

• Firefox Mobile (beta): 安卓