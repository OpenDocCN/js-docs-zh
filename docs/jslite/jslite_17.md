# Ajax

执行 Ajax 请求。请求地址可以是本地的或者跨域的，在支持的浏览器中通过 [HTTP access control](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS)或者通过 [JSONP](http://json-p.org/)来完成。

> 执行 Ajax 请求。
> type：请求方法 ("GET", "POST")
> data：(默认：none)发送到服务器的数据；如果是 get 请求，它会自动被作为参数拼接到 url 上。非 String 对象
> processData (默认： true)： 对于非 Get 请求。是否自动将 data 转换为字符串。
> dataType：(`json`, `jsonp`, `xml`, `html`, or `text`)
> contentType：一个额外的"{键:值}"对映射到请求一起发送
> headers：(默认：{})： 一个额外的"{键:值}"对映射到请求一起发送
> url：发送请求的地址
> async：此参数不传默认为 true(异步请求)，false 同步请求
> success(cdata)：请求成功之后调用。传入返回后的数据，以及包含成功代码的字符串。
> error(status, statusText)：请求出错时调用。 (超时，解析错误，或者状态码不在 HTTP 2xx)。

## $.get

> $.get(url, function(data, status, xhr){ ... }) ? XMLHttpRequest
> $.get(url, [data], [function(data, status, xhr){ ... }], [dataType]) ? XMLHttpRequest

```js
$.get('http://127.0.0.1/api.php?wcj=123', function(cdata) {
    console.log('ok', cdata)
},'json')

$.get('http://127.0.0.1/api.php?wcj=123',{"JSLite":4}, function(cdata) {
    console.log('ok', cdata)
}) 
```

## $.ajax(GET)

1.JSLite 独有....

```js
$.ajax('GET', 'http://127.0.0.1/api.php', {"wcj":"123","ok":'11'},function(cdata) {
    console.log('ok', cdata)
}) 
```

2.通用调用方法

```js
$.ajax({
    type:'GET',
    dataType:'json',
    data:{'nike':'a'},
    url:'http://127.0.0.1/api.php',
    success:function(data){
       console.log('success:',data)
    },
    error:function(d){
       console.log('error:',d)
    }
}) 
```

## $.getJSON

发送一个 Ajax GET 请求并解析返回的 JSON 数据。方法支持跨域请求。
$.getJSON(url, function(data, status, xhr){ ... })

```js
$.getJSON('http://127.0.0.1/api.php', function(data){
  console.log(data)
}) 
```

## jsonp

JSONP 方式

```js
$.ajax({
    url: 'http://127.0.0.1/api.php?callback',
    dataType: 'jsonp',
    success: function(data) {
        console.log(data)
    }
})

$.ajax({
    url: 'http://localhost/api3.php',
    dataType: 'jsonp',
    success: function(data) {
        console.log('success:2:',data)
    },
    error:function(d){
       console.log('error:',d)
    }
}) 
```

## $.post

> $.post(url, [data], function(data, status, xhr){ ... }, [dataType])

```js
$.post('http://127.0.0.1/api.php', {'nike':0},
function(cdata) {
    console.log('ok', cdata)
}) 
```

## $.ajax(POST)

1.JSLite 独有....

```js
var data = { 'key': 'key', 'from': 'from'}
$.ajax('POST', 'http://127.0.0.1/api.php', data,function(data) {
    console.log('ok', data)
},'json') 
```

2.通用调用方法

```js
$.ajax({
    type:'POST',
    dataType:'json',
    data:{"nike":"123","kacper":{"go":34,"to":100}},
    url:'http://127.0.0.1/api.php',
    success:function(data){
       console.log('success:',data)
    },
    error:function(d){
       console.log('error:',d)
    }
})
$.ajax({
    type:'POST',
    dataType:'json',
    data:JSON.stringify('{"nike":"123","kacper":{"go":34,"to":100}}'),
    url:'http://127.0.0.1/api.php',
    success:function(data){
       console.log('success:',data)
    },
    error:function(d){
       console.log('error:',d)
    }
})

$.ajax({
    type:'POST',
    dataType:'json',
    data:JSON.stringify({'nike':'a'}),
    url:'http://127.0.0.1/api.php',
    success:function(data){
       console.log('success:',data)
    },
    error:function(d){
       console.log('error:',d)
    }
})

$.ajax({
    type:'POST',
    data:{'nike':'a'},
    url:'http://127.0.0.1/api.php',
    success:function(data){
       console.log('success:',data)
    },
    error:function(d){
       console.log('error:',d)
    }
})

$.ajax({
    type:'POST',
    dataType:'json',
    data:{'nike':'a'},
    url:'http://127.0.0.1/api.php',
    success:function(data){
       console.log('success:',data)
    },
    error:function(d){
       console.log('error:',d)
    },
    headers: {
        "Access-Control-Allow-Origin":"http://pc175.com",
        "Access-Control-Allow-Headers":"X-Requested-With"
    },
    contentType: 'application/json'
}) 
```

## $.ajaxJSONP

已过时，使用 `$.ajax` 代替。此方法相对 `$.ajax` 没有优势，建议不要使用。 $.ajaxJSONP(options) ? 模拟 XMLHttpRequest

## load

> load() 方法从服务器加载数据，并把返回的数据放入被选元素中。

$(selector).load(URL,data,callback);
必需的 `URL` 参数规定您希望加载的 URL。
可选的 `data` 参数规定与请求一同发送的查询字符串键/值对集合。
可选的 `callback` 参数是 `load()` 方法完成后所执行的函数名称。

这是示例文件（"demo.txt"）的内容：

```js
<h2>JSLite 中 AJAX 的一个方法！</h2>
<p id="demo">这是一个文本文件</p> 
```

```js
// 把文件 "demo.txt" 的内容加载到指定的 <div> 元素中
$("#div1").load("demo.txt");
//把 "demo.txt" 文件中 id="div1" 的元素的内容，加载到指定的 <div> 元素中：
$("#div1").load("demo.txt #p1"); 
```

* * *