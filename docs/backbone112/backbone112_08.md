# Backbone.sync（同步）

## Backbone.sync（同步）

**Backbone.sync** 是 Backbone 每次向服务器读取或保存模型时都要调用执行的函数。 默认情况下，它使用 `jQuery.ajax` 方法发送 RESTful json 请求，并且返回一个 [jqXHR](http://www.css88.com/jqapi-1.9/jQuery.ajax/#jqXHR)。 如果想采用不同的持久化方案，比如 WebSockets, XML, 或 Local Storage，我们可以重载该函数。

**Backbone.sync** 的语法为 `sync(method, model, [options])`。

*   **method** – CRUD 方法 (`"create"`, `"read"`, `"update"`, or `"delete"`)
*   **model** – 要被保存的模型（或要被读取的集合）
*   **options** – 成功和失败的回调函数，以及所有 jQuery 请求支持的选项

默认情况下，当 **Backbone.sync** 发送请求以保存模型时，其属性会被序列化为 JSON，并以 `application/json` 的内容类型发送。 当接收到来自服务器的 JSON 响应后，对经过服务器改变的模型进行拆解，然后在客户端更新。 当 `"read"` 请求从服务器端响应一个集合（Collection#fetch）时，便拆解模型属性对象的数组。

当一个模型或集合开始 **sync**到服务器时，将触发一个 `"request"` 事件。 如果请求成功完成，你会得到一个`"sync"`事件， 如果请求失败，你会得到一个 `"error"`事件。

**sync**函数可重写为全局性的`Backbone.sync`， 或在细粒度级别， 通过添加一个 `sync`函数 到 Backbone 集合或单个模型时。

默认 **sync** 映射 REST 风格的 CRUD 类似下面这样：

*   **create → POST** `/collection`
*   **read → GET** `/collection[/id]`
*   **update → PUT** `/collection/id`
*   **patch → PATCH** `/collection/id`
*   **delete → DELETE** `/collection/id`

举个例子，一个 Rail 4 处理程序响应一个来自`Backbone`的`"update"`调用，可能是这样的： *（在真正的代码中， 千万不要盲目的使用`update_attributes`， ，你可以被改变的属性始终是白名单。）*

```js
def update
  account = Account.find params[:id]
  account.update_attributes params.require(:account).permit(:name, :otherparam)
  render :json => account
end 
```

一个技巧： 通过设置`ActiveRecord::Base.include_root_in_json = false`，在模型上禁用默认命名空间的`to_json`来整合 Rails 3.1 之前的版本， 。

**ajax**`Backbone.ajax = function(request) { ... };` 如果你想使用自定义的 AJAX 功能， 或者你的客户端不支持的[jQuery.ajax](http://www.css88.com/jqapi-1.9/jQuery.ajax/) API，你需要调整的东西， 您可以通过设置`Backbone.ajax`这样做。

**emulateHTTP**`Backbone.emulateHTTP = true` 如果你想在不支持 Backbone 的默认 REST/ HTTP 方式的 Web 服务器上工作， 您可以选择开启`Backbone.emulateHTTP`。 设置该选项将通过 `POST` 方法伪造 `PUT`，`PATCH` 和 `DELETE` 请求 用真实的方法设定`X-HTTP-Method-Override`头信息。 如果支持`emulateJSON`，此时该请求会向服务器传入名为 `_method` 的参数。

```js
Backbone.emulateHTTP = true;

model.save();  // POST to "/collection/id", with "_method=PUT" + header. 
```

**emulateJSON**`Backbone.emulateJSON = true` 如果你想在不支持发送 `application/json` 编码请求的 Web 服务器上工作，设置`Backbone.emulateJSON = true;`将导致 JSON 根据模型参数进行序列化， 并通过`application/x-www-form-urlencoded` MIME 类型来发送一个伪造 HTML 表单请求，