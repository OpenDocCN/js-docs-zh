# Backbone.Model（模型）

## Backbone.Model（模型）

**Models（模型）**是任何 Javascript 应用的核心，包括数据交互及与其相关的大量逻辑： 转换、验证、计算属性和访问控制。你可以用特定的方法扩展 **Backbone.Model**，**Model** 也提供了一组基本的管理变化的功能。

下面的示例演示了如何定义一个模型，包括自定义方法、设置属性、以及触发该属性变化的事件。一旦运行此代码后，`sidebar`在浏览器的控制台就可用，这样你就可以充分发挥了。

```js
var Sidebar = Backbone.Model.extend({
  promptColor: function() {
    var cssColor = prompt("Please enter a CSS color:");
    this.set({color: cssColor});
  }
});

window.sidebar = new Sidebar;

sidebar.on('change:color', function(model, color) {
  $('#sidebar').css({background: color});
});

sidebar.set({color: 'white'});

sidebar.promptColor(); 
```

**extend**`Backbone.Model.extend(properties, [classProperties])` 要创建自己的 **Model** 类，你可以扩展 **Backbone.Model** 并提供实例 **properties(属性)** ， 以及可选的可以直接注册到构造函数的**classProperties(类属性)**。

**extend** 可以正确的设置原型链，因此通过 **extend** 创建的子类 (subclasses) 也可以被深度扩展。

```js
var Note = Backbone.Model.extend({

  initialize: function() { ... },

  author: function() { ... },

  coordinates: function() { ... },

  allowedToEdit: function(account) {
    return true;
  }

});

var PrivateNote = Note.extend({

  allowedToEdit: function(account) {
    return account.owns(this);
  }

}); 
```

父类（`super`） 的简述：Javascript 没有提供一种直接调用父类的方式 — 如果你要重载原型链中上层定义的同名函数，如 `set`, 或 `save` ， 并且你想调用父对象的实现，这时需要明确的调用它，类似这样：

```js
var Note = Backbone.Model.extend({
  set: function(attributes, options) {
    Backbone.Model.prototype.set.apply(this, arguments);
    ...
  }
}); 
```

**constructor / initialize**`new Model([attributes], [options])` 当创建 model 实例时，可以传入 属性 (**attributes**)初始值，这些值会被 set （设置）到 model。 如果定义了 **initialize** 函数，该函数会在 model 创建后执行。

```js
new Book({
  title: "One Thousand and One Nights",
  author: "Scheherazade"
}); 
```

在极少数的情况下，你可能需要去重写 **constructor** ，它可以让你替换你的 model 的实际构造函数。

```js
var Library = Backbone.Model.extend({
  constructor: function() {
    this.books = new Books();
    Backbone.Model.apply(this, arguments);
  },
  parse: function(data, options) {
    this.books.reset(data.books);
    return data.library;
  }
}); 
```

如果你传入`{collection: ...}` ，这个 **options**表示这个 model 属于哪个`collection`，且用于计算这个 model 的 url。否则`model.collection` 这个属性会在你第一次添加 model 到一个 collection 的时候被自动添加。 需要注意的是相反的是不正确的，因为传递这个选项给构造函数将不会自动添加 model 到集合。有时这个是很有用的。

如果`{parse: true}`被作为一个**option**选项传递， **attributes**将在 set 到 model 之前首先通过 parse 被转换。

**get**`model.get(attribute)` 从当前 model 中获取当前属性(attributes)值，比如： `note.get("title")`

**set**`model.set(attributes, [options])` 向 model 设置一个或多个 hash 属性(attributes)。如果任何一个属性改变了 model 的状态，在不传入 {silent: true} 选项参数的情况下，会触发 `"change"` 事件，更改特定属性的事件也会触发。 可以绑定事件到某个属性，例如：`change:title`，及 `change:content`。

```js
note.set({title: "March 20", content: "In his eyes she eclipses..."});

book.set("title", "A Scandal in Bohemia"); 
```

