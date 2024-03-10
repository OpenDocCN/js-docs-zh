# Backbone.View（视图）

## Backbone.View（视图）

Backbone 视图几乎约定比他们的代码多 — 他们并不限定你的 HTML 或 CSS， 并可以配合使用任何 JavaScript 模板库。 一般是组织您的接口转换成逻辑视图， 通过模型的支持， 模型变化时， 每一个都可以独立地进行更新， 而不必重新绘制该页面。我们再也不必钻进 JSON 对象中，查找 DOM 元素，手动更新 HTML 了，通过绑定视图的 `render` 函数到模型的 `"change"` 事件 — 模型数据会即时的显示在 UI 中。

**extend**`Backbone.View.extend(properties, [classProperties])` 开始创建自定义的视图类。 通常我们需要重载 render 函数，声明 events， 以及通过 `tagName`, `className`, 或 `id` 为视图指定根元素。

```
var DocumentRow = Backbone.View.extend({

  tagName: "li",

  className: "document-row",

  events: {
    "click .icon":          "open",
    "click .button.edit":   "openEditDialog",
    "click .button.delete": "destroy"
  },

  initialize: function() {
    this.listenTo(this.model, "change", this.render);
  },

  render: function() {
    ...
  }

}); 
```

直到运行时， 像`tagName`, `id`, `className`, `el`, 和 `events`这样的属性也可以被定义为一个函数，

**constructor / initialize**`new View([options])` 有几个特殊的选项， 如果传入，则直接注册到视图中去： `model`, `collection`, `el`, `id`, `className`, `tagName`, `attributes` 和 `events`。 如果视图定义了一个**initialize**初始化函数， 首先创建视图时，它会立刻被调用。 如果希望创建一个指向 DOM 中已存在的元素的视图，传入该元素作为选项：`new View({el: existingElement})`。

```
var doc = documents.first();

new DocumentRow({
  model: doc,
  id: "document-row-" + doc.id
}); 
```

**el**`view.el` 所有的视图都拥有一个 DOM 元素（**el** 属性），即使该元素仍未插入页面中去。 视图可以在任何时候渲染，然后一次性插入 DOM 中去，这样能尽量减少 reflows 和 repaints 从而获得高性能的 UI 渲染。 `this.el` 可以从视图的 `tagName`, `className`, `id` 和 `attributes` 创建，如果都未指定，**el** 会是一个空 `div`。

```
var ItemView = Backbone.View.extend({
  tagName: 'li'
});

var BodyView = Backbone.View.extend({
  el: 'body'
});

var item = new ItemView();
var body = new BodyView();

alert(item.el + ' ' + body.el); 
```

**$el**`view.$el` 一个视图元素的缓存 jQuery 对象。 一个简单的引用，而不是重新包装的 DOM 元素。

```
view.$el.show();

listView.$el.append(itemView.el); 
```

**setElement**`view.setElement(element)` 如果你想应用一个 Backbone 视图到不同的 DOM 元素， 使用**setElement**， 这也将创造缓存`$el`引用，视图的委托事件从旧元素移动到新元素上。

**attributes**`view.attributes` 属性的键值对， 将被设置为视图`el`上的 HTML DOM 元素的属性， 或者是返回这样的键值对的一个函数。

**$ (jQuery)**`view.$(selector)` 如果页面中引入了 jQuery，每个视图都将拥有 **$** 函数，可以在视图元素查询作用域内运行。 如果使用该作用域内的 jQuery 函数，就不需要从列表中指定的元素获取模型的 ids 这种查询了，我们可以更多的依赖 HTML class 属性。 它等价于运行：`view.$el.find(selector)`。

```
ui.Chapter = Backbone.View.extend({
  serialize : function() {
    return {
      title: this.$(".title").text(),
      start: this.$(".start-page").text(),
      end:   this.$(".end-page").text()
    };
  }
}); 
```

