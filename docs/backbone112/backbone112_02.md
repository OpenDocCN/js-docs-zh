# 升级到 1.1

## 升级到 1.1

从 Backbone **0.9.X**系列版本升级到 **1.1** 应该是相当容易的。如果你从旧版本升级， 一定要检查更新日志。简单地说，一些大规模的重大更改是：

*   如果你想漂亮的更新一个 Collection(集合)的内容，增加新的 models（模型），删除丢失，和合并那些已经存在，你现在可以调用 set(以前叫做"update") ，Model（模型）类似的操作也调用`set`。这是目前默认的，当你在 collection（集合）上调用 fetch 时。为了得到旧的行为，传递`{reset: true}`。
*   如果你的 URL 片段中有字符，需要 URL 编码，Backbone 现在会在你路由处理程序接收它们作为参数前为你解码（跨浏览器规范的行为）。
*   在**0.9.x**中，Backbone 事件有了两个新的方法：listenTo 和 stopListening， 这使得它能更容易地创建 Views（视图）监听，当你想 remove view（视图）时，解除他们所有绑定的监听。
*   model（模型）验证现在只默认执行在 save 中 —不再执行在 set 中，除非传递了`{validate:true}`选项。model（模型）验证现在会触发一个 `"invalid"`事件，而不是`"error"`事件。
*   在 1.1 中 ，Backbone Views（视图）不再有 `options` 参数自动附加在`this.options`上。如果你喜欢可以继续附加。
*   在 1.1 中 ，**Collection**的 `add`, `remove`, `set`, `push`, 和 `shift` 方法现在返回来自 collection（集合）的 models（模型）(或 models)。