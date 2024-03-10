# Touch

# Touch

## Touch events

“touch”模块添加以下事件，可以使用 on 和 off。

*   `tap` —元素 tap 的时候触发。
*   `singleTap` and `doubleTap` — 这一对事件可以用来检测元素上的单击和双击。(如果你不需要检测单击、双击，使用 `tap` 代替)。
*   `longTap` — 当一个元素被按住超过 750ms 触发。
*   `swipe`, `swipeLeft`, `swipeRight`, `swipeUp`, `swipeDown` — 当元素被划过时触发。(可选择给定的方向)

这些事件也是所有 Zepto 对象集合上的快捷方法。

```
<style>.delete { display: none; }</style>

<ul id=items>
  <li>List item 1 <span class=delete>DELETE</span></li>
  <li>List item 2 <span class=delete>DELETE</span></li>
</ul>

<script>
// show delete buttons on swipe
$('#items li').swipe(function(){
  $('.delete').hide()
  $('.delete', this).show()
})

// delete row on tapping delete button
$('.delete').tap(function(){
  $(this).parent('li').remove()
})
</script> 
```