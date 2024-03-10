# URL

## $.getUrlParam

> 获取 `url` 参数的值。

```
//[URL] = http://blog.pc175.com/?param=2
$.getUrlParam("param") //? 2 
```

## $.param

> 将表单元素数组或者对象序列化。如果 shallow 设置为 true，嵌套对象不会被序列化，嵌套数组的值不会使用放括号在他们的 key 上。
> `$.param(object, [shallow]) ? string`
> `$.param(array) ? string`

```
$.param({
    foo: {one: 1,two: 2 }
})  //? "foo[one]=1&foo[two]=2"

$.param({
    ids:["a1","b2","c3"],
    c:{g:23,e:[567]},
    a:3
},true) //? ids=a1&&ids=b2&&ids=c3&&c=[object Object]&a=3

$.param({
    ids:["a1","b2","c3"],
    c:{g:23,e:[567]},
    a:3
}) //? ids[]=a1&&ids[]=b2&&ids[]=c3&&c[g]=23&&c[e]=567&&a=3

$.param([1,2,3]) //? 0=1&&1=2&&2=3

$.param({
    ids:[1,2,3] 
})  //=> "ids[]=1&ids[]=2&ids[]=3" 
```

* * *