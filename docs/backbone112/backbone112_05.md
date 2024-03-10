# Backbone.Collection（集合）

## Backbone.Collection（集合）

集合是模型的有序组合，我们可以在集合上绑定 `"change"` 事件，从而当集合中的模型发生变化时`fetch`（获得）通知，集合也可以监听 `"add"` 和 `"remove"` 事件， 从服务器更新，并能使用 Underscore.js 提供的方法。

集合中的模型触发的任何事件都可以在集合身上直接触发，所以我们可以监听集合中模型的变化： `documents.on("change:selected", ...)`

**extend**`Backbone.Collection.extend(properties, [classProperties])` 通过扩展 **Backbone.Collection** 创建一个 **Collection** 类。实例属性参数 **properties** 以及 类属性参数 **classProperties** 会被直接注册到集合的构造函数。

**model**`collection.model` 覆盖此属性来指定集合中包含的模型类。可以传入原始属性对象（和数组）来 add, create,和 reset，传入的属性会被自动转换为适合的模型类型。

```js
var Library = Backbone.Collection.extend({
  model: Book
}); 
```

集合也可以包含多态模型，通过用构造函数重写这个属性，返回一个模型。

```js
var Library = Backbone.Collection.extend({

  model: function(attrs, options) {
    if (condition) {
      return new PublicDocument(attrs, options);
    } else {
      return new PrivateDocument(attrs, options);
    }
  }

}); 
```

**constructor / initialize**`new Backbone.Collection([models], [options])` 当创建集合时，你可以选择传入初始的 **models** 数组。 集合的 comparator 函数也可以作为选项传入。 传递`false`作为 comparator 选项将阻止排序。 如果定义了 **initialize** 函数，会在集合创建时被调用。 有几个选项， 如果提供的话，将直接附加到集合上：`model` 和 `comparator`。 通过传递`null`给`models`选项来创建一个空的集合。

```js
var tabs = new TabSet([tab1, tab2, tab3]);
var spaces = new Backbone.Collection([], {
  model: Space
}); 
```

**models**`collection.models` 访问集合中模型的内置的 JavaScript 数组。通常我们使用 `get`， `at`，或 **Underscore 方法** 访问模型对象，但偶尔也需要直接访问。

