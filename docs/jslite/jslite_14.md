# 查找节点

## find

> 后代节点的集合(可以带上滤选择器)。

```
$("#box").find()        //?后代节点的集合
$("#box").find(".box")  //?后代节点的集合，返回匹配'.box' 的集合 
```

## children

> 获得每个匹配元素集合元素的直接子元素(可以带上滤选择器)。

```
$("#box").children()
//下面这种方法也可以的 CSS3 节点选择器 -_+
$("#box *") 
```

## contents

> 获得每个匹配元素集合元素的子元素，包括文字和注释节点。 `contents() ? collection`

```
$("#box").contents() 
```

## parent

> 对象集合中每个元素的直接父元素。

```
$("#box").parent() 
```

## parents

> 获取对象集合每个元素所有的祖先元素（不包含根元素）。
> `parents([selector]) ? collection`

```
$("#box").parents()

$("#boxWhy").parents(".boxss") 
```

## closest

> 从元素本身开始，逐级向上级元素匹配，并返回最先匹配`selector`的祖先元素。如果`context`节点参数存在。那么直考虑该节点的后代。这个方法与 `parents(selector)`有点相像，但他只返回最先匹配的祖先元素。

```
$("#box").closest('div')

$(document).bind("click", function(e) {
    console.log(e.target)//当前点击的对象
    $(e.target).closest("li").css('background','red');
});

$("#boxWhy").closest('.boxss',$('#box')[0])//#boxWhy 节点的父节点为："$('#box')[0]"的子节点".boxss" 
```

## prev

> 获取对象集合每个元素的所有上一个对象(可以带上滤选择器)。

```
$("#box").prev("div") 
```

## next

> 获取对象集合每个元素的所有下一个对象(可以带上滤选择器)。

```
$("#box").next("div") 
```

## prevAll

> 获取对此对象【上】所有兄弟对象(可以带上滤选择器)。

```
$("#box").prevAll("div") 
```

## nextAll

> 获取对此对象【下】所有兄弟对象(可以带上滤选择器)。

```
$("#box").nextAll("div") 
```

## siblings

> 获取对此对象【其它】所有兄弟对象(可以带上滤选择器)。

```
$("#box").siblings() 
```

## slice

> array 中提取的方法。从 start 开始，如果 end 指出。提取不包含 end 位置的元素。 `slice(start, [end]) ? array`

```
$("div").slice(3) //返回数组中第三个(包含第三个)之后的所有元素
$("div").slice(3,5) //返回数组 3-5 之间的元素 
```

## add

> 添加元素到匹配的`JSLite`对象集合

```
$("#box").siblings() 
```

* * *