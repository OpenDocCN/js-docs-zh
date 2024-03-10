# Utility（实用功能）

## Utility（实用功能）

**Backbone.noConflict**`var backbone = Backbone.noConflict();` 返回 `Backbone` 对象的原始值。 您可以使用`Backbone.noConflict()`的返回值以保持局部引用 Backbone。 通常用于在第三方网站上引入了多个 Backbone 文件，避免冲突。

```
var localBackbone = Backbone.noConflict();
var model = localBackbone.Model.extend(...); 
```

**Backbone.$**`Backbone.$ = $;` 如果页面上有多个`jQuery`副本， 或者只是想告诉 Backbone 使用特定对象作为其 DOM / Ajax 库， 那么这个属性可以为您服务。 如果您正在使用 CommonJS 加载 Backbone （例如，节点，组件，或 browserify） 您必须手动设置该属性。

```
var Backbone.$ = require('jquery'); 
```