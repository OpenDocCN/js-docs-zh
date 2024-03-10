# Selectors

# Selectors

## :data() Selector

选择数据已存储在指定的键下的元素。

Also in: [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## :focusable Selector

选择可被聚焦的元素。

Also in: [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## :tabbable Selector

选择用户可通过 tab 键聚焦的元素。

# :data() Selector

# :data() Selector

Categories: [Selectors](http://www.css88.com/jquery-ui-api/category/selectors/ "View all posts in Selectors") | [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

**Description:** 选择数据已存储在指定的键下的元素。

*   #### jQuery( ":data(key)" )

    **key:** 数据的键。

表达式 `$( "div:data(foo)")` 匹配一个通过 `.data( "foo", value )` 存储数据的 `&lt;div&gt;`。

## Example:

#### 选择带有数据的元素，改变它们的背景颜色。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>data demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <style>
  div {
    width: 100px;
    height: 100px;
    border: 1px solid #000;
    float: left;
  }
  </style>
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<div id="one"></div>
<div id="two"></div>
<div id="three"></div>

<script>
$( "#one" ).data( "color", "blue" );
$( "#three" ).data( "color", "green" );

$( ":data(color)" ).each(function() {
  var element = $( this );
  element.css( "backgroundColor", element.data( "color" ) );
});
</script>

</body>
</html> 
```

# :focusable Selector

# :focusable Selector

Categories: [Selectors](http://www.css88.com/jquery-ui-api/category/selectors/ "View all posts in Selectors") | [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

**Description:** 选择可被聚焦的元素。

*   #### jQuery( ":focusable" )

一些元素本身是可聚焦的（focusable），而另一些元素需要显式设置 tab 索引。以上两种情况，为了可聚焦（focusable），元素都必须是可见的。

下面类型的元素如果未被禁用，则是可聚焦的（focusable）：`input`、`select`、`textarea`、`button` 和 `object`。锚如果带有 `href` 或 `tabindex` 属性，则是可聚焦的（focusable）。`area` 元素如果在一个已命名的 map 内，且带有 `href` 属性，且有一个可见的图像使用了该 map，则是可聚焦的（focusable）。所有其他完全基于 `tabindex` 属性和可见度的元素是可聚焦的（focusable）。

注释：带有负的 tab 索引的元素是 `:focusable`，不是 `:tabbable`。

## Example:

#### 选择可聚焦的元素，且用一个红色边框突出显示。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>focusable demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <style>
  input, a, p {
    border: 1px solid #000;
  }
  div {
    padding: 5px;
  }
  </style>
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<div><input value="text input"></div>
<div><a>anchor without href</a></div>
<div><a href="#">anchor with href</a></div>
<div><p>paragraph without tabindex</p></div>
<div><p tabindex="1">paragraph with tabindex</p></div>

<script>
$( ":focusable" ).css( "border-color", "red" );
</script>

</body>
</html> 
```

# :tabbable Selector

# :tabbable Selector

Categories: [Selectors](http://www.css88.com/jquery-ui-api/category/selectors/ "View all posts in Selectors") | [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

**Description:** 选择用户可通过 tab 键聚焦的元素。

*   #### jQuery( ":tabbable" )

一些元素本身是可通过 tab 键聚焦的（tabbable），而另一些元素需要显式设置一个正的 tab 索引。以上两种情况，为了可通过 tab 键聚焦（tabbable），元素都必须是可见的。

下面类型的元素如果不带有负的 tab 索引且未被禁用，则是可通过 tab 键聚焦的（tabbable）：`input`、`select`、`textarea`、`button` 和 `object`。锚如果带有 `href` 或正的 `tabindex` 属性，则是可通过 tab 键聚焦的（tabbable）。`area` 元素如果在一个已命名的 map 内，且带有 `href` 属性，且有一个可见的图像使用了该 map，则是可通过 tab 键聚焦的（tabbable）。所有其他完全基于 `tabindex` 属性和可见度的元素是可通过 tab 键聚焦的（tabbable）。

注释：带有负的 tab 索引的元素是 `:focusable`，不是 `:tabbable`。

## Example:

#### 选择可通过 tab 键聚焦的元素，且用一个红色边框突出显示。

```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>tabbable demo</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.10.4/themes/smoothness/jquery-ui.css">
  <style>
  input {
    border: 1px solid #000;
  }
  div {
    padding: 5px;
  }
  </style>
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.10.4/jquery-ui.js"></script>
</head>
<body>

<div><input value="no tabindex"></div>
<div><input tabindex="5" value="positive tabindex"></div>
<div><input tabindex="-1" value="negative tabindex"></div>

<script>
$( ":tabbable" ).css( "border-color", "red" );
</script>

</body>
</html> 
```