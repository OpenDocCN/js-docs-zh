# 尺寸位置

## offset

> 获得当前元素相对于 document 的位置。返回一个对象含有：left|top|width|height

```
$("#box").offset()  //?Object {left: 8, top: 8, width: 1260, height: 0}
$("#box").offset().left  //?  8 
```

## width

> width() ? number
> width(value) ? self
> width(function(index, oldWidth){ ... }) ? self
> 获取对象象集合中第一个元素的宽，或设置对象集合所有元素的宽。

```
$('#box').width()   // => 342
$(window).width()   // => 456 (可视区域宽度)
$(document).width() // => dsf 
```

## height

> height() ? number
> height(value) ? self
> height(function(index, oldWidth){ ... }) ? self
> 获取对象象集合中第一个元素的高，或设置对象集合所有元素的高。

```
$('#box').height()   // => 342
$(window).height()   // => 456 (可视区域高度)
$(document).height() // => dsf 
```

## scrollLeft

> scrollLeft() ? self 获取匹配的元素集合中第一个元素的当前水平滚动条的位置

```
$('body').scrollLeft(400); 
```

## scrollTop

> scrollTop() ? self 获取匹配的元素集合中第一个元素的当前垂直滚动条的位置

```
$('body').scrollTop(400); 
```

* * *