**template**`view.template([data])` 虽然模板化的视图 不是 Backbone 直接提供的一个功能， 它往往是一个在你视图定义**template**函数很好的约定。 如此， 渲染你的视图时， 您方便地访问实例数据。 例如，使用 Underscore 的模板：

```
var LibraryView = Backbone.View.extend({
  template: _.template(...)
}); 
```

**render**`view.render()` **render** 默认实现是没有操作的。 重载本函数可以实现从模型数据渲染视图模板，并可用新的 HTML 更新 `this.el`。 推荐的做法是在 **render** 函数的末尾 `return this` 以开启链式调用。

```
var Bookmark = Backbone.View.extend({
  template: _.template(...),
  render: function() {
    this.$el.html(this.template(this.model.attributes));
    return this;
  }
}); 
```

Backbone 并不知道您首选 HTML 模板的方法。 **render**（渲染） 函数中可以采用拼接 HTML 字符串，， 或者使用`document.createElement`生成 DOM 树。 但还是建议选择一个好的 Javascript 模板引擎。 [Mustache.js](http://github.com/janl/mustache.js), [Haml-js](http://github.com/creationix/haml-js), 和 [Eco](http://github.com/sstephenson/eco) 都是很好的选择。 因为[Underscore.js](http://www.css88.com/doc/underscore/)已经引入页面了，如果你喜欢简单的插入 JavaScript 的样式模板。 [_.template](http://www.css88.com/doc/underscore/#template)可以使用并是一个很好的选择。

无论基于什么考虑，都*永远*不要在 Javascript 中拼接 HTML 字符串。 在 DocumentCloud 中， 我们使用[Jammit](http://documentcloud.github.com/jammit/) 来打包 JavaScript 模板，并存储在`/app/views`中，作为我们主要的`core.js`包的一部分。

**remove**`view.remove()` 从 DOM 中移除一个视图。同事调用 stopListening 来移除通过 listenTo 绑定在视图上的 所有事件。

**delegateEvents**`delegateEvents([events])` 采用 jQuery 的`on`函数来为视图内的 DOM 事件提供回调函数声明。 如果未传入 **events** 对象，使用 `this.events` 作为事件源。 事件对象的书写格式为 `{"event selector": "callback"}`。 省略 `selector` 则事件被绑定到视图的根元素（`this.el`）。 默认情况下，`delegateEvents` 会在视图的构造函数内被调用，因此如果有 `events` 对象，所有的 DOM 事件已经被连接， 并且我们永远不需要去手动调用本函数。

`events` 属性也可以被定义成返回 **events** 对象的函数，这样让我们定义事件，以及实现事件的继承变得更加方便。

视图 render 期间使用 **delegateEvents** 相比用 jQuery 向子元素绑定事件有更多优点。 所有注册的函数在传递给 jQuery 之前已被绑定到视图上，因此当回调函数执行时， `this` 仍将指向视图对象。 当 **delegateEvents** 再次运行，此时或许需要一个不同的 `events` 对象，所以所有回调函数将被移除，然后重新委托 — 这对模型不同行为也不同的视图挺有用处。

搜索结果页面显示文档的视图看起来类似这样：

```
var DocumentView = Backbone.View.extend({

  events: {
    "dblclick"                : "open",
    "click .icon.doc"         : "select",
    "contextmenu .icon.doc"   : "showMenu",
    "click .show_notes"       : "toggleNotes",
    "click .title .lock"      : "editAccessLevel",
    "mouseover .title .date"  : "showTooltip"
  },

  render: function() {
    this.$el.html(this.template(this.model.attributes));
    return this;
  },

  open: function() {
    window.open(this.model.get("viewer_url"));
  },

  select: function() {
    this.model.set({selected: true});
  },

  ...

}); 
```

**undelegateEvents**`undelegateEvents()` 删除视图所有委托事件。如果要从临时的 DOM 中禁用或删除视图时，比较有用。