# 节点属性

## pluck

> 获取对象集合中每一个元素的属性值。

```
$("#box").pluck("nodeName") //? ["DIV"]
$("#box").pluck("nextElementSibling") //? <div class="boxs">1234567890</div>
$("#box").pluck('children') //? [HTMLCollection[4]] 
```

## attr

> 读取或设置 dom 的属性。

```
$(".button").attr({"class":"","style":"background:red"}) //? self 设置红色清空 class
$(".button").attr("class","name")  //? self 设置 class 替换之前的
$(".button").attr("class")  //? string 获取 class 属性值 
```

## removeAttr

> 移动当前对象集合中所有元素的指定属性。

```
$("#box").removeAttr("class") //? self 移除 class 
```

## prop

> 读取或设置 dom 的属性。它在读取属性值的情况下优先于 attr，因为这些属性值会因为用户的交互发生改变，如 `checked` 和 `selected` 。

```
<input class="taiyang" id="check1" type="checkbox" checked="checked">
<input class="yaotaiyang" id="check2" type="checkbox">
<script type="text/javascript"> $("#check1").attr("checked"); //=> "checked"
    $("#check1").prop("checked"); //=> "true"
    $("#check2").attr("checked"); //=> "false"
    $("#check2").prop("checked"); //=> "false"
    $("input[type='checkbox']").prop("type",function(index,oldvalue){
        console.log(index+"|"+oldvalue);
    });
    //=> 0|checkbox
    //=> 1|checkbox
    $("input[type='checkbox']").prop("className",function(index,oldvalue){
        console.log(index+"|"+oldvalue);
    });
    //=> 0|taiyang
    //=> 1|yaotaiyang </script> 
```

## removeProp

> 为集合中匹配的元素删除一个属性（property）。`removeProp()` 方法用来删除由`.prop()`方法设置的属性集。

**注意**: 不要使用此方法来删除原生的属性（ property ），比如 checked, disabled, 或者 selected。这将完全移除该属性，一旦移除，不能再次被添加到元素上。使用.prop()来设置这些属性设置为 false 代替。

```
<p id="n2" class="demo test" data-key="UUID" data_value="1235456465">CodePlayer</p>
<script> var $n2 = $("#n2");
$n2.prop("prop_a", "CodePlayer");
$n2.prop("prop_b", { name: "CodePlayer", age: 20 } );

console.log($n2.prop("prop_a")) //? CodePlayer
console.log($n2.prop("prop_b")) //? Object {name: "CodePlayer", age: 20}

$n2.removeProp("data-key");
$n2.prop("data-key") //? undefined
$n2.attr("data-key") //? "UUID" </script> 
```

* * *