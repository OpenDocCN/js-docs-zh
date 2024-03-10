# CSS 类

## css

> 获取或设置节点对象的 style 样式内容。

```
$("#box").css('color','yellow')     //? self 返回 Array 节点内容
$("#box").css({'color':'yellow'})   //? self 返回 Array 节点内容 
```

## hasClass

> 集合中是否有节点对象含有指定的 class。

```
$("#box").hasClass('box2') //? true 
```

## addClass

> 为每个匹配的节点对象添加指定的 class 类名。

```
$("#box").addClass('box23 go') //? self 原有对象 class 上添加 box23 和 go

$("#box").addClass(function(){
    return 'box23 wcj'
}) //? self 原有对象 class 上添加 box23 和 wcj 
```

## removeClass

> 清除节点对象中所有节点对象的指定 class 类名，不填写清空。

```
$("#box").removeClass('box23') //? self 删除原有对象 class 中 box23
$("div").removeClass() //? self  所有匹配的对象 class 属性被删除 
```

## toggleClass

> 在匹配的节点对象集合中的每个节点对象上添加或删除一个或多个样式类。

```
$("#box").toggleClass('box1 box2') //? self 原有对象 class 上添加 "box1 box2"或者删除"box1 box2" 
```

* * *