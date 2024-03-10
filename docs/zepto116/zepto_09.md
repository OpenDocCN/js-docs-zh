# Ajax 请求

## $.ajax

```
$.ajax(options)   => XMLHttpRequest 
```

执行 Ajax 请求。它可以是本地资源，或者通过支持[HTTP access control](https://developer.mozilla.org/en/http_access_control)的浏览器 或者通过 [JSONP](http://json-p.org)来实现跨域。

选项:

*   `type`(默认： “GET”)：请求方法 (“GET”, “POST”, or other)
*   `url` (默认： 当前地址)：发送请求的地址
*   `data` (默认：none)：发送到服务器的数据；如果是 GET 请求，它会自动被作为参数拼接到 url 上。非 String 对象将通过 $.param 得到序列化字符串。
*   `processData` (默认： true)： 对于非 Get 请求。是否自动将 `data` 转换为字符串。
*   `contentType` (默认： “application/x-www-form-urlencoded”)： 发送信息至服务器时内容编码类型。 (这也可以通过设置 `headers`)。通过设置 `false` 跳过设置默认值。
*   `mimeType` (默认： none): 覆盖响应的 MIME 类型。 v1.1+
*   `dataType` (默认： none)：预期服务器返回的数据类型(“json”, “jsonp”, “xml”, “html”, or “text”)
*   `jsonp` (默认：“callback”): JSONP 回调查询参数的名称
*   `jsonpCallback` (默认： “jsonp{N}”): 全局 JSONP 回调函数的 字符串（或返回的一个函数）名。设置该项能启用浏览器的缓存。 v1.1+
*   `timeout` (默认： `0`): 以毫秒为单位的请求超时时间, `0` 表示不超时。
*   `headers`: Ajax 请求中额外的 HTTP 信息头对象
*   `async` (默认：true): 默认设置下，所有请求均为异步。如果需发送同步请求，请将此设置为 `false`。
*   `global` (默认：true): 请求将触发全局 Ajax 事件处理程序，设置为 false 将不会触发全局 Ajax 事件。
*   `context` (默认：window): 这个对象用于设置 Ajax 相关回调函数的上下文(this 指向)。
*   `traditional` (默认： false): 激活传统的方式通过$.param 来得到序列化的 `data`。
*   `cache` (默认： true): 浏览器是否应该被允许缓存 GET 响应。从 v1.1.4 开始，当 dataType 选项为 `"script"` 或 `jsonp`时，默认为`false`。
*   `xhrFields` (默认： none): 一个对象包含的属性被逐字复制到 XMLHttpRequest 的实例。 v1.1+
*   `username` & `password` (默认： none): HTTP 基本身份验证凭据。 v1.1+

如果 URL 中含有 `=?`或者`dataType`是“jsonp”，这讲求将会通过注入一个 `&lt;script&gt;`标签来代替使用 XMLHttpRequest (查看 [JSONP](http://json-p.org))。此时 `contentType`, `dataType`, `headers`有限制，`async` 不被支持。

### Ajax 回调函数

你可以指定以下的回调函数，他们将按给定的顺序执行：

1.  `beforeSend(xhr, settings)`：请求发出前调用，它接收 xhr 对象和 settings 作为参数对象。如果它返回 `false` ，请求将被取消。

2.  `success(data, status, xhr)`：请求成功之后调用。传入返回后的数据，以及包含成功代码的字符串。

3.  `error(xhr, errorType, error)`：请求出错时调用。 (超时，解析错误，或者状态码不在 HTTP 2xx)。

4.  `complete(xhr, status)`：请求完成时调用，无论请求失败或成功。

### Promise 回调接口 v1.1+

如果可选的“callbacks” 和 “deferred” 模块被加载，从`$.ajax()`返回的 XHR 对象实现了 promise 接口链式的回调：

```
xhr.done(function(data, status, xhr){ ... })
xhr.fail(function(xhr, errorType, error){ ... })
xhr.always(function(){ ... })
xhr.then(function(){ ... }) 
```

这些方法取代了 `success`, `error`, 和 `complete` 回调选项.

### Ajax 事件

当`global: true`时。在 Ajax 请求生命周期内，以下这些事件将被触发。

1.  `ajaxStart` *(global)*：如果没有其他 Ajax 请求当前活跃将会被触发。

2.  `ajaxBeforeSend` (data: xhr, options)：再发送请求前，可以被取消。

3.  `ajaxSend` (data: xhr, options)：像 `ajaxBeforeSend`，但不能取消。

4.  `ajaxSuccess` (data: xhr, options, data)：当返回成功时。

5.  `ajaxError` (data: xhr, options, error)：当有错误时。

6.  `ajaxComplete` (data: xhr, options)：请求已经完成后，无论请求是成功或者失败。

7.  `ajaxStop` *(global)*：如果这是最后一个活跃着的 Ajax 请求，将会被触发。

默认情况下，Ajax 事件在 document 对象上触发。然而，如果请求的 `context` 是一个 DOM 节点，该事件会在此节点上触发然后再 DOM 中冒泡。唯一的例外是 `ajaxStart` & `ajaxStop`这两个全局事件。

```
$(document).on('ajaxBeforeSend', function(e, xhr, options){
  // This gets fired for every Ajax request performed on the page.
  // The xhr object and $.ajax() options are available for editing.
  // Return false to cancel this request.
})

$.ajax({
  type: 'GET',
  url: '/projects',
  // data to be added to query string:
  data: { name: 'Zepto.js' },
  // type of data we are expecting in return:
  dataType: 'json',
  timeout: 300,
  context: $('body'),
  success: function(data){
    // Supposing this JSON payload was received:
    //   {"project": {"id": 42, "html": "<div>..." }}
    // append the HTML to context object.
    this.append(data.project.html)
  },
  error: function(xhr, type){
    alert('Ajax error!')
  }
})

// post a JSON payload:
$.ajax({
  type: 'POST',
  url: '/projects',
  // post payload:
  data: JSON.stringify({ name: 'Zepto.js' }),
  contentType: 'application/json'
}) 
```

## $.ajaxJSONP

不推荐, 使用 $.ajax 代替。

```
$.ajaxJSONP(options)   => mock XMLHttpRequest 
```

执行 JSONP 跨域获取数据。

此方法相对 $.ajax 没有优势，建议不要使用。

## $.ajaxSettings

一个包含 Ajax 请求的默认设置的对象。大部分的设置在 $.ajax 中已经描述。以下设置为全局非常有用：

*   `timeout` (默认： `0`)：对 Ajax 请求设置一个非零的值指定一个默认的超时时间，以毫秒为单位。
*   `global` (默认： true)：设置为 false。以防止触发 Ajax 事件。
*   `xhr` (默认：XMLHttpRequest factory)：设置为一个函数，它返回 XMLHttpRequest 实例(或一个兼容的对象)
*   `accepts`: 从服务器请求的 MIME 类型，指定`dataType`值：
    *   script: “text/javascript, application/javascript”
    *   json: “application/json”
    *   xml: “application/xml, text/xml”
    *   html: “text/html”
    *   text: “text/plain”

## $.get

```
$.get(url, function(data, status, xhr){ ... })   => XMLHttpRequest
$.get(url, [data], [function(data, status, xhr){ ... }], [dataType])   => XMLHttpRequest v1.0+ 
```

执行一个 Ajax GET 请求。这是一个 $.ajax 的简写方式。

```
$.get('/whatevs.html', function(response){
  $(document.body).append(response)
}) 
```

## $.getJSON

```
$.getJSON(url, function(data, status, xhr){ ... })   => XMLHttpRequest
$.getJSON(url, [data], function(data, status, xhr){ ... })   => XMLHttpRequest v1.0+ 
```

通过 Ajax GET 请求获取 JSON 数据。这是一个 $.ajax 的简写方式。

```
$.getJSON('/awesome.json', function(data){
  console.log(data)
})

// fetch data from another domain with JSONP
$.getJSON('//example.com/awesome.json?callback=?', function(remoteData){
  console.log(remoteData)
}) 
```

## $.param

```
$.param(object, [shallow])   => string
$.param(array)   => string 
```

序列化一个对象，在 Ajax 请求中提交的数据使用 URL 编码的查询字符串表示形式。如果 shallow 设置为 true。嵌套对象不会被序列化，嵌套数组的值不会使用放括号在他们的 key 上。

如果任何对象的某个属性值是一个函数，而不是一个字符串，该函数将被调用并且返回值后才会被序列化。

此外，还接受 serializeArray 格式的数组，其中每个项都有 “name” 和 “value”属性。

```
$.param({ foo: { one: 1, two: 2 }})
//=> "foo[one]=1&foo[two]=2)"

$.param({ ids: [1,2,3] })
//=> "ids[]=1&ids[]=2&ids[]=3"

$.param({ ids: [1,2,3] }, true)
//=> "ids=1&ids=2&ids=3"

$.param({ foo: 'bar', nested: { will: 'not be ignored' }})
//=> "foo=bar&nested[will]=not+be+ignored"

$.param({ foo: 'bar', nested: { will: 'be ignored' }}, true)
//=> "foo=bar&nested=[object+Object]"

$.param({ id: function(){ return 1 + 2 } })
//=> "id=3" 
```

## $.post

```
$.post(url, [data], function(data, status, xhr){ ... }, [dataType])   => XMLHttpRequest 
```

执行 Ajax POST 请求。这是一个 $.ajax 的简写方式。

```
$.post('/create', { sample: 'payload' }, function(response){
  // process response
}) 
```

`data` 参数可以是一个字符串：

```
$.post('/create', $('#some_form').serialize(), function(response){
  // ...
}) 
```

## load

```
load(url, function(data, status, xhr){ ... })   => self 
```

通过 GET Ajax 载入远程 HTML 内容代码并插入至 当前的集合 中。另外，一个 css 选择器可以在 url 中指定，像这样，可以使用匹配 selector 选择器的 HTML 内容来更新集合。

```
$('#some_element').load('/foo.html #bar') 
```

如果没有给定 CSS 选择器，将使用完整的返回文本。

请注意，在没有选择器的情况下，任何 javascript 块都会执行。如果带上选择器，匹配选择器内的 script 将会被删除。