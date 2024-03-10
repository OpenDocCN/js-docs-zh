# 与浏览器交互

# 书签

## 内容

1.  介绍
2.  对象和属性
3.  例子
4.  API 参考：chrome.bookmarks
    1.  方法
        1.  create
        2.  get
        3.  getChildren
        4.  getRecent
        5.  getTree
        6.  move
        7.  remove
        8.  removeTree
        9.  search
        10.  update
    2.  事件
        1.  onChanged
        2.  onChildrenReordered
        3.  onCreated
        4.  onImportBegan
        5.  onImportEnded
        6.  onMoved
        7.  onRemoved
    3.  类型
        1.  BookmarkTreeNode

使用 chrome.bookmarks 模块来创建、组织和管理书签。也可参看 Override Pages，来创建一个可定制的书签管理器页面。

![Clicking the star adds a bookmark](img/bookmarks.png)

## 介绍

您必须在扩展说明文件中声明使用书签 API 的权限。例如：

```js
{
  "name": "My extension",
  ...
  **"permissions": [
    "bookmarks"
  ]**,
  ...
} 
```

## 对象和属性

书签是按照树状结构组织的，每个节点都是一个书签或者一组节点（每个书签夹可包含多个节点）。每个节点都对应一个 BookmarkTreeNode 对象。

可以通过 chrome.bookmarks API 来使用 BookmarkTreeNode 的属性。例如，当调用函数 create()，可以传入参数新节点的父节点（父节点 ID），以及可选的节点索引，标题和 url 属性。可参看 BookmarkTreeNode 来获取节点的信息。

## 例子

下面的 代码创建了一个标题为 "Extension bookmarks"的书签夹。函数 create()的第一个参数指定了新书签夹的属性，第二个参数定义了一个在书签夹创建后要执行的回调函数

```js
chrome.bookmarks.create({'parentId': bookmarkBar.id,
                         'title': 'Extension bookmarks'},
                        function(newFolder) {
  console.log("added folder: " + newFolder.title);
}); 
```

接下来的代码创建了一个指向扩展开发文档的书签。如果创建书签失败，也不会引起什么问题，所以没有指定回调函数。

```js
chrome.bookmarks.create({'parentId': extensionsFolderId,
                         'title': 'Extensions doc',
                         'url': 'http://code.google.com/chrome/extensions'}); 
```