**escape**`model.escape(attribute)` 与 get 类似，只是返回的是 HTML 转义后版本的 model 属性值。如果从 model 插入数据到 HTML，使用 escape 取数据可以避免 [XSS](http://en.wikipedia.org/wiki/Cross-site_scripting) 攻击。

```js
var hacker = new Backbone.Model({
  name: "<script>alert('xss')</script>"
});

alert(hacker.escape('name')); 
```

**has**`model.has(attribute)` 属性值为非 null 或非 undefined 时返回 `true`。

```js
if (note.has("title")) {
  ...
} 
```

**unset**`model.unset(attribute, [options])` 从内部属性散列表中删除指定属性(attribute)。 如果未设置 `silent` 选项，会触发 `"change"` 事件。

**clear**`model.clear([options])` 从 model 中删除所有属性， 包括`id`属性。 如果未设置 `silent` 选项，会触发 `"change"` 事件。

**id**`model.id` id 是 model 的特殊属性，可以是任意字符串（整型 **id** 或 UUID）。在属性中设置的 **id** 会被直接拷贝到 model 属性上。 我们可以从集合（collections）中通过 id 获取 model，另外 id 通常用于生成 model 的 URLs。

**idAttribute**`model.idAttribute` 一个 model 的唯一标示符，被储存在 `id` 属性下。如果使用一个不同的唯一的 key 直接和后端通信。可以设置 Model 的 `idAttribute` 到一个从 key 到 `id` 的一个透明映射中。

```js
var Meal = Backbone.Model.extend({
  idAttribute: "_id"
});

var cake = new Meal({ _id: 1, name: "Cake" });
alert("Cake id: " + cake.id); 
```

**cid**`model.cid` model 的特殊属性，**cid** 或客户 id 是当所有 model 创建时自动产生的唯一标识符。 客户 ids 在 model 尚未保存到服务器之前便存在，此时 model 可能仍不具有最终的 **id**， 但已经需要在用户界面可见。

**attributes**`model.attributes` **attributes** 属性是包含模型状态的内部散列表 — 通常（但不一定）JSON 对象的形式表示在服务器上模型数据 。它通常是数据库中一个行的简单的序列，但它也可以是客户端的计算状态。

建议采用 set 更新 **attributes**而不要直接修改。 如果您想检索和获取模型属性的副本， 用 `_.clone(model.attributes)` 取而代之。

由于这样的事实： Events（事件）接受空格分隔事件列表， 但是属性名称不应该包括空格。

**changed**`model.changed` **changed**属性是一个包含所有属性的内部散列，自最后 set 已改变。 自最后一组已改变。 请不要直接更新 **changed**，因为它的状态是由 set 内部维护。 **changed**的副本可从 changedAttributes 获得。

**defaults**`model.defaults or model.defaults()` **defaults** 散列（或函数）用于为模型指定默认属性。 创建模型实例时，任何未指定的属性会被设置为其默认值。

```js
var Meal = Backbone.Model.extend({
  defaults: {
    "appetizer":  "caesar salad",
    "entree":     "ravioli",
    "dessert":    "cheesecake"
  }
});

alert("Dessert will be " + (new Meal).get('dessert')); 
```

需要提醒的是，在 Javascript 中，对象是按引用传值的，因此如果包含一个对象作为默认值，它会被所有实例共享。可以定义 **defaults**为一个函数取代。

**toJSON**`model.toJSON([options])` 返回一个模型的 attributes 浅拷贝副本的 JSON 字符串化形式。 它可用于模型的持久化、序列化，或者发送到服务之前的扩充。 该方法名称比较混乱，因为它事实上并不返回 JSON 字符串， 但这是对 [JavaScript API 的 **JSON.stringify**](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#toJSON_behavior) 实现。

```js
var artist = new Backbone.Model({
  firstName: "Wassily",
  lastName: "Kandinsky"
});

artist.set({birthday: "December 16, 1866"});

alert(JSON.stringify(artist)); 
```

**sync**`model.sync(method, model, [options])` 使用 Backbone.sync 可以将一个模型的状态持续发送到服务器。 可以自定义行为覆盖。

**fetch**`model.fetch([options])` 通过委托给 Backbone.sync 从服务器重置模型的状态。返回[jqXHR](http://www.css88.com/jqapi-1.9/jQuery.ajax/#jqXHR)。 如果模型从未填充数据时非常有用， 或者如果你想确保你有最新的服务器状态。 如果服务器的状态不同于当前属性的`"change"`事件将被触发。 接受 `success` 和 `error`回调的选项散列， 这两个回调都可以传递`(model, response, options)`作为参数。

```js
// 每隔 10 秒从服务器拉取数据以保持频道模型是最新的
setInterval(function() {
  channel.fetch();
}, 10000); 
```

**save**`model.save([attributes], [options])` 通过委托给 Backbone.sync，保存模型到数据库（或替代持久化层）。 如果验证成功，返回[jqXHR](http://www.css88.com/jqapi-1.9/jQuery.ajax/#jqXHR)，否则为 `false`。 **attributes**散列（如 set）应包含你想改变的属性 - 不涉及的键不会被修改 - 但是，该资源的一个*完整表示*将被发送到服务器。 至于`set`，你可能会传递单独的键和值，而不是一个哈希值。 如果模型有一个 validate 方法，并且验证失败， 该模型将不会被保存。 如果模型 isNew， 保存将采用`"create"`（HTTP `POST`）， 如果模型在服务器上已经存在， 保存将采用`"update"`（HTTP `PUT`）。

相反，如果你只想将*改变*属性发送到服务器， 调用`model.save(attrs, {patch: true})`。 你会得到一个 HTTP `PATCH`请求将刚刚传入的属性发送到服务器。

通过新的属性调用`save` 将立即触发一个`"change"`事件，一个`"request"`事件作为 Ajax 请求开始到服务器， 并且当服务器确认成功修改后立即触发 一个`"sync"`事件。 如果你想在模型上等待服务器设置新的属性，请传递`{wait: true}`。

在下面的例子中， 注意我们如何覆盖`Backbone.sync`的版本，在模型初次保存时接收到 `"create"`请求，第二次接收到 `"update"` 请求的。

```js
Backbone.sync = function(method, model) {
  alert(method + ": " + JSON.stringify(model));
  model.set('id', 1);
};

var book = new Backbone.Model({
  title: "The Rough Riders",
  author: "Theodore Roosevelt"
});

book.save();

book.save({author: "Teddy"}); 
```

**save** 支持在选项散列表中传入 `success` 和 `error` 回调函数， 回调函数支持传入 `(model, response, options)` 作为参数。 如果服务端验证失败，返回非 `200` 的 HTTP 响应码，将产生文本或 JSON 的错误内容。

```js
book.save("author", "F.D.R.", {error: function(){ ... }}); 
```

**destroy**`model.destroy([options])` 通过委托给 Backbone.sync，保存模型到数据库（或替代持久化层）。 通过委托一个 HTTP `DELETE`请求给 Backbone.sync 破坏服务器上的模型。 返回一个[jqXHR](http://www.css88.com/jqapi-1.9/jQuery.ajax/#jqXHR)对象， 或者如果模型 isNew，那么返回`false`。 选项散列表中接受 `success` 和 `error` 回调函数， 回调函数支持传入 `(model, response, options)` 作为参数。 在模型上触发 `"destroy"` 事件，该事件将会冒泡到任何包含这个模型的集合中， 一个`"request"`事件作为 Ajax 请求开始到服务器， 并且当服务器确认模型被删除后立即触发 一个`"sync"`事件。如果你想在集合中删除这个模型前等待服务器相应，请传递`{wait: true}`。

```js
book.destroy({success: function(model, response) {
  ...
}}); 
```

**Underscore 方法 (6)** Backbone 代理了 **Underscore.js**用来给**Backbone.Model**提供 6 个对象函数。这里没有完全记录他们，但你可以看看 Underscore 文档中全部详情… (愚人码头注：下面链接已经替换成中文文档的地址)

*   [keys](http://www.css88.com/doc/underscore/#keys)
*   [values](http://www.css88.com/doc/underscore/#values)
*   [pairs](http://www.css88.com/doc/underscore/#pairs)
*   [invert](http://www.css88.com/doc/underscore/#invert)
*   [pick](http://www.css88.com/doc/underscore/#pick)
*   [omit](http://www.css88.com/doc/underscore/#omit)

```js
user.pick('first_name', 'last_name', 'email');

chapters.keys().join(', '); 
```

**validate**`model.validate(attributes, options)` 这种方法是未定义的， 如果您有任何可以在 JavaScript 中执行的代码 并且我们鼓励你用你自定义验证逻辑覆盖它 。 默认情况下**validate**在`save`之前调用， 但如果传递了 `{validate:true}`，也可以在`set`之前调用。 **validate**方法是通过模型的属性， 选项和`set` 和 `save`是一样的。 如果属性是有效的， **validate**不返回验证任何东西; 如果它们是无效的， 返回一个你选择的错误。 它可以是一个用来显示的简单的字符串错误信息， 或一个以编程方式描述错误的完整错误对象。 如果**validate**返回一个错误， `save`不会继续， 并且在服务器上该模型的属性将不被修改。 校验失败将触发`"invalid"`事件， 并用此方法返回的值设置模型上的`validationError`属性。

```js
var Chapter = Backbone.Model.extend({
  validate: function(attrs, options) {
    if (attrs.end < attrs.start) {
      return "can't end before it starts";
    }
  }
});

var one = new Chapter({
  title : "Chapter One: The Beginning"
});

one.on("invalid", function(model, error) {
  alert(model.get("title") + " " + error);
});

one.save({
  start: 15,
  end:   10
}); 
```

`"invalid"`事件提供粗粒度的错误信息 在模型或集合层面上是很有用。

**validationError**`model.validationError` 用 validate 最后验证失败时返回的值。

**isValid**`model.isValid()` 运行 validate 来检查模型状态。

```js
var Chapter = Backbone.Model.extend({
  validate: function(attrs, options) {
    if (attrs.end < attrs.start) {
      return "can't end before it starts";
    }
  }
});

var one = new Chapter({
  title : "Chapter One: The Beginning"
});

one.set({
  start: 15,
  end:   10
});

if (!one.isValid()) {
  alert(one.get("title") + " " + one.validationError);
} 
```

**url**`model.url()` 返回模型资源在服务器上位置的相对 URL 。 如果模型放在其它地方，可通过合理的逻辑重载该方法。 生成 URLs 的默认形式为：`"/[collection.url]/[id]"`， 如果模型不是集合的一部分，你可以通过指定明确的`urlRoot`覆盖。

由于是委托到 Collection#url 来生成 URL， 所以首先需要确认它是否定义过，或者所有模型共享一个通用根 URL 时，是否存在 urlRoot 属性。 例如，一个 id 为 `101` 的模型，存储在 `url` 为 `"/documents/7/notes"` 的 Backbone.Collection 中， 那么该模型的 URL 为：`"/documents/7/notes/101"`

**urlRoot**`model.urlRoot or model.urlRoot()` 如果使用的集合*外部*的模型，通过指定 `urlRoot` 来设置生成基于模型 id 的 URLs 的默认 url 函数。 `"[urlRoot]/id"`。通常情况下，你不会需要定义这一点。 需要注意的是`urlRoot`也可以是一个函数。

```js
var Book = Backbone.Model.extend({urlRoot : '/books'});

var solaris = new Book({id: "1083-lem-solaris"});

alert(solaris.url()); 
```

**parse**`model.parse(response, options)` **parse** 会在通过 fetch 从服务器返回模型数据，以及 save 时执行。 传入本函数的为原始 `response` 对象，并且应当返回可以 set 到模型的属性散列表。 默认实现是自动进行的，仅简单传入 JSON 响应。 如果需要使用已存在的 API，或者更好的命名空间响应，可以重载它。

如果使用的 3.1 版本之前的 Rails 后端，需要注意 Rails's 默认的 `to_json` 实现已经包含了命名空间之下的模型属性。 对于无缝的后端集成环境禁用这种行为：

```js
ActiveRecord::Base.include_root_in_json = false 
```

**clone**`model.clone()` 返回该模型的具有相同属性的新实例。

**isNew**`model.isNew()` 模型是否已经保存到服务器。 如果模型尚无 `id`，则被视为新的。

**hasChanged**`model.hasChanged([attribute])` 标识模型从上次 set 事件发生后是否改变过。 如果传入 **attribute** ，当指定属性改变后返回 `true`。

注意，本方法以及接下来 change 相关的方法，仅对 `"change"`事件发生有效。

```js
book.on("change", function() {
  if (book.hasChanged("title")) {
    ...
  }
}); 
```

**changedAttributes**`model.changedAttributes([attributes])` 只从最后一次 set 开始检索已改变的模型属性散列（hash）， 或者如果没有，返回 `false`。 作为可选，可以传递外部属性哈希（hash）， 返回与该模型不同的属性的哈希（hash）。 这可以用来找出视图的哪些部分应该更新，或者确定哪些需要与服务器进行同步。

**previous**`model.previous(attribute)` 在 `"change"` 事件发生的过程中，本方法可被用于获取已改变属性的旧值。

```js
var bill = new Backbone.Model({
  name: "Bill Smith"
});

bill.on("change:name", function(model, name) {
  alert("Changed name from " + bill.previous("name") + " to " + name);
});

bill.set({name : "Bill Jones"}); 
```

**previousAttributes**`model.previousAttributes()` 返回模型的上一个属性的副本。一般用于获取模型的不同版本之间的区别，或者当发生错误时回滚模型状态。