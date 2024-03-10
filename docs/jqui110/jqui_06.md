# Methods

虽然 jQuery UI 主要包含的是 widgets, interactions, h 和 effects, 也添加了几个简单方便的方法。

Also in: [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .disableSelection()

禁用选择匹配的元素集合内的文本内容。

Also in: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core")

## .effect()

对一个元素应用动画特效。

Also in: [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .enableSelection()

启用选择匹配的元素集合内的文本内容。

Also in: [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides") | [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .focus()

异步聚焦到一个元素。

Also in: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides")

## .hide()

使用自定义效果来隐藏匹配的元素。

Also in: [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides") | [Utilities](http://www.css88.com/jquery-ui-api/category/utilities/ "View all posts in Utilities")

## .position()

相对另一个元素定位一个元素。

Also in: [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .removeUniqueId()

为匹配的元素集合移除由 .uniqueId() 设置的 Id。

Also in: [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .scrollParent()

获取最近的可滚动的祖先。

Also in: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides")

## .show()

使用自定义效果来显示匹配的元素。

Also in: [Effects](http://www.css88.com/jquery-ui-api/category/effects/ "View all posts in Effects") | [Effects Core](http://www.css88.com/jquery-ui-api/category/effects-core/ "View all posts in Effects Core") | [Method Overrides](http://www.css88.com/jquery-ui-api/category/overrides/ "View all posts in Method Overrides")

## .toggle()

使用自定义效果来显示或隐藏匹配的元素。

Also in: [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .uniqueId()

为匹配的元素集合生成并申请一个唯一的 Id。

Also in: [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .zIndex()

为元素获取 z-index。

# .disableSelection()

Categories: [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods") | [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .disableSelection()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 禁用选择匹配的元素集合内的文本内容。

*   #### version added: 1.6, deprecated: 1.9.disableSelection()

    *   该方法不接受任何参数。

禁用的文本选择是有害的，不建议使用。

# .enableSelection()

Categories: [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods") | [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .enableSelection()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 启用选择匹配的元素集合内的文本内容。

*   #### version added: 1.6, deprecated: 1.9.enableSelection()

    *   该方法不接受任何参数。

`.enableSelection()` 方法可用于启用通过 `.disableSelection()` 禁用的文本选择。

# .removeUniqueId()

Categories: [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods") | [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .removeUniqueId()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 为匹配的元素集合移除由 `.uniqueId()` 设置的 Id。

*   #### version added: 1.9.removeUniqueId()

    *   该方法不接受任何参数。

`.removeUniqueId()`移除由 `.uniqueId()` 设置的 id。在未使用 `.uniqueId()` 设置 id 的元素上调用 `.removeUniqueId()`则无影响，即使该元素有一个 id。

# .scrollParent()

Categories: [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods") | [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .scrollParent()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 获取最近的可滚动的祖先。

*   #### .scrollParent()

    *   该方法不接受任何参数。

该方法查找最近的可滚动的祖先。换句话说，`.scrollParent()` 查找当前所选元素在其内滚动的元素。

*注意: 该方法只在包含一个元素的 jQuery 对象上工作。*

# .uniqueId()

Categories: [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods") | [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

## .uniqueId()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 为匹配的元素集合生成并申请一个唯一的 Id。

*   #### version added: 1.9.uniqueId()

    *   该方法不接受任何参数。

许多小部件需要元素生成唯一的 id。`.uniqueId()` 会检查元素是否有 id，如果元素没有 id，它将生成一个 id，并设置为该元素的 id。在未检查元素是否具有 id 就调用 `.uniqueId()` 是安全的。当小部件使用后需要清除，如果 id 是通过 `.uniqueId()` 添加的，`.removeUniqueId()` 方法将从元素上移除 id，如果 id 不是通过 .uniqueId() 添加的，则无影响。`.removeUniqueId()` 之所以能区分 id，是因为 `.uniqueId()` 生成的 id 带有前缀 "ui-id-"。

# .zIndex()

Categories: [Methods](http://www.css88.com/jquery-ui-api/category/methods/ "View all posts in Methods") | [UI Core](http://www.css88.com/jquery-ui-api/category/ui-core/ "View all posts in UI Core")

*   .zIndex()
    *   .zIndex()
*   .zIndex( zIndex )
    *   .zIndex( zIndex )

## .zIndex()Returns: [jQuery](http://api.jquery.com/Types/#jQuery)

**Description:** 为元素获取 z-index。

*   #### .zIndex()

    *   该方法不接受任何参数。

`.zIndex()` 方法在查找一个元素的 z-index 时非常有用，忽略 z-index 是否是直接设置在元素上还是设置在祖先元素上。为了确定 z-index，该方法会在指定的元素上开始，且会沿着 DOM 查找，直到找到一个带有 z-index 的已定位的元素。如果未找到这样的元素，该方法将返回一个 `0` 值。

该方法假设带有嵌套 z-index 的元素不带有一个 `0` 值的 z-index。例如，给出下面的 DOM，内部元素将被当成不带有 z-index，因为在 Internet Explorer 中无法区分一个 `0` 显式值和无值。

```
<div style="z-index: -10;">
  <div style="z-index: 0;"></div>
</div> 
```

## .zIndex( zIndex )Returns: [Integer](http://api.jquery.com/Types/#Integer)

**Description:** 为元素设置 z-index。

*   #### .zIndex( zIndex )

    *   **zIndex**Type: [Integer](http://api.jquery.com/Types/#Integer)要设置的 z-index。

这相当于 `.css( "zIndex", zIndex )`。