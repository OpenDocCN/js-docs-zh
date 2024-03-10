# 表单方法

# 表单方法

## serialize

```
serialize()   => string 
```

在 Ajax post 请求中将用作提交的表单元素的值编译成 URL 编码的 字符串。

## serializeArray

```
serializeArray()   => array 
```

将用作提交的表单元素的值编译成拥有`name`和`value`对象组成的数组。不能使用的表单元素，buttons，未选中的 radio buttons/checkboxs 将会被跳过。结果不包含 file inputs 的数据。

```
$('form').serializeArray()
//=> [{ name: 'size', value: 'micro' },
//    { name: 'name', value: 'Zepto' }] 
```

## submit

```
submit()   => self
submit(function(e){ ... })   => self 
```

为 "submit" 事件绑定一个处理函数，或者触发元素上的 "submit" 事件。当没有给定 function 参数时，触发当前表单“submit”事件，并且执行默认的提交表单行为，除非调用了 `preventDefault()`。

当给定 function 参数时，在当前元素上它简单得为其在“submit”事件绑定一个处理函数。