# 对象访问

## each

> 遍历一个 `JSLite` 集合对象，为每一个匹配元素执行一个函数。this 关键字指向当前 item(作为函数的第二个参数传递)。如果函数返回 false，遍历结束。

```
$("img").each(function(i){
    this.src = "test" + i + ".jpg";
});
//? 找到所有的 img 对象给设置 src 
//? 返回 [ <img src="test0.jpg" />, <img src="test1.jpg" /> ] 
```

## map

> 遍历节点对象集合中的所有节点对象返回一个新的集合对象

```
$(".box").map(function(index,item){
    return $(this).text()
})
//? 返回 ["12boxOne", "6", "11", "22123456", "7123123"] 
```

## forEach

> 类似 each，forEach 遍历不会停止。

```
//遍历数组
[1,5,2,3].forEach(function(item,index,array){
    console.log(item,index,array)
})
//遍历节点
$("img").forEach(function(item,index,array){
    console.log(item,index,array)
}) 
```

## eq

> 指定匹配元素的集合为的索引的哪一个元素。一个整数，指示元素的位置，以 `0` 为基数。 eq(index) ? collection eq(-index) ? collection

```
$("div").eq(0)//? 返回数组第一个节点数组 [div#box.boxOne.box2.box3, init: function…]
$("div").eq(-1)//? 倒数第一个节点数组
$("div").eq(-2)//? 倒数第二个节点数组 
```

## first

> 获取当前对象集合中的第一个元素。 first() ? collection

```
$('form').first() 
```

## get

> 当前对象集合中获取所有节点对象或单个节点对象。

```
$("div").get(0)//? 返回节点 <div id="box" class="boxOne box2 box3" ></div> 
```

## index

> 获取一个元素的位置。当 elemen 参数没有给出时，返回当前元素在兄弟节点中的位置。 .index() //对象中第一个元素相对于它同辈元素的位置 .index(selector)
> .index(element)

```
$("#box").index()//? 4
$("div").index("#box")//? 2
$("div").index($("#box"))//? 2
$("div").index($("#box")[0])//? 2 
```

## indexOf

> 在当前获取的节点数组中获取一个元素在这个数组的位置。

```
$("div").indexOf($("#box")[0])
//? 2 
```

## length

> 对象中元素的个数。

```
$("img").length;
//? 2 
```

* * *