# HTML 代码/文本/值

## text

> 取得所有匹配节点对象的文本内容。

```js
$("#box").text() //? string 返回文本
$("#box").text(function(){
    return "这里干点儿什么？"
}) //? string 返回"#box"中的文本 
```

## html

> 获取或设置节点对象内容。

```js
$("#box").html()
//? string 返回包括 HTML 的文本 
```

## val

> 获取设置 input 的 value 。

```js
$('input').val() //? string 
$('input').val('test') //? self 

$('#input').val(function(index,oldvalue){
    console.log(index,oldvalue)
    return '111' + oldvalue
}) //? self 
```

## data

> 读取或写入 dom 的 data-* 属性。 data(name) ? value data(name, value) ? self

```js
$('#test').eq(0).data('name',{"sss":1}) //? self
$('#test').eq(0).data('name',[1,2,3,4]) //? self 
$('#test').eq(0).data('name') //? [1,2,3,4]  或者 {"sss":1} 对象
$('#test').data({"aa":1,"www":334343}) //? 设置节点属性 data-aa="1" | data-www="334343"
$('#test').data() //?  {"aa":1,"www":334343} 
```

* * *