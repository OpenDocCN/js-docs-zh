# 过滤

## filter

> 筛选出与指定表达式匹配的元素集合。
> `filter(selector)`
> `filter(function(index){ ... })` 筛选出与 `非` 指定表达式匹配的元素集合。

```js
$("div").filter("#box") //? self 在所有的 div 对象中选择器为 #box 的过滤出来。

$("#select option").filter(function(idx){
    console.log(this.selected)
    return this.selected
})
//上面这种方法跟 not(function(index){ ... })  是一样的 
```

## not

> not(selector) ? collection
> not(collection) ? collection
> not(function(index){ ... }) ? collection
> 筛选出与 `非` 指定表达式匹配的元素集合。它的作用刚好与 `filter` 相反，返回。

```js
$("#select option").not(function(idx){
    console.log(this.selected)
    return this.selected
})
//? [<option value="3">哈哈 3</option>]
$('input').not('#input') //? 返回除去 匹配到的#input

$('input').not(function(){
    console.log(this.type)
    return this.type=='text'
}) 
```

* * *