使用该 API 的实例请参看 [basic bookmarks sample](http://src.chromium.org/viewvc/chrome/trunk/src/chrome/common/extensions/docs/examples/api/bookmarks/basic/)。其他例子和源码请参看 Samples。

## API 参考：chrome.bookmarks

### Properties

#### getLastError

chrome.extensionlastError

### 方法

#### create

void chrome.bookmarks.create(, object `bookmark`, function `callback`)

Undocumented.

在指定父节点下创建一个书签或者书签夹。如果 url 为空，则创建一个书签夹。

#### 参数

`bookmark`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`parentId` 父节点 ID*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`index`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`title`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

The callback *parameter* should specify a function that looks like this:

如果需要指定回调函数，则回调函数格式如下：

```js
function(BookmarkTreeNode result) {...}; 
```

`result`*( optional enumerated BookmarkTreeNode array of paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### method name

void chrome.module.methodName(, ``)

Undocumented.

A description from the json schema def of the function goes here.

#### Parameters

#### Returns

#### Callback function

The callback *parameter* should specify a function that looks like this:

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Type param1, Type param2) {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### get

void chrome.bookmarks.get(, string or array of string `idOrIdList`, function `callback`)

Undocumented.

获取指定的书签节点。

#### 参数

`idOrIdList`*( optional enumerated Type array of string or array of string )*

Undocumented.

一个字符串类型的 Id，或者字符串数组

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

如果需要指定回调函数，则回调函数格式如下：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(array of BookmarkTreeNode results) {...}; 
```

`results`*( optional enumerated Type array of BookmarkTreeNode array of paramType paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### getChildren

void chrome.bookmarks.getChildren(, string `id`, function `callback`)

Undocumented.

获取指定的书签节点的子节点

#### 参数

`id`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

如果需要指定回调函数，则回调函数格式如下：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(array of BookmarkTreeNode results) {...}; 
```

`results`*( optional enumerated Type array of BookmarkTreeNode array of paramType paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### getRecent

void chrome.bookmarks.getRecent(, integer `numberOfItems`, function `callback`)

Undocumented.

获取最近添加的书签。

#### Parameters

`numberOfItems`*( optional enumerated Type array of integer )*

Undocumented.

最多返回的条目数量。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

如果需要指定回调函数，则回调函数格式如下：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(array of BookmarkTreeNode results) {...}; 
```

`results`*( optional enumerated Type array of BookmarkTreeNode array of paramType paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### getTree

void chrome.bookmarks.getTree(, function `callback`)

Undocumented.

按照层次结构获取所有书签。

#### Parameters

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

回调参数 *parameter* 指定的回调函数如下：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(array of BookmarkTreeNode results) {...}; 
```

`results`*( optional enumerated Type array of BookmarkTreeNode array of paramType paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### method name

void chrome.module.methodName(, ``)

Undocumented.

A description from the json schema def of the function goes here.

#### Parameters

#### Returns

#### Callback function

The callback *parameter* should specify a function that looks like this:

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Type param1, Type param2) {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### move

void chrome.bookmarks.move(, string `id`, object `destination`, function `callback`)

Undocumented.

移动指定的书签节点到指定的位置。

#### Parameters

`id`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`destination`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`parentId`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`index`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

如果需要指定*callback*参数，函数格式如下：

```js
function(BookmarkTreeNode result) {...}; 
```

`result`*( optional enumerated BookmarkTreeNode array of paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### remove

void chrome.bookmarks.remove(, string `id`, function `callback`)

Undocumented.

删除一个书签或者空书签夹。

#### Parameters

`id`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

如果需要指定*callback*参数，函数格式如下：

```js
function() {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### removeTree

void chrome.bookmarks.removeTree(, string `id`, function `callback`)

Undocumented.

删除书签夹目录（和它的子目录）。

#### 参数

`id`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

如果需要指定*callback*参数，函数格式如下：

```js
function() {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### search

void chrome.bookmarks.search(, string `query`, function `callback`)

Undocumented.

根据指定查询条件搜索书签节点。

#### 参数

`query`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

回调函数格式如下：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(array of BookmarkTreeNode results) {...}; 
```

`results`*( optional enumerated Type array of BookmarkTreeNode array of paramType paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### update

void chrome.bookmarks.update(, string `id`, object `changes`, function `callback`)

Undocumented.

更新书签或者书签夹的属性。指定需要改变的属性；未指定的属性将不会被改变。**注意：** 近期只支持 'title'和 'url'。

#### 参数

`id`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`changes`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`title`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

如果需要指定 callback 参数，函数格式如下：

```js
function(BookmarkTreeNode result) {...}; 
```

`result`*( optional enumerated BookmarkTreeNode array of paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

### 事件

#### onChanged

chrome.bookmarks.onChanged.addListener(function(string id, object changeInfo) {...});

Undocumented.

当书签或者书签夹发生改变时触发该事件。**注意：** 近期只有标题和 url 发生改变时，才触发该事件。

#### 参数

`id`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`changeInfo`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`title`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### onChildrenReordered

chrome.bookmarks.onChildrenReordered.addListener(function(string id, object reorderInfo) {...});

Undocumented.

由于 UI 中的顺序发生改变时，书签夹会改变其子节点的顺序，此时会触发该事件。函数 move()不会触发该事件。

#### Parameters

`id`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`reorderInfo`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`childIds`*( optional enumerated Type array of Type array of string paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### onCreated

chrome.bookmarks.onCreated.addListener(function(string id, BookmarkTreeNode bookmark) {...});

Undocumented.

当创建书签或者书签夹夹时，会触发该事件。

#### 参数

`id`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`bookmark`*( optional enumerated BookmarkTreeNode array of paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### onImportBegan

chrome.bookmarks.onImportBegan.addListener(function() {...});

Undocumented.

当开始导入书签时，会触发该事件 。事件响应者在导入结束前不要处理标签创建、更新的事件。但仍然可以立即处理其他事件。

#### Parameters

#### onImportEnded

chrome.bookmarks.onImportEnded.addListener(function() {...});

Undocumented.

当导入书签结束时，会触发该事件 。

#### Parameters

#### onMoved

chrome.bookmarks.onMoved.addListener(function(string id, object moveInfo) {...});

Undocumented.

当书签或者书签夹被移动到其他父书签夹时，触发该事件。

#### 参数

`id`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`moveInfo`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`parentId`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`index`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`oldParentId`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`oldIndex`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### onRemoved

chrome.bookmarks.onRemoved.addListener(function(string id, object removeInfo) {...});

Undocumented.

当书签和书签夹被删除时，触发该事件。当递归删除书签夹时，只会触发一个节点删除事件，它的子节点不会触发节点删除事件。

#### 参数

`id`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`removeInfo`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`parentId`*( optional enumerated Type array of string )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`index`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

### Types

#### BookmarkTreeNode

`paramName`*( optional enumerated Type array of object )*

Undocumented.

这个节点对象代表一个书签或者一个书签目录项。 节点对象有父子关系。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`id`*( optional enumerated Type array of string )*

Undocumented.

节点的唯一标识。IDs 在当前配置文件中是唯一的，浏览器重启后依然有效。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`parentId`*( optional enumerated Type array of string )*

Undocumented.

父节点的 ID。根节点没有父节点。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`index`*( optional enumerated Type array of integer )*

Undocumented.

在父节点的书签夹范围内，该节点的索引，从 0 开始。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string )*

Undocumented.

当用户点击书签时，浏览器访问的 url。书签夹没有该属性 。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`title`*( optional enumerated Type array of string )*

Undocumented.

节点的说明文字。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`dateAdded`*( optional enumerated Type array of number )*

Undocumented.

节点创建时距纪元时间的毫秒数。 (`new Date(dateAdded)`).

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`dateGroupModified`*( optional enumerated Type array of number )*

Undocumented.

书签夹内容的最后更新时间距纪元时间的毫秒数。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`children`*( optional enumerated Type array of BookmarkTreeNode array of paramType paramType )*

Undocumented.

节点的孩子的有序列表。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

# Cookies

## 内容

1.  清单
    1.  <a>h3Name</a>
2.  范例
    1.  <a>h3Name</a>
3.  API 参考: chrome.cookies
    1.  属性
        1.  propertyName
    2.  方法
        1.  get
        2.  getAll
        3.  getAllCookieStores
        4.  remove
        5.  set
    3.  事件
        1.  onChanged
    4.  类型
        1.  Cookie
        2.  CookieStore

For information on how to use experimental APIs, see the chrome.experimental.* APIs page.

Cookies

## 清单

要使用 cookies API, 你必须在你的清单中声明"cookies"权限，以及任何你希望 cookie 可以访问的主机权限。例如：

```js
{
  "name": "My extension",
  ...
  **"permissions": [
    "cookies",
    "*://*.google.com"
  ]**,
  ...
} 
```

## 范例

你可以在[examples/api/cookies](http://src.chromium.org/viewvc/chrome/trunk/src/chrome/common/extensions/docs/examples/api/cookies/)目录下找到一个使用 cookies API 的简单范例。对于其他的例子和查看源代码的帮助，参见 示例。

## API 参考: chrome.cookies

### 属性

#### getLastError

chrome.extensionlastError

### 方法

#### get

void chrome.cookies.get(, object `details`, function `callback`)

Undocumented.

获取一个 cookie 的信息。如果对于给定的 URL 有多个 cookie 存在，将返回对应于最长路径的 cookie。对于路径长度相同的 cookies，将返回最早创建的 cookie。

#### 参数

`details`*( optional enumerated Type array of object 对象 )*

Undocumented.

用于识别所收到的 cookie 的详细信息。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string 字符串 )*

Undocumented.

与所收到的 cookie 关联的 URL。这个参数可以是一个完整的 URL，这时候所有跟随在 URL 上的数据（比如查询字符串）将被忽略。如果清单文件中没有设置这个 URL 对应的主机权限，那么这个 API 调用会失败。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`name`*( optional enumerated Type array of string 字符串 )*

Undocumented.

收到的 cookie 名字。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`storeId`*( optional enumerated Type array of string 可选，字符串 )*

Undocumented.

cookie 的存储 id，用于从中检索 cookie。默认情况下，当前执行上下文的 cookie 存储将被使用。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function 函数 )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

如果指定了回调参数，它应该指定一个如下所示函数：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Cookie cookie) {...}; 
```

`cookie`*( optional enumerated Cookie array of paramType )*（可选，Cookie）

Undocumented.

包含 cookie 的详细信息。如果没找到 cookie，该参数为 null。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### getAll

void chrome.cookies.getAll(, object `details`, function `callback`)

Undocumented.

从一个 cookie 存储获取与给定信息匹配的所有 cookies。所获取 cookies 将按照最长路径优先排序。当多个 cookies 有相同长度路径，最早创建的 cookie 在前面。

#### 参数

`details`*( optional enumerated Type array of object )*

Undocumented.

对 cookies 进行筛选的信息。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string 可选，字符串 )*

Undocumented.

限定只查找与给定 URL 匹配的 cookies。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`name`*( optional enumerated Type array of string 可选，字符串 )*

Undocumented.

根据名称过滤 cookies。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`domain`*( optional enumerated Type array of string 可选，字符串 )*

Undocumented.

限定只查找与给定域名或者子域名匹配的 cookies。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`path`*( optional enumerated Type array of string 可选，字符串 )*

Undocumented.

限定只查找与给定路径完全一致的 cookies。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`secure`*( optional enumerated Type array of boolean 可选，Boolean 类型 )*

Undocumented.

根据 cookie 的 Secure 属性进行筛选。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`session`*( optional enumerated Type array of boolean 可选，Boolean 类型 )*

Undocumented.

根据 cookie 的生命周期是会话的还是持久的进行过滤。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`storeId`*( optional enumerated Type array of string 可选，字符串 )*

Undocumented.

cookie 的存储 id，用于从中检索 cookie。默认情况下，当前执行上下文的 cookie 存储将被使用。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

如果指定了回调参数，它应该指定一个如下所示函数：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(array of Cookie cookies) {...}; 
```

`cookies`*( optional enumerated Type array of Cookie array of paramType paramType* 可选，cookie 列表*)*

Undocumented.

所有与给定 cookie 信息匹配、存在并未过期的 cookie 列表。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### getAllCookieStores

void chrome.cookies.getAllCookieStores(, function `callback`)

Undocumented.

列举所有存在的 cookie 存储。

#### 参数

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

如果指定了回调参数，它应该指定一个如下所示函数：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(array of CookieStore cookieStores) {...}; 
```

`cookieStores`*( optional enumerated Type array of CookieStore* 可选，cookie 存储列表 *array of paramType paramType )*

Undocumented.

所有存在的 cookie 存储。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### remove

void chrome.cookies.remove(, object `details`)

Undocumented.

根据名称删除 cookie。

#### 参数

`details`*( optional enumerated Type array of object )*

Undocumented.

用于鉴定待删除 cookie 的信息。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string )*

Undocumented.

与所收到的 cookie 关联的 URL。如果清单文件中没有设置这个 URL 对应的主机权限，那么这个 API 调用会失败。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`name`*( optional enumerated Type array of string )*

Undocumented.

待删除 cookie 的名称。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`storeId`*( optional enumerated Type array of string )*

Undocumented.

cookie 的存储 id，用于从中检索 cookie。默认情况下，当前执行上下文的 cookie 存储将被使用。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

The callback *parameter* should specify a function that looks like this:

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Type param1, Type param2) {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### set

void chrome.cookies.set(, object `details`)

Undocumented.

用给定数据设置一个 cookie。如果相同的 cookie 存在，它们可能会被覆盖。

#### 参数

`details`*( optional enumerated Type array of object )*

Undocumented.

待设置 cookie 的详细信息。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string )*

Undocumented.

与待设置 cookie 相关的 URL。该值影响所创建 cookie 的默认域名与路径值。如果清单文件中没有设置这个 URL 对应的主机权限，那么这个 API 调用会失败。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`name`*( optional enumerated Type array of string )*

Undocumented.

cookie 名称，默认为空值。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`value`*( optional enumerated Type array of string )*

Undocumented.

cookie 的值，默认为空值。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`domain`*( optional enumerated Type array of string )*

Undocumented.

cookie 的域名。如果未指定，则该 cookie 是 host-only cookie。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`path`*( optional enumerated Type array of string )*

Undocumented.

cookie 的路径。默认是 url 参数的路径部分。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`secure`*( optional enumerated Type array of boolean )*

Undocumented.

是否 cookie 标记为保密。默认为 false。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`httpOnly`*( optional enumerated Type array of boolean )*

Undocumented.

是否 cookie 被标记为 HttpOnly。默认为 false。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`expirationDate`*( optional enumerated Type array of number )*

Undocumented.

cookie 的过期时间，用从 UNIX epoch 开始计的秒数表示。如果未指定，该 cookie 是一个会话 cookie。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`storeId`*( optional enumerated Type array of string )*

Undocumented.

用于保存该 cookie 的存储 id。默认情况下，当前执行上下文的 cookie 存储将被使用。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### Callback function

The callback *parameter* should specify a function that looks like this:

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Type param1, Type param2) {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

### 事件

#### onChanged

chrome.cookies.onChanged.addListener(function(object changeInfo) {...});

Undocumented.

当一个 cookie 被设置或者删除时候触发。

#### 参数

`changeInfo`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`removed`*( optional enumerated Type array of boolean )*

Undocumented.

True 表示一个 cookie 被删除。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`cookie`*( optional enumerated Cookie array of paramType )*

Undocumented.

被设置或者删除的 cookie 的信息。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

### 类型

#### Cookie

`paramName`*( optional enumerated Type array of object )*

Undocumented.

表示一个 HTTP cookie 的信息。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`name`*( optional enumerated Type array of string )*

Undocumented.

cookie 名称。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`value`*( optional enumerated Type array of string )*

Undocumented.

cookie 值。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`domain`*( optional enumerated Type array of string )*

Undocumented.

cookie 的域名。(例如 "www.google.com", "example.com").

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`hostOnly`*( optional enumerated Type array of boolean )*

Undocumented.

True 表示 cookie 是一个 host-only cookie (例如，一个检索的主机必须与 cookie 的域名完全一致）。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`path`*( optional enumerated Type array of string )*

Undocumented.

cookie 的路径。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`secure`*( optional enumerated Type array of boolean )*

Undocumented.

True 表示 cookie 被标记为保密。(例如，它的有效范围被限制于加密频道，最典型是 HTTPS).

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`httpOnly`*( optional enumerated Type array of boolean )*

Undocumented.

True 表示 cookie 被标记为 HttpOnly (例如 cookie 在客户端的脚本无法访问)。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`session`*( optional enumerated Type array of boolean )*

Undocumented.

True 表示 cookie 是线程 cookie，与有过期时间的持久 cookie 相对应。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`expirationDate`*( optional enumerated Type array of number )*

Undocumented.

cookie 的过期时间，用从 UNIX epoch（00:00:00 UTC on 1 January 1970）开始计的秒数表示。会话 cookie 没有该属性。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`storeId`*( optional enumerated Type array of string )*

Undocumented.

包含该 cookie 的存储 id，可通过 getAllCookieStores()获取。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### CookieStore

`paramName`*( optional enumerated Type array of object )*

Undocumented.

表示浏览器中的 cookie 存储。那些隐藏模式窗体使用与非隐藏窗体不同的一个独立 cookie 存储。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`id`*( optional enumerated Type array of string )*

Undocumented.

cookie 存储的唯一 id。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`tabIds`*( optional enumerated Type array of Type array of integer paramType )*

Undocumented.

共享该 cookie 存储的浏览器标签集合的 id 列表。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

# chrome.devtools.* APIs

下列 API 模块提供了开发人员工具的部分接口，以支持您对开发人员工具进行扩展。

*   devtools.inspectedWindow
*   devtools.network
*   devtools.panels

## 如何使用 DevTools APIs

1.  1\. 在扩展的 manifest 中指定 "devtools_page"项：

    ```js
    {
      "name": ...
      "version": "1.0",
      "minimum_chrome_version": "10.0",
      **"devtools_page": "devtools.html"**,
      ...
    } 
    ```

2.  2\. 一旦开发人员工具窗口打开，将会创建一个 manifest 中 devtools_page 项指定的实例。通过使用 devtools.panels ，这个页面可以在开发人员工具窗口中添加其他扩展页面，如面板或侧边栏等。

3.  3\. chrome 的 devtools.* API 模块仅适用于在开发人员工具窗口中加载的页面。Content scripts 和其他的扩展页面无法使用这些接口。也因此,该模块仅在开发人员工具窗口的生命周期内可用。
4.  4\. 在开发人员工具窗口内扩展页面可用的接口包括所有的 上面列举出来的 devtools 模块 和 chrome.extension API。其他扩展 API 在开发人员工具页面都无法使用，您可以通过扩展的 background page 里发送请求来调用它们，这和在 content scripts 中调用类似。
5.  5\. 还有一些开发人员工具 API 仍处于试验阶段。您可以通过 [chrome.experimental.* APIs](http://code.google.com/chrome/extensions/experimental.html) 获取这些 API 列表并了解如何使用它们。
6.  6\. [意见反馈！](http://groups.google.com/group/google-chrome-developer-tools/topics) 您的意见和建议将会帮助我们改进这些 API。

## 更多信息

想了解扩展可以使用的标准 API 信息,您可以访问 [chrome.* APIs](http://code.google.com/chrome/extensions/api_index.html) 和 [Other APIs](http://code.google.com/chrome/extensions/api_other.html) 。

## 示例

您可以通过 Samples 找到使用开发人员工具 API 的示例。

# Events

For information on how to use experimental APIs, see the chrome.experimental.* APIs page.

`Event` 是一个对象，当你关注的一些事情发生时通知你。 以下是一个使用 `chrome.tabs.onCreated event` 的例子，每当一个新标签创建时，event 对象会得到通知：

```js
chrome.tabs.onCreated.**addListener(function(**tab**) {**
  appendToLog('tabs.onCreated --'
              + ' window: ' + tab.windowId
              + ' tab: '    + tab.id
              + ' index: '  + tab.index
              + ' url: '    + tab.url);
**});** 
```

如示例所示，使用 `addListener()` 方法注册通知。 `addListener()` 方法的参数总是一个函数，是你定义来处理事件的函数， 但该函数的参数取决于你的事件处理。 查看 `chrome.tabs.onCreated` 的文档， 你可以看到该函数有一个参数：一个 Tab 对象，包含新创建的标签的信息。

## 方法

你可以调用任何 `Event` 对象的以下方法：

```js
void addListener(function callback(...))
void removeListener(function callback(...))
bool hasListener(function callback(...)) 
```

# chrome.history

chorme.history 模块被用于和浏览器所访问的页面记录交互。你可以添加、删除、查询浏览器的历史记录。如果您想覆写历史页面，请查看 Override 替代页.

## Manifest

您必须在扩展 Manifest 文件中定义"history"许可，以便使用 history API. 如下所示：

```js
{
  "name": "My extension",
  ...
  **"permissions": [
    "history"
  ]**,
  ...
} 
```

## 过渡类型

History API 用一种过渡类型来描述浏览器是如何访问的特定的 URL。例如：如果 URL 是在用户访问页面时，点击链接跳转访问的，此时的过渡类型为 "link"。

如下的列表详细定义了各种过渡类型。.

| 过渡类型 | 描述 |
| --- | --- |
| "link" | 用户通过点击页面中的链接，跳转至本 URL |
| "typed" | 用户通过地址栏输入网址，来访问本 URL。这种类型也适用于显式的导航动作。与之相反，你可以参阅 generated，它适用于用户没看到（不知道）网址 URL 的情况。 |
| "auto_bookmark" | 用户通过界面的推荐到达本 URL。例如，通过点击菜单项打开的页面。 |
| "auto_subframe" | 子框架导航。这种类型是指那些非顶层框架自动加载的内容。例如，如果一个页面由许多包含广告的子框架构成， 那些广告链就拥有这种过渡类型。用户可能没有意识到页面中的这些内容是个单独的框架，所以他们也可能根本没有在意这些 URL（请查阅 manual_subframe)。 |
| "manual_subframe" | 此种类型是为用户显式请求的子框架导航以及在前进/后退列表中的生成导航入口的子框架导航所设置。由于用户更关心所请求框架被加载的效果，因此显式请求的框架可能会比自动载入的框架更为重要。 |
| "generated" | 用户通过在地址栏输入，而选择一个不像网址的入口到达的 URL 页面。例如，匹配结果中可能包含 Google 搜索结果页的 URL, 但是它可能以"Google 搜索"的形式展现。这类导航和 typed 导航是有差异的，因为用户没有输入或者看到最终的 URL。请参阅 keyword。 |
| "start_page" | 页面是在命令行中被指定（打开），或者其本身就是起始页。 |
| "form_submit" | 用户提交的表单。请注意，某些情况，诸如表单运用脚本来提交，不属于此种类型。 |
| "reload" | 用户通过点击刷新按钮或者在地址栏输入回车键来刷新页面属于此种类型。会话重置，重开标签页都属于此种类型。 |
| "keyword" | URL 通过可替代的关键字，而不是默认的搜索引擎产生。请查阅 keyword_generated 。 |
| "keyword_generated" | 相应由关键字生成的访问。请查阅 keyword。 |

## 示例

请查看 [history 样例目录](http://src.chromium.org/viewvc/chrome/trunk/src/chrome/common/extensions/docs/examples/api/history/) 和 [history API 测试目录](http://src.chromium.org/viewvc/chrome/trunk/src/chrome/test/data/extensions/api_test/history/) 中如何使用 API 的例子。 如果想获取源代码中的样例及帮助，请查看 样例。

## API reference: chrome.history

### Properties

#### getLastError

chrome.extensionlastError

### Methods

#### addUrl

void chrome.history.addUrl(, object `details`)

Undocumented.

在当前历史记录中添加一条过渡类型为"link"的 URL。

#### Parameters

`details`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string )*

Undocumented.

要添加的 URL。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### Callback function

The callback *parameter* should specify a function that looks like this:

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Type param1, Type param2) {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### deleteAll

void chrome.history.deleteAll(, function `callback`)

Undocumented.

删除历史记录中的所有条目。

#### Parameters

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### Callback function

回调函数的*参数*应当如下定义：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function() {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### deleteRange

void chrome.history.deleteRange(, object `range`, function `callback`)

Undocumented.

删除特定日期范围内的所有历史记录条目。页面本身只会在所有访问均在所设定日期的范围内才会被删除。

#### Parameters

`range`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`startTime`*( optional enumerated Type array of number )*

Undocumented.

条目添加起始时间， 以纪元开始的毫秒数表示。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`endTime`*( optional enumerated Type array of number )*

Undocumented.

条目添加终止时间， 以纪元开始的毫秒数表示。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### Callback function

回调函数的*参数*应当如下定义：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function() {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### deleteUrl

void chrome.history.deleteUrl(, object `details`)

Undocumented.

删除指定 URL 的所有历史记录。

#### Parameters

`details`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string )*

Undocumented.

要删除的 URL。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### Callback function

The callback *parameter* should specify a function that looks like this:

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Type param1, Type param2) {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### getVisits

void chrome.history.getVisits(, object `details`, function `callback`)

Undocumented.

获取访问特定 URL 的所有信息。

#### Parameters

`details`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string )*

Undocumented.

需要获取访问信息的 URL。URL 必须与历史记录搜索的返回值格式一致。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### Callback function

回调函数的*参数*应当如下定义：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(array of VisitItem results) {...}; 
```

`results`*( optional enumerated Type array of VisitItem array of paramType paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### search

void chrome.history.search(, object `query`, function `callback`)

Undocumented.

搜索历史中，匹配条件的最后一次访问的页面。

#### Parameters

`query`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`text`*( optional enumerated Type array of string )*

Undocumented.

历史服务的文字查询。若想获取所有页面的信息，把此参数设置为空。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`startTime`*( optional enumerated Type array of number )*

Undocumented.

限制结果访问日期至此日期之后, 以纪元开始的毫秒数表示。.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`endTime`*( optional enumerated Type array of number )*

Undocumented.

限制结果访问日期至此日期以前, 以纪元开始的毫秒数表示。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`maxResults`*( optional enumerated Type array of integer )*

Undocumented.

所获取结果的最大数目。 默认值为 100。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### Callback function

回调函数的*参数*应当如下定义：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(array of HistoryItem results) {...}; 
```

`results`*( optional enumerated Type array of HistoryItem array of paramType paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

### Events

#### onVisitRemoved

chrome.history.onVisitRemoved.addListener(function(object removed) {...});

Undocumented.

当一条或着多条 URL 从历史服务中删除，此事件触发。当所有访问被移除后， 此条 URL 从来历史记录中被移除。

#### Parameters

`removed`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`allHistory`*( optional enumerated Type array of boolean )*

Undocumented.

如需删除所有历史记录，则设置成 True。如果设置成 true, 所有 url 为空。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`urls`*( optional enumerated Type array of Type array of string paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### onVisited

chrome.history.onVisited.addListener(function(HistoryItem result) {...});

Undocumented.

当 URL 被访问时，此事件被触发。并提供相应 URL 的 HistoryItem 数据。

#### Parameters

`result`*( optional enumerated HistoryItem array of paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

### Types

#### HistoryItem

`paramName`*( optional enumerated Type array of object )*

Undocumented.

封装历史查询结果的对象。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`id`*( optional enumerated Type array of string )*

Undocumented.

条目的唯一标识符。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string )*

Undocumented.

用户所访问的 URL。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`title`*( optional enumerated Type array of string )*

Undocumented.

历史页面的标题。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`lastVisitTime`*( optional enumerated Type array of number )*

Undocumented.

页面被载入的最后时间, 以纪元开始的毫秒数表示。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`visitCount`*( optional enumerated Type array of integer )*

Undocumented.

用户访问此页面的次数。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`typedCount`*( optional enumerated Type array of integer )*

Undocumented.

用户通过地址栏输入访问目的页面的次数。

#### VisitItem

`paramName`*( optional enumerated Type array of object )*

Undocumented.

封装 URL 访问的对象。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`id`*( optional enumerated Type array of string )*

Undocumented.

条目的唯一标识符。

`visitId`*( optional enumerated Type array of string )*

Undocumented.

访问的唯一标识符。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`visitTime`*( optional enumerated Type array of number )*

Undocumented.

访问的时间， 以纪元开始的毫秒数表示。

`referringVisitId`*( optional enumerated Type array of string )*

Undocumented.

访问来源的 visit_id 。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`transition`*( optional enumerated Type array of string ["link", "typed", "auto_bookmark", "auto_subframe", "manual_subframe", "generated", "start_page", "form_submit", "reload", "keyword", "keyword_generated"] )*

Undocumented.

访问来源的过渡类型。

# Management

`chrome.management` 模块提供了管理已安装和正在运行中的扩展或应用的方法。对于重写内建的新标签页的扩展尤其有用。

## Manifest

要使用这个 API，您必须在扩展清单文件中 中对授权，例如:

```js
{
  "name": "My extension",
  ...
  **"permissions": [ "management" ]**,
  ...
} 
```

只有一个方法不需要事先授权使用，那就是: `getPermissionWarningsByManifest`

## API reference: chrome.management

### 方法

#### get

chrome.management.get(string `id`, function `callback`)

获得指定 id 的扩展/应用的信息。

#### 参数

`id`*( string )*

应用或扩展（ExtensionInfo）中的 ID。

`callback`*( optional function )*

#### 回调

如果你指定了 *回调函数* 它看起来应该像下面这个样子：

```js
function(ExtensionInfo result) {...}; 
```

`result`*( ExtensionInfo )*

#### getAll

chrome.management.getAll(function `callback`)

返回所有已安装的扩展。

#### 参数

`callback`*( optional function )*

#### 回调

如果你指定了 *回调函数*，它看起来应该像下面这个样子：

```js
function(array of ExtensionInfo result) {...}; 
```

`result`*( array of ExtensionInfo )*

#### getPermissionWarningsById

chrome.management.getPermissionWarningsById(string `id`, function `callback`)

获得指定 id 的扩展的 [授权 警告](http://code.google.com/chrome/extensions/permission_warnings.html)。

#### 参数

`id`*( string )*

`callback`*( optional function )*

#### 回调

如果你指定了 *回调函数*它看起来应该像下面这个样子：

```js
function(array of string permissionWarnings) {...}; 
```

`permissionWarnings`*( array of string )*

#### getPermissionWarningsByManifest

chrome.management.getPermissionWarningsByManifest(string `manifestStr`, function `callback`)

获得指定的 manifest 清单文件中所包含的[权限警告](http://code.google.com/chrome/extensions/permission_warnings.html)清单。注意，这一函数不需要在 manifest 文件中进行授权就可以使用。

#### 参数

`manifestStr`*( string )*

扩展的 manifest 文件内容（是个 JSON 字符串）。

`callback`*( optional function )*

#### 回调

如果你指定了 *回调函数*，它看起来应该像下面这个样子：

```js
function(array of string permissionWarnings) {...}; 
```

`permissionWarnings`*( array of string )*

#### launchApp

chrome.management.launchApp(string `id`, function `callback`)

启动一个应用。

#### 参数

`id`*( string )*

应用的唯一 ID。

`callback`*( optional function )*

#### 回调

如果你指定了 *回调函数*，它看起来应该像下面这个样子：

```js
function() {...}; 
```

#### setEnabled

chrome.management.setEnabled(string `id`, boolean `enabled`, function `callback`)

启用或禁用一个应用或扩展。

#### 参数

`id`*( string )*

应用或扩展（ExtensionInfo）的唯一 ID。

`enabled`*( boolean )*

应用或扩展是否被启用或禁用。

`callback`*( optional function )*

#### 回调

如果你指定了 *回调函数*，它看起来应该像下面这个样子：

```js
function() {...}; 
```

#### uninstall

chrome.management.uninstall(string `id`, function `callback`)

卸载一个应用或扩展。

#### 参数

`id`*( string )*

应用或扩展（ExtensionInfo）的唯一 ID。

`callback`*( optional function )*

#### 回调

If you specify the *callback* parameter, it should specify a function that looks like this:

如果你指定了 *回调函数*，它看起来应该像下面这个样子：

```js
function() {...}; 
```

### 事件

#### onDisabled

chrome.management.onDisabled.addListener(function(ExtensionInfo info) {...});

当应用或扩展被禁用时触发。

#### 参数

`info`*( ExtensionInfo )*

#### onEnabled

chrome.management.onEnabled.addListener(function(ExtensionInfo info) {...});

当应用或扩展被启用时触发。

#### 参数

`info`*( ExtensionInfo )*

#### onInstalled

chrome.management.onInstalled.addListener(function(ExtensionInfo info) {...});

当应用或扩展被安装时触发。

#### 参数

`info`*( ExtensionInfo )*

#### onUninstalled

chrome.management.onUninstalled.addListener(function(string id) {...});

当应用或扩展被卸载时触发。

#### 参数

`id`*( string )*

被卸载的扩展或应用的 id。

### 类型

#### IconInfo

*( object )*

扩展或应用的图标信息。

`size`*( integer )*

一个表示图标宽高的整数值，比如 128、48、24、16 或者其他值。

`url`*( string )*

该图标图像的 URL。如果要显示一个灰度版本的图标（例如表示扩展程序已禁用时），请在 URL 后附加`grayscale=true`

#### ExtensionInfo

*( object )*

已安装的扩展或应用的的信息。

`id`*( string )*

该扩展的唯一 ID。

`name`*( string )*

扩展或应用的名字。

`description`*( string )*

扩展或应用的描述信息。

`version`*( string )*

扩展或应用的版本。

`mayDisable`*( boolean )*

该扩展是否允许用户禁用和卸载。

`enabled`*( boolean )*

该扩展当前是否被启用或禁用。

`disabledReason`*( optional enumerated string ["unknown", "permissions_increase"] )*

当前扩展或应用被禁用的原因。

`isApp`*( boolean )*

是否是应用，如果 true，则是。

`appLaunchUrl`*( optional string )*

应用的启动 URL。

`homepageUrl`*( optional string )*

扩展或应用的主页。

`updateUrl`*( optional string )*

扩展或应用的升级页。

`offlineEnabled`*( boolean )*

扩展或应用是否支持离线使用。

`optionsUrl`*( string )*

扩展或应用的选项页，如果它们进行选项配置的话。

`icons`*( optional array of IconInfo )*

包含所有图标信息。注意这只反映声明在清单文件中的信息，URL 指定的实际图像可能比声明的更大或更小，所以您引用这些图像时可能要考虑在图像标签中显式使用 width 和 height 属性。有关更多细节，请参见 manifest documentation on icons。

`permissions`*( array of string )*

根据授权情况返回允许使用的所有 API 列表。

`hostPermissions`*( array of string )*

根据授权情况返回所有允许访问的主机白名单。

# 标签

chrome 标签模块被用于和浏览器的标签系统交互。此模块被用于创建，修改，重新排列浏览器中的标签。.

![Two tabs in a window](img/tabs.png)

## Manifest

几乎所有 chrome 标签方法需要你在 extension manifest 中定义标签权限。例如：

```js
{
  "name": "My extension",
  ...
  **"permissions": [
    "tabs"
  ]**,
  ...
} 
```

不需要"标签"权限的方法是：create 和 update.

## 示例

你可以在[examples/api/tabs](http://src.chromium.org/viewvc/chrome/trunk/src/chrome/common/extensions/docs/examples/api/tabs/) 目录下找到运用标签模块的示例。在源代码中查看帮助或者示例，请查阅 Samples

。

## API reference: chrome.tabs

### Properties

#### getLastError

chrome.extensionlastError

### Methods

#### captureVisibleTab

void chrome.tabs.captureVisibleTab(, integer `windowId`, object `options`, function `callback`)

Undocumented.

在特定窗口中，抓取当前选中标签的可视区域。 这要求必须在 host permission 中指定对标签 URL 的访问权限。

#### Parameters

`windowId`*( optional enumerated Type array of integer )*

Undocumented.

目标窗口，默认值为当前窗口.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`options`*( optional enumerated Type array of object )*

Undocumented.

设置抓取图像参数。设置图像抓取的参数，比如生成的图像的格式。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`format`*( optional enumerated Type array of string ["jpeg", "png"] )*

Undocumented.

生成的图像的格式。默认是 jpeg。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`quality`*( optional enumerated Type array of integer )*

Undocumented.

如果格式是'jpeg'，控制结果图像的质量。此参数对 PNG 图像无效。当质量降低的时候，抓取的画质会下降，需要存储的字节数也会递减。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### Callback function

回调 *参数* 应该如下定义：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(string dataUrl) {...}; 
```

`dataUrl`*( optional enumerated Type array of string )*

Undocumented.

被抓取标签的可视区域的 URL。此 URL 可能会作为图像的 src 属性。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### connect

Port chrome.tabs.connect(, integer `tabId`, object `connectInfo`)

Undocumented.

连接到特定标签中的 content script(s)。 事件 chrome.extension.onConnect 将被触发给每个指定页面上运行的 content script 扩展。了解更多请查看 Content Script Messaging。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`connectInfo`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`name`*( optional enumerated Type array of string )*

Undocumented.

会被传输到监听连接事件的 content scirpt 的 onConnect 函数当中。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

`paramName`*( optional enumerated Port array of paramType )*

Undocumented.

可以和在指定标签中运行的内容脚本通信。当标签被关闭或者不存在时，端口的 onDisconnect 事件被触发。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Callback function

The callback *parameter* should specify a function that looks like this:

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Type param1, Type param2) {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### create

void chrome.tabs.create(, object `createProperties`, function `callback`)

Undocumented.

创建新的标签。注： 无需请求 manifest 的标签权限，此方法也可以被使用。

#### Parameters

`createProperties`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`windowId`*( optional enumerated Type array of integer )*

Undocumented.

创建新标签的目标窗口。默认是当前窗口 。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`index`*( optional enumerated Type array of integer )*

Undocumented.

标签在窗口中的位置。 值在零至标签数量之间。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string )*

Undocumented.

标签导航的初始页面。完整的 URL 必须包含一个前缀 (如 '[`www.google.com`](http://www.google.com)', 不能写为 'www.google.com')。 相对 URL 则与扩展所在的页面相对， 默认值为新标签页面。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`selected`*( optional enumerated Type array of boolean )*

Undocumented.

标签是否成为选中标签。默认为 true。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`pinned`*( optional enumerated Type array of boolean )*

Undocumented.

标签是否被固定。默认值为 false。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### Callback function

The callback *parameter* should specify a function that looks like this:

回调 *参数* 应该如下定义：

```js
function(Tab tab) {...}; 
```

`tab`*( optional enumerated Tab array of paramType )*

Undocumented.

所创建的标签的细节，包含新标签的 ID。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### detectLanguage

void chrome.tabs.detectLanguage(, integer `tabId`, function `callback`)

Undocumented.

检测标签内容的主要语言。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

默认为"当前窗口"所选定的标签。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### Callback function

回调 *参数* 应该如下定义：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(string language) {...}; 
```

`language`*( optional enumerated Type array of string )*

Undocumented.

ISO 语言编码，例如 en 或者 fr。若要查看此方法支持的完整语言列表，请参阅[kLanguageInfoTable](http://src.chromium.org/viewvc/chrome/trunk/src/third_party/cld/languages/internal/languages.cc) 。第 2 列和第 4 列会被检测，而且第一个不为空的值会被返回。 简体中文是个例外，返回 zh-CN。对于未知语言，返回 und。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### executeScript

void chrome.tabs.executeScript(, integer `tabId`, object `details`, function `callback`)

Undocumented.

向页面注入 JavaScript 脚本执行。要了解详情，请查阅内容脚本文档的 programmatic injection 部分。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

运行脚本的标签 ID；默认为当前窗口所选中的标签。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`details`*( optional enumerated Type array of object )*

Undocumented.

要执行的脚本内容，可选 code 或者 file，但不能同时选两者。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`code`*( optional enumerated Type array of string )*

Undocumented.

要执行的脚本代码。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`file`*( optional enumerated Type array of string )*

Undocumented.

要执行的脚本文件。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`allFrames`*( optional enumerated Type array of boolean )*

Undocumented.

true 的时候，给所有 frame 执行脚本。默认为 false，只给顶级 frame 执行脚本。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

所有脚本执行后会被调用的回调。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### Callback function

The callback *parameter* should specify a function that looks like this:

回调 *参数* 应该如下定义：

```js
function() {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### get

void chrome.tabs.get(, integer `tabId`, function `callback`)

Undocumented.

获取指定标签的细节信息。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

回调 *参数* 应该如下定义：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Tab tab) {...}; 
```

`tab`*( optional enumerated Tab array of paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### getAllInWindow

void chrome.tabs.getAllInWindow(, integer `windowId`, function `callback`)

Undocumented.

获取指定窗口所有标签的细节信息。

#### Parameters

`windowId`*( optional enumerated Type array of integer )*

Undocumented.

默认为当前窗口。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

T 回调 *参数* 应该如下定义：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(array of Tab tabs) {...}; 
```

`tabs`*( optional enumerated Type array of Tab array of paramType paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### getCurrent

void chrome.tabs.getCurrent(, function `callback`)

Undocumented.

获取生成脚本调用的标签。此函数不适用于脚本被非标签内容调用的情况。(例如: 背景页 或者 弹出视图) 。

#### Parameters

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

回调 *参数* 应该如下定义：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Tab tab) {...}; 
```

`tab`*( optional enumerated Tab array of paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### getSelected

void chrome.tabs.getSelected(, integer `windowId`, function `callback`)

Undocumented.

获取特定窗口指定的标签。

#### Parameters

`windowId`*( optional enumerated Type array of integer )*

Undocumented.

默认为当前窗口。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

回调 *参数* 应该如下定义：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Tab tab) {...}; 
```

`tab`*( optional enumerated Tab array of paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### insertCSS

void chrome.tabs.insertCSS(, integer `tabId`, object `details`, function `callback`)

Undocumented.

向页面注入 CSS。要了解详情，请参阅内容脚本文档中的 programmatic injection 部分。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

要注入 CSS 的标签 ID；默认为当前窗口选定的标签。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`details`*( optional enumerated Type array of object )*

Undocumented.

要注入的 CSS 的内容，可选 code 或者 file，但不能同时选两者。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`code`*( optional enumerated Type array of string )*

Undocumented.

要注入的 CSS 代码。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`file`*( optional enumerated Type array of string )*

Undocumented.

要注入的 CSS 文件。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`allFrames`*( optional enumerated Type array of boolean )*

Undocumented.

true 的时候，给所有 frame 注入 CSS。默认为 false，只给顶级 frame 注入 CSS。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

当所有的 CSS 被注入后，回调被调用。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

回调 *参数* 应该如下定义：

```js
function() {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### move

void chrome.tabs.move(, integer `tabId`, object `moveProperties`, function `callback`)

Undocumented.

把标签移动至窗口内特定的位置，或者移至一个新窗口。请注意只能在普通窗口之间切移(window.type === "normal") 。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`moveProperties`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`windowId`*( optional enumerated Type array of integer )*

Undocumented.

默认为标签所在的窗口。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`index`*( optional enumerated Type array of integer )*

Undocumented.

移动到的目标窗口位置。赋值必须在零至目标窗口的标签数目之间。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

回调 *参数* 应该如下定义：

```js
function(Tab tab) {...}; 
```

`tab`*( optional enumerated Tab array of paramType )*

Undocumented.

所被移动的标签细节。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### remove

void chrome.tabs.remove(, integer `tabId`, function `callback`)

Undocumented.

关闭标签。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

回调 *参数* 应该如下定义：

```js
function() {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### sendRequest

void chrome.tabs.sendRequest(, integer `tabId`, any `request`, function `responseCallback`)

Undocumented.

向特定的标签 content script 发送一个的请求， 并在响应返回时，可附带一个回调。在所有 content script 响应请求后， chrome.extension.onRequest 事件将会为当前扩展触发。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`request`*( optional enumerated Type array of any )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`responseCallback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

##### Parameters

`response`*( optional enumerated Type array of any )*

Undocumented.

响应的 JSON 对象。如果错误发生，回调将不会有参数。并会在 chrome.extension.lastError 产生一个错误。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

回调 *参数* 应该如下定义：

```js
function(any response) {...}; 
```

`response`*( optional enumerated Type array of any )*

Undocumented.

响应的 JSON 对象。如果错误发生，回调将不会有参数。并会在 chrome.extension.lastError 产生一个错误。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### update

void chrome.tabs.update(, integer `tabId`, object `updateProperties`, function `callback`)

Undocumented.

修改标签的属性。没有在 updateProperties 中指定的属性不会被修改。注：即使没有向 manifest 请求'tabs'权限，这个方法依然适用。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`updateProperties`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of undefined )*

Undocumented.

让标签浏览的 URL。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`selected`*( optional enumerated Type array of boolean )*

Undocumented.

标签是否应被选中。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`pinned`*( optional enumerated Type array of boolean )*

Undocumented.

标签是否应被固定。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

The callback *parameter* should specify a function that looks like this:

回调 *参数* 应该如下定义：

```js
function(Tab tab) {...}; 
```

`tab`*( optional enumerated Tab array of paramType )*

Undocumented.

被更新的标签细节。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

### Events

#### onAttached

chrome.tabs.onAttached.addListener(function(integer tabId, object attachInfo) {...});

Undocumented.

当标签附着在窗口上，此事件被触发。例如，此事件会发生在标签在窗口之前移动时。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`attachInfo`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`newWindowId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`newPosition`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### onCreated

chrome.tabs.onCreated.addListener(function(Tab tab) {...});

Undocumented.

标签创建时，此事件触发。请注意，当事件触发时，标签的 URL 可能没有被设置， 但是当 URL 被设置时，可以通过 onUpdated 事件接听。

#### Parameters

`tab`*( optional enumerated Tab array of paramType )*

Undocumented.

标签创建的细节。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### onDetached

chrome.tabs.onDetached.addListener(function(integer tabId, object detachInfo) {...});

Undocumented.

当标签从窗口脱离时，此事件被触发，例如标签在窗口之间移动。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`detachInfo`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`oldWindowId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`oldPosition`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### onMoved

chrome.tabs.onMoved.addListener(function(integer tabId, object moveInfo) {...});

Undocumented.

当标签在窗口内移动时，此事件被触发。只有一个移动事件被触发，给用户直接移动的标签。其他响应移动事件的标签不触发移动事件。 请参阅 onDetached.查看详情。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`moveInfo`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`windowId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`fromIndex`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`toIndex`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### onRemoved

chrome.tabs.onRemoved.addListener(function(integer tabId, object removeInfo) {...});

Undocumented.

标签关闭时被触发。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`removeInfo`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`isWindowClosing`*( optional enumerated Type array of boolean )*

Undocumented.

当窗口被关闭，标签随之被关闭时，此参数为 true。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### onSelectionChanged

chrome.tabs.onSelectionChanged.addListener(function(integer tabId, object selectInfo) {...});

Undocumented.

当窗口选中的标签改变时，此事件触发

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

被选中标签的 ID。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`selectInfo`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`windowId`*( optional enumerated Type array of integer )*

Undocumented.

标签发生变化的窗口 ID。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### onUpdated

chrome.tabs.onUpdated.addListener(function(integer tabId, object changeInfo, Tab tab) {...});

Undocumented.

当标签更新时，此事件被触发。

#### Parameters

`tabId`*( optional enumerated Type array of integer )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`changeInfo`*( optional enumerated Type array of object )*

Undocumented.

列出标签更新时的状态。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`status`*( optional enumerated Type array of string )*

Undocumented.

标签的状态。可以为 *loading* or *complete*。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string )*

Undocumented.

经历变化的标签的 URL。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`pinned`*( optional enumerated Type array of boolean )*

Undocumented.

标签被锁定的新状态。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`tab`*( optional enumerated Tab array of paramType )*

Undocumented.

更新的标签的状态。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

### Types

#### Tab

`paramName`*( optional enumerated Type array of object )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`id`*( optional enumerated Type array of integer )*

Undocumented.

标签 ID。在一个浏览器会话内， 标签 ID 是唯一的。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`index`*( optional enumerated Type array of integer )*

Undocumented.

窗口内从零开始的标签索引。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`windowId`*( optional enumerated Type array of integer )*

Undocumented.

标签所在窗口的窗口 ID。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`selected`*( optional enumerated Type array of boolean )*

Undocumented.

标签是否被选中。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`pinned`*( optional enumerated Type array of boolean )*

Undocumented.

标签是否被锁定。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string )*

Undocumented.

标签所显示的 URL。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`title`*( optional enumerated Type array of string )*

Undocumented.

标签的标题。当标签被加载时，标题可能不能被成功获取。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`favIconUrl`*( optional enumerated Type array of string )*

Undocumented.

标签收藏夹图标的 URL。当标签被加载时，图标可能不能被成功获取。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`status`*( optional enumerated Type array of string )*

Undocumented.

可以被设置为 *loading* 或者 *complete*。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`incognito`*( optional enumerated Type array of boolean )*

Undocumented.

可以被设置为 *loading* 或者 *complete*.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

# 视窗

## 内容

1.  清单
    1.  <a>h3Name</a>
2.  当前视窗
    1.  <a>h3Name</a>
3.  范例
    1.  <a>h3Name</a>
4.  API 参考: chrome.windows
    1.  属性
        1.  WINDOW_ID_NONE
    2.  方法
        1.  create
        2.  get
        3.  getAll
        4.  getCurrent
        5.  getLastFocused
        6.  remove
        7.  update
    3.  事件
        1.  onCreated
        2.  onFocusChanged
        3.  onRemoved
    4.  类型
        1.  Window

For information on how to use experimental APIs, see the chrome.experimental.* APIs page.

## 视窗

使用 chrome.windows 模块与浏览器视窗进行交互。 你可以使用这个模块在浏览器中创建、修改和重新排列视窗。

![Two windows, each with one tab](img/windows.png)

## 清单

要使用视窗 API，你必须在 manifest.json 声明"tabs"的权限 。（不，这不是一个错字 - 窗口和标签模块的互动如此密切，我们决定它们共享一个权限。）例如：

```js
{
  "name": "My extension",
  ...
  **"permissions": ["tabs"]**,
  ...
} 
```

## 当前视窗

很多扩展系统的功能有一个可选的 windowId 参数，其默认值为当前视窗。

*当前视窗*是指包含当前正在执行的代码的视窗。重要的是要认识到，它可以跟最顶层或有焦点的视窗不一样。

例如，假设一个扩展从一个单一的 HTML 文件中创建了一些标签或视窗，而这个 HTML 文件包含一个 chrome.tabs.getSelected 的调用 。 当前视窗是指那个包含了发起调用的页面的视窗，不管它是不是最顶层视窗。

在背景页这个例子中 ，当前视窗就是最后一个活动视窗。在某些情况下，背景页可能没有当前视窗。

## 范例

你可以在[examples/api/windows](http://src.chromium.org/viewvc/chrome/trunk/src/chrome/common/extensions/docs/examples/api/windows/) 目录下找到一些使用 windows 模块的简单范例。另外一个范例是在[tabs_api.html](http://src.chromium.org/viewvc/chrome/trunk/src/chrome/common/extensions/docs/examples/api/tabs/inspector/tabs_api.html?content-type=text/plain)文件中的[检查器](http://src.chromium.org/viewvc/chrome/trunk/src/chrome/common/extensions/docs/examples/api/tabs/inspector/)范例。 对于其他的例子和查看源代码的帮助，参见示例 。

## API 参考: chrome.windows

### 属性

#### WINDOW_ID_NONE

chrome.windows.WINDOW_ID_NONE

`WINDOW_ID_NONE`*( optional enumerated Type array of 整数 )*

Undocumented.

这个 windowId 值表示没有 Chrome 浏览器窗口的情况。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

### 方法

#### create

void chrome.windows.create(, object `createData`, function `callback`)

Undocumented.

使用任何可选大小、位置或者默认提供的 URL 来创建（打开）一个新的浏览器。

#### 参数

`createData`*( optional enumerated Type array of object 可选，对象 )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`url`*( optional enumerated Type array of string or array of string 可选，字符串或者字符串数组)*

Undocumented.

一个或者一组在视窗作为标签打开的 URL。完全合格的 URL 必须包括一个类型（即'[`www.google.com'，不是'www.google.com'）。相对 URL 将与扩展内的当前页相关。默认为新的标签页面。`](http://www.google.com'，不是'www.google.com'）。相对 URL 将与扩展内的当前页相关。默认为新的标签页面。)

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`tabId`*( optional enumerated Type array of integer 可选，整数 )*

Undocumented.

你想要在新视窗选定的标签的 id。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`left`*( optional enumerated Type array of integer 可选，整数 )*

Undocumented.

新视窗相对于屏幕的左边缘的位置的像素值。如果没有指定，那么新的视窗从最后一个有焦点的视窗自然偏移。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`top`*( optional enumerated Type array of integer 可选，整数 )*

Undocumented.

新视窗相对于屏幕的上边缘的位置的像素值。如果没有指定，那么新的视窗从最后一个有焦点的视窗自然偏移。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`width`*( optional enumerated Type array of integer 可选，整数 )*

Undocumented.

新视窗的像素宽度。如果没有指定，默认为自然宽度。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`height`*( optional enumerated Type array of integer 可选，整数 )*

Undocumented.

新视窗的像素高度。如果没有指定，默认为自然高度。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`incognito`*( optional enumerated Type array of boolean 可选，Boolean 类型 )*

Undocumented.

新视窗是否是隐身。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`type`*( optional enumerated Type array of string ["normal", "popup"]可选，枚举字符串["normal", "popup"] )*

Undocumented.

指定新建浏览器视窗的类型。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function 可选，函数 )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

The callback *parameter* should specify a function that looks like this:

如果指定了回调参数，它应该指定一个如下所示函数：

```js
function(Window window) {...}; 
```

`window`*( optional enumerated Window 可选，视窗 array of paramType )*

Undocumented.

包含新创建视窗的详细信息。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### get

void chrome.windows.get(, integer `windowId`, function `callback`)

Undocumented.

获取有关窗口的详细信息。

#### 参数

`windowId`*( optional enumerated Type array of integer 整数 )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function 函数 )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### Callback function

如果指定了回调参数，它应该指定一个如下所示函数：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Window window) {...}; 
```

`window`*( optional enumerated Window array of paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### getAll

void chrome.windows.getAll(, object `getInfo`, function `callback`)

Undocumented.

获得所有的视窗。

#### 参数

`getInfo`*( optional enumerated Type array of object 可选，对象 )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`populate`*( optional enumerated Type array of boolean 可选，Boolean 类型)*

Undocumented.

如果是 true 表示每个视窗对象都有一个包含该视窗所有标签的 tabs 属性。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function 函数 )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

回调参数应该指定一个如下函数：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(array of Window windows) {...}; 
```

`windows`*( optional enumerated Type array of Window array of paramType paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### getCurrent

void chrome.windows.getCurrent(, function `callback`)

Undocumented.

获得当前视窗。

#### 参数

`callback`*( optional enumerated Type array of function 函数)*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

如果指定了回调参数，它应该指定一个如下所示函数：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Window window) {...}; 
```

`window`*( optional enumerated Window array of paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### getLastFocused

void chrome.windows.getLastFocused(, function `callback`)

Undocumented.

获取最近有焦点的视窗 — 一般是最顶层的视窗。

#### 参数

`callback`*( optional enumerated Type array of function 函数)*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

如果指定了回调参数，它应该指定一个如下所示函数：

If you specify the *callback* parameter, it should specify a function that looks like this:

```js
function(Window window) {...}; 
```

`window`*( optional enumerated Window array of paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### remove

void chrome.windows.remove(, integer `windowId`, function `callback`)

Undocumented.

关闭一个视窗以及其包含的所有标签。

#### 参数

`windowId`*( optional enumerated Type array of integer 整数 )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function 可选，函数 )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

The callback *parameter* should specify a function that looks like this:

如果指定了回调参数，它应该指定一个如下所示函数：

```js
function() {...}; 
```

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### update

void chrome.windows.update(, integer `windowId`, object `updateInfo`, function `callback`)

Undocumented.

更新一个视窗的属性。只指定那些你希望修改的属性，未指定的属性将保持不变。

#### 参数

`windowId`*( optional enumerated Type array of integer 整数 )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`updateInfo`*( optional enumerated Type array of object 对象 )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`left`*( optional enumerated Type array of integer 可选，整数 )*

Undocumented.

视窗相对屏幕左边界进行移动的像素偏移值。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`top`*( optional enumerated Type array of integer 可选，整数 )*

Undocumented.

视窗相对屏幕上边界进行移动的像素偏移值。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`width`*( optional enumerated Type array of integer 可选，整数 )*

Undocumented.

视窗宽度调整的像素值。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`height`*( optional enumerated Type array of integer 可选，整数 )*

Undocumented.

视窗高度调整的像素值。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`focused`*( optional enumerated Type array of boolean 可选，Boolean 类型 )*

Undocumented.

如果是 true，将该视窗提至前面。否则，将 z-order 上下一视窗提至前面。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`callback`*( optional enumerated Type array of function 可选，函数)*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### Returns

#### 回调函数

The callback *parameter* should specify a function that looks like this:

如果指定了回调参数，它应该指定一个如下所示函数：

```js
function(Window window) {...}; 
```

`window`*( optional enumerated Window array of paramType )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

This function was added in version . If you require this function, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

### 事件

#### onCreated

chrome.windows.onCreated.addListener(function(Window window) {...});

Undocumented.

当一个新视窗被创建时触发。

#### 参数

`window`*( optional enumerated Window array of paramType )*

Undocumented.

被创建窗体的详细信息。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### onFocusChanged

chrome.windows.onFocusChanged.addListener(function(integer windowId) {...});

Undocumented.

当前获得焦点窗口改变时触发。Will be chrome.windows.WINDOW_ID_NONE if all chrome windows have lost focus. Note: On some Linux window managers, WINDOW_ID_NONE will always be sent immediately preceding a switch from one chrome window to another.

#### Parameters

`windowId`*( optional enumerated Type array of integer )*

Undocumented.

ID of the newly focused window.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

#### onRemoved

chrome.windows.onRemoved.addListener(function(integer windowId) {...});

Undocumented.

当一个视窗被关闭时触发。

#### 参数

`windowId`*( optional enumerated Type array of integer 整数)*

Undocumented.

被关闭视窗的 ID。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

### 类型

#### Window

`paramName`*( optional enumerated Type array of object 视窗，对象 )*

Undocumented.

Description of this parameter from the json schema.

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`id`*( optional enumerated Type array of integer 整数)*

Undocumented.

视窗的 ID。视窗 ID 在一个浏览器会话中是唯一的。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`focused`*( optional enumerated Type array of boolean )*

Undocumented.

该窗口是否当前焦点窗口。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`top`*( optional enumerated Type array of integer*整数 *)*

Undocumented.

窗体相对屏幕上边缘的偏移像素值。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`left`*( optional enumerated Type array of integer*整数 *)*

Undocumented.

窗体相对屏幕左边缘的偏移像素值。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`width`*( optional enumerated Type array of integer*整数 *)*

Undocumented.

窗体宽度像素值。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`height`*( optional enumerated Type array of integer*整数 *)*

Undocumented.

窗体高度像素值。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`tabs`*( optional enumerated Type array of Tab 可选，标签数组 array of paramType paramType )*

Undocumented.

表征窗体所包含标签的数组。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`incognito`*( optional enumerated Type array of boolean )*

Undocumented.

窗体是否隐藏。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.

`type`*( optional enumerated Type array of string ["normal", "popup", "app"] )*

Undocumented.

浏览器视窗类型。

This parameter was added in version . You must omit this parameter in earlier versions, and you may omit it in any version. If you require this parameter, the manifest key minimum_chrome_version can ensure that your extension won't be run in an earlier browser version.