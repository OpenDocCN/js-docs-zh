# Download Zepto

# Download Zepto

默认构建包含以下模块： *Core, Ajax, Event, Form, IE*.

Zepto v1.0 默认捆绑了 Effects, iOS3, 和 Detect 模块。 请参阅下面的 可选模块(optional modules)。

*   [zepto.js v1.1.6 (for development)](http://zeptojs.com/zepto.js) – *54.6k uncompressed, lots of comments*
*   [zepto.min.js v1.1.6 (for production)](http://zeptojs.com/zepto.min.js) – *9.1k when gzipped*

Or **[grab the latest version on GitHub](https://github.com/madrobby/zepto)**.

用一个 script 标签引入 Zepto 到你的页面的底部：

```
...
<script src=zepto.min.js></script>
</body>
</html> 
```

如果`$`变量尚未定义，Zepto 只设置全局变量`$`指向它本身。 没有`Zepto.noConflict`方法。

**如果你需要支持旧的浏览器，如 Internet Explorer 9 或以下，你可以退回到 jQuery 的 1.x。**