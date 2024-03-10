# Effects

# Effects

## $.fx

全局地动画设置：

*   `$.fx.off` (在支持 css transition 的浏览器中默认为 false)：设置 true 来禁止所有`animate()` transitions。

*   `$.fx.speeds`：用来设置动画时间的对象。

    *   `_default` (400 ms)
    *   `fast` (200 ms)
    *   `slow` (600 ms)

改变现有值或者添加一个新属性去影响使用一个字符串来设置时间的动画。

## animate

```
animate(properties, [duration, [easing, [function(){ ... }]]])   => self
      animate(properties, { duration: msec, easing: type, complete: fn })   => self
      animate(animationName, { ... })   => self 
```

对当前对象集合中元素进行 css transition 属性平滑过渡。

*   `properties`: 一个对象，该对象包含了 css 动画的值，或者 css 帧动画的名称。
*   `duration` (默认 400)：以毫秒为单位的时间，或者一个字符串。
    *   `fast` (200 ms)
    *   `slow` (600 ms)
    *   任何`$.fx.speeds`自定义属性
*   `easing` (默认 `linear`)：指定动画的缓动类型，使用以下一个：
    *   `ease`
    *   `linear`
    *   `ease-in` / `ease-out`
    *   `ease-in-out`
    *   [`cubic-bezier(...)`](http://www.w3.org/TR/css3-transitions/#transition-timing-function_tag)
*   `complete`：动画完成时的回调函数

`delay`

Zepto 还支持以下 [CSS transform](http://www.w3.org/TR/css3-transforms/#transform-functions) 属性：

*   `translate(X|Y|Z|3d)`
*   `rotate(X|Y|Z|3d)`
*   `scale(X|Y|Z)`
*   `matrix(3d)`
*   `perspective`
*   `skew(X|Y)`

如果 duration 参数为 `0` 或 `$.fx.off` 为 true(在不支持 css transitions 的浏览器中默认为 true)，动画将不被执行；替代动画效果的目标位置会即刻生效。类似的，如果指定的动画不是通过动画完成，而且动画的目标位置即可生效。这种情况下没有动画， `complete`方法也不会被调用。

如果第一个参数是字符串而不是一个对象，它将被当作一个 css 关键帧动画 [CSS keyframe animation](http://www.w3.org/TR/css3-animations/#animations)的名称。

```
$("#some_element").animate({
        opacity: 0.25,
        left:
        '50px',
        color:
        '#abcdef',
        rotateZ:
        '45deg',
        translate3d: '0,10px,0'
        }, 500,
        'ease-out') 
```

Zepto 只使用 css 过渡效果的动画。jquery 的 easings 不会支持。jquery 的相对变化("=+10px") syntax 也不支持。请查看 [list of animatable properties](http://www.w3.org/TR/css3-transitions/#animatable-properties-)。浏览器的支持可能不同，所以一定要测试你所想要支持的浏览器。