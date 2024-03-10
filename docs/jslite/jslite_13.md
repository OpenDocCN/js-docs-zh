# 删除节点

## empty

> 所有匹配节点对象集合中移除所有的 dom 子节点，不包括自己，清空内容。

```
$("#box").empty()
//? self <div id="box" class="boxOne box2 box3" ></div> 
```

## remove

> 删除所有匹配节点对象【自己】及所有【自己】里面的内容。

```
$("#box").remove()
//? self <div id="box" class="boxOne box2 box3" ></div> 
```

## detach !

> 被遗弃的方法(不建议使用)，作用跟 remove 一样，所有绑定的事件、附加的数据等都会保留下来。

```
$("#box").click(function(){
    console.log("wcj")
})
var a = $('#box').detach();//删除的对象赋给 a
$('body').append(a)//将 a 添加到 body 中还是可以点击 
```

* * *