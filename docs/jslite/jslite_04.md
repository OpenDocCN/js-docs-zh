# 数组对象操作

## 最大(小)值

```js
//顺带小教程
//获取最大值最小值
var a=[1,2,3,5];
console.log(Math.max.apply(null, a));//最大值
console.log(Math.min.apply(null, a));//最小值

var a=[1,2,3,[5,6],[1,4,8]];
var ta=a.join(",").split(",");//转化为一维数组
console.log(Math.max.apply(null,ta));//最大值
console.log(Math.min.apply(null,ta));//最小值 
```

## Array.remove

> 这个是在 Array 原型对象上扩展的。

```js
[1,5,6].remove(1)//? [5, 6] 
```

## $.intersect

> 数组交集

```js
$.intersect([1,2,3,'asdkjf'],[2,3,6,'asdkjf'])
//? [2, 3, "asdkjf"] 
```

## $.unique

> 删除数组中重复元素。

```js
$.unique([1,2,12,3,2,1,2,1,1,1,1]) //? [1, 2, 12, 3]
var arr = $('#box').concat($('#box')) //两个一模一样的数组
$.unique(arr) //去重 
```

## $.sibling

> 根据类型获取节点对象属性的集合 `(node,type)`。

```js
$.sibling($("input"),"type")    //? ["text", "button", "checkbox"] 
$.sibling($("input"),"tagName") //? ["INPUT"] 
```

## $.inArray

> 搜索数组中指定值并返回它的索引（如果没有找到则返回`-1`)。

```js
var arr = [ 4, "Pete", 8, "John" ];
$.inArray("John", arr);     //? 3
$.inArray(4, arr);          //? 0
$.inArray("David", arr);    //? -1
$.inArray("Pete", arr, 2);  //? -1 
```

## $.map

> 通过遍历集合中的节点对象，通过函数返回一个新的数组，`null` 或 `undefined` 将被过滤掉。

```js
$.map({"w":1,"c":2,"j":3},function(idx,item){
     return item
}); 
//? ["w", "c", "j"] 
```

## $.each

> 通用例遍方法，可用于例遍对象和数组

```js
$.each(['a', 'b', 'c'], function(index, item){
    console.log('item %d is: %s', index, item)
}) 
```

## $.grep

> 使用过滤函数过滤数组元素。

```js
$.grep( [0,1,2], function(n,i){
  return n != 0;
}); 
```

## $.parseJSON

> 与 `JSON.parse` 方法相同，接受一个标准格式的 JSON 字符串，并返回解析后的 JavaScript 对象。

* * *