**toJSON**`collection.toJSON([options])` 返回集合中包含的每个模型(通过 toJSON) 的属性哈希的数组。可用于集合的序列化和持久化。本方法名称容易引起混淆，因为它与 [JavaScript's JSON API](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#toJSON_behavior) 命名相同。

```js
var collection = new Backbone.Collection([
  {name: "Tim", age: 5},
  {name: "Ida", age: 26},
  {name: "Rob", age: 55}
]);

alert(JSON.stringify(collection)); 
```

**sync**`collection.sync(method, collection, [options])` 使用 Backbone.sync 来将一个集合的状态持久化到服务器。 可以自定义行为覆盖。

**Underscore 方法 (32)** Backbone 代理了 **Underscore.js**用来给**Backbone.Collection**提供 6 个对象函数。这里没有完全记录他们，但你可以看看 Underscore 文档中全部详情…(愚人码头注：下面链接已经替换成中文文档的地址)

*   [forEach (each)](http://www.css88.com/doc/underscore/#each)
*   [map (collect)](http://www.css88.com/doc/underscore/#map)
*   [reduce (foldl, inject)](http://www.css88.com/doc/underscore/#reduce)
*   [reduceRight (foldr)](http://www.css88.com/doc/underscore/#reduceRight)
*   [find (detect)](http://www.css88.com/doc/underscore/#find)
*   [filter (select)](http://www.css88.com/doc/underscore/#filter)
*   [reject](http://www.css88.com/doc/underscore/#reject)
*   [every (all)](http://www.css88.com/doc/underscore/#every)
*   [some (any)](http://www.css88.com/doc/underscore/#some)
*   [contains (include)](http://www.css88.com/doc/underscore/#contains)
*   [invoke](http://www.css88.com/doc/underscore/#invoke)
*   [max](http://www.css88.com/doc/underscore/#max)
*   [min](http://www.css88.com/doc/underscore/#min)
*   [sortBy](http://www.css88.com/doc/underscore/#sortBy)
*   [groupBy](http://www.css88.com/doc/underscore/#groupBy)
*   [shuffle](http://www.css88.com/doc/underscore/#shuffle)
*   [toArray](http://www.css88.com/doc/underscore/#toArray)
*   [size](http://www.css88.com/doc/underscore/#size)
*   [first (head, take)](http://www.css88.com/doc/underscore/#first)
*   [initial](http://www.css88.com/doc/underscore/#initial)
*   [rest (tail, drop)](http://www.css88.com/doc/underscore/#rest)
*   [last](http://www.css88.com/doc/underscore/#last)
*   [without](http://www.css88.com/doc/underscore/#without)
*   [indexOf](http://www.css88.com/doc/underscore/#indexOf)
*   [lastIndexOf](http://www.css88.com/doc/underscore/#lastIndexOf)
*   [isEmpty](http://www.css88.com/doc/underscore/#isEmpty)
*   [chain](http://www.css88.com/doc/underscore/#chain)
*   [difference](http://www.css88.com/doc/underscore/#difference)
*   [sample](http://www.css88.com/doc/underscore/#sample)
*   [partition](http://www.css88.com/doc/underscore/#partition)
*   [countBy](http://www.css88.com/doc/underscore/#countBy)
*   [indexBy](http://www.css88.com/doc/underscore/#indexBy)

```js
books.each(function(book) {
  book.publish();
});

var titles = books.map(function(book) {
  return book.get("title");
});

var publishedBooks = books.filter(function(book) {
  return book.get("published") === true;
});

var alphabetical = books.sortBy(function(book) {
  return book.author.get("name").toLowerCase();
}); 
```

**add**`collection.add(models, [options])` 向集合中增加一个模型（或一个模型数组），触发`"add"`事件。 如果已经定义了 model 属性， 您也可以通过原始属性的对象让其看起来像一个模型实例。 返回已经添加的（或预先存在的，如果重复）模式。 传递`{at: index}`可以将模型插入集合中特定的`index`索引位置。 如果您要添加 集合中已经存在的模型 到集合，他们会被忽略， 除非你传递`{merge: true}`， 在这种情况下，它们的属性将被合并到相应的模型中， 触发任何适当的`"change"` 事件。

```js
var ships = new Backbone.Collection;

ships.on("add", function(ship) {
  alert("Ahoy " + ship.get("name") + "!");
});

ships.add([
  {name: "Flying Dutchman"},
  {name: "Black Pearl"}
]); 
```

请注意，添加相同的模型（具有相同`id`的模型）到一个集合，一次以上 是空操作。

**remove**`collection.remove(models, [options])` 从集合中删除一个模型（或一个模型数组），并且返回他们。会触发 `"remove"` 事件，同样可以使用 `silent` 关闭。移除前该模型的 index 可用作`options.index`类监听。

**reset**`collection.reset([models], [options])` 每次都是只添加和删除一个模型那没问题， 但有时，你需要改变很多模型，那么你宁愿只更新集合。 使用**reset**，将一个新的模型（或属性散列）列表替换集合，最后触发一个但单独的`"reset"`事件。 到与模型的新列表替换集合（或属性散列），触发一个单一的“复位”事件在末端。 返回新的模型集合。 为方便起见， 在一个 `"reset"`事件中， 任何以前的模型列表可作为`options.previousModels`。 通过传递`null`给`models`选项来清空你的集合。

下面是一个例子 使用**reset**来引导一个集合在页面初始化时加载， 在 Rails 应用程序中：

```js
<script>
  var accounts = new Backbone.Collection;
  accounts.reset(<%= @accounts.to_json %>);
</script> 
```

调用`collection.reset()`，不传递任何模型作为参数 将清空整个集合。

**set**`collection.set(models, [options])` **set**方法通过传递模型列表执行一个集合的"smart(智能)"的更新。 如果列表中的一个模型尚不在集合中，那么它将被添加; 如果模型已经在集合中，其属性将被合并; 并且如果集合包含*不*存在于列表中的任何模型，他们将被删除。 以上所有将触发相应的`"add"`, `"remove"`, 和 `"change"`事件。 返回集合中的模型。 如果您想自定义的行为， 你可以设置选项：`{add: false}`, `{remove: false}`, 或 `{merge: false}`，将其禁用。

```js
var vanHalen = new Backbone.Collection([eddie, alex, stone, roth]);

vanHalen.set([eddie, alex, stone, hagar]);

// Fires a "remove" event for roth, and an "add" event for "hagar".
// Updates any of stone, alex, and eddie's attributes that may have
// changed over the years. 
```

**get**`collection.get(id)` 通过一个 id，一个 cid，或者传递一个**model**来 获得集合中 的模型。

```js
var book = library.get(110); 
```

**at**`collection.at(index)` 获得集合中指定索引的模型。不论你是否对模型进行了重新排序， **at** 始终返回其在集合中插入时的索引值。

**push**`collection.push(model, [options])` 在集合尾部添加一个模型。选项和 add 相同。

**pop**`collection.pop([options])` 删除并且返回集合中最后一个模型。选项和 remove 相同。

**unshift**`collection.unshift(model, [options])` 在集合开始的地方添加一个模型。选项和 add 相同。

**shift**`collection.shift([options])` 删除并且返回集合中第一个模型。选项和 remove 相同。

**slice**`collection.slice(begin, end)` 返回一个集合的模型的浅拷贝副本，使用与原生[Array#slice](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)相同的选项。

**length**`collection.length` 与数组类似，集合拥有 `length` 属性，返回该集合包含的模型数量。

**comparator**`collection.comparator` 默认情况下，集合没有声明 **comparator** 函数。如果定义了该函数，集合中的模型会按照指定的算法进行排序。 换言之，被增加模型，会被插入 `collection.models`中适合的位置。 comparator 可以被定义为[sortBy](http://www.css88.com/doc/underscore/#sortBy)（传递带有一个参数的函数）， 作为一个[sort](https://developer.mozilla.org/JavaScript/Reference/Global_Objects/Array/sort)（传递一个一个参数函数需要两个参数）， 或者作为一个表示属性的字符串进行排序。

"sortBy"比较函数接受一个模型，并且返回一个该模型相对于其他模型的排序数字或字符串值。 "sort"比较函数接受两个模型，并且，如果第一个模型应该在第二模型个之前，返回`-1`； 如果他们是同一等级的，返回`0`； 如果第一个模型应该在第二模型个之后，返回`1`； *需要注意的是 Backbone 这两种风格的比较功能的确定 取决于参数个数。所以如果你绑定了比较函数，需要格外小心。*

注意即使下面例子中的 chapters 是后加入到集合中的，但它们都会遵循正确的排序：

```js
var Chapter  = Backbone.Model;
var chapters = new Backbone.Collection;

chapters.comparator = 'page';

chapters.add(new Chapter({page: 9, title: "The End"}));
chapters.add(new Chapter({page: 5, title: "The Middle"}));
chapters.add(new Chapter({page: 1, title: "The Beginning"}));

alert(chapters.pluck('title')); 
```

如果以后更改模型属性，带有比较函数的集合不会自动重新排序。 所以你不妨改变模型的属性后调用`sort`， 这会影响排序。

**sort**`collection.sort([options])` 强制对集合进行重排序。一般情况下不需要调用本函数，因为当一个模型被添加时， comparator 函数会实时排序。要禁用添加模型时的排序，可以传递`{sort: false}`给`add`。 调用**sort**会触发的集合的`"sort"`事件。

**pluck**`collection.pluck(attribute)` 从集合中的每个模型中拉取 attribute（属性）。等价于调用 `map`，并从迭代器中返回单个属性。

```js
var stooges = new Backbone.Collection([
  {name: "Curly"},
  {name: "Larry"},
  {name: "Moe"}
]);

var names = stooges.pluck("name");

alert(JSON.stringify(names)); 
```

**where**`collection.where(attributes)` 返回集合中所有匹配所传递 **attributes**（属性）的模型数组。 对于简单的`filter（过滤）`比较有用。

```js
var friends = new Backbone.Collection([
  {name: "Athos",      job: "Musketeer"},
  {name: "Porthos",    job: "Musketeer"},
  {name: "Aramis",     job: "Musketeer"},
  {name: "d'Artagnan", job: "Guard"},
]);

var musketeers = friends.where({job: "Musketeer"});

alert(musketeers.length); 
```

**findWhere**`collection.findWhere(attributes)` 就像 where， 不同的是**findWhere**直接返回匹配所传递 **attributes**（属性）的第一个模型。

**url**`collection.url or collection.url()` 设置 **url** 属性（或函数）以指定集合对应的服务器位置。集合内的模型使用 **url** 构造自身的 URLs。

```js
var Notes = Backbone.Collection.extend({
  url: '/notes'
});

// Or, something more sophisticated:

var Notes = Backbone.Collection.extend({
  url: function() {
    return this.document.url() + '/notes';
  }
}); 
```

**parse**`collection.parse(response, options)` 每一次调用 fetch 从服务器拉取集合的模型数据时，**parse**都会被调用。 本函数接收原始 `response` 对象，返回可以 added（添加） 到集合的模型属性数组。 默认实现是无需操作的，只需简单传入服务端返回的 JSON 对象。 如果需要处理遗留 API，或者在返回数据定义自己的命名空间，可以重写本函数。

```js
var Tweets = Backbone.Collection.extend({
  // The Twitter Search API returns tweets under "results".
  parse: function(response) {
    return response.results;
  }
}); 
```

**clone**`collection.clone()` 返回一个模型列表完全相同的集合新实例。

**fetch**`collection.fetch([options])` 从服务器拉取集合的默认模型设置 ，成功接收数据后会 setting（设置）集合。 **options** 支持 `success` 和 `error` 回调函数，两个回调函数接收 `(collection, response, options)`作为参数。当模型数据从服务器返回时， 它使用 set 来（智能的）合并所获取到的模型， 除非你传递了 `{reset: true}`， 在这种情况下，集合将（有效地）重置。 可以委托 Backbone.sync 在幕后自定义持久性策略 并返回一个[jqXHR](http://www.css88.com/jqapi-1.9/jQuery.ajax/#jqXHR)。 **fetch**请求的服务器处理器应该返回模型 JSON 数组。

```js
Backbone.sync = function(method, model) {
  alert(method + ": " + model.url);
};

var accounts = new Backbone.Collection;
accounts.url = '/accounts';

accounts.fetch(); 
```

**fetch**行为可以通过使用有效的 set 选项进行定制。 例如，要获取一个集合，每一个新的模型会得到一个 `"add"`事件，和每改变现有的模型的 `"change"`事件， 不删除任何东西： `collection.fetch({remove: false})`

**jQuery.ajax**选项也可以直接传递作为 **fetch**选项， 所以要获取一个分页集合的特定页面使用：`Documents.fetch({data: {page: 3}})`。

需要注意的是 **fetch** 不应该被用来在页面加载完毕时填充集合数据 — 所有页面初始数据应当在 bootstrapped 时已经就绪。 **fetch** 适用于惰性加载不需立刻展现的模型数据：例如：例如文档中 可切换打开和关闭的选项卡内容。

**create**`collection.create(attributes, [options])` 方便的在集合中创建一个模型的新实例。 相当于使用属性哈希（键值对象）实例化一个模型， 然后将该模型保存到服务器， 创建成功后将模型添加到集合中。 返回这个新模型。 如果客户端验证失败，该模型将不会被保存， 与验证错误。 为了能正常运行，需要在集合中设置 model 属性。 create 方法接收键值对象或者已经存在尚未保存的模型对象作为参数。

创建一个模型将立即触发集合上的`"add"`事件， 一个`"request"`的事件作为新的模型被发送到服务器， 还有一个 `"sync"` ”事件，一旦服务器响应成功创建模型。 如果你想在集合中添加这个模型前等待服务器相应，请传递`{wait: true}`。

```js
var Library = Backbone.Collection.extend({
  model: Book
});

var nypl = new Library;

var othello = nypl.create({
  title: "Othello",
  author: "William Shakespeare"
}); 
```