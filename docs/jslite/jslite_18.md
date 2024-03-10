# Form

> 表单提交的一些方法

## submit

> submit() 方法把表单数据提交到 Web 服务器。这个是原生态提供的方法，还没有封装更改 *。

```js
$('form')[0].submit() //此处直接原生态提交表单，日后封装，直接在 JSLite 对象上就可以提交。 
```

## serializeArray

> 将用作提交的表单元素的值组合成拥有 name 和 value 的键值对组成的数组。不能使用的表单元素，buttons，未选中的 radio buttons/checkboxs 将会被跳过。结果不包含 file inputs 的数据。

```js
$('form').serializeArray();
//=> [{"name":"golang","value":"456"},{"name":"name","value":""},{"name":"password","value":""},{"name":"sel","value":[]},{"name":"kaikai","value":""},{"name":"w","value":""},{"name":"w","value":""}] 
```

## serialize

> 将表单元素数组或者对象序列化。

```js
$('form').serialize();
//=> golang=456&name=&password=&sel=&kaikai=&w=asd&w2=asdf 
```