# 在 htc 某些机型下 seajs 加载 css 未触发 onload 回调

hi，玉伯，我在开发一个 webapp 时遇到一个问题，初步找到重现的方法是在 js 模块里 require 一个 css，而 css 加载完成的回调未执行，导致依赖这个 css 的 js 的 onload 也未执行，我的测试机型是 HTC-T328d，浏览器为手机自带的，userAgent 为：
Mozilla/5.0(Linux;U;Android4.0.3;zh-cn;HTC-T328d/1.67.1401.3) AndroidWebKit/534.30(KHTML,Like Gecko) Version/4.0 Mobile Safari/534.30

深入到 seajs 源码中继续定位，发现这种机型有两个问题：
1 supportOnload = ‘onload’ in node 返回 true，但是通过创建 link 标签加载 css 却无法触发 onload
2 ua 中没有 AppleWebkit，而是 AndroidWebkit，导致 seajs 判断是否为老版本的 webkit 时错误
var isOldWebKit = +navigator.userAgent
.replace(/.*AppleWebKit\/(\d+)..*/, "$1") < 536

之后导致 seajs 在 addOnload 方法中错误的进入了 supportonload 的分支
if (isCSS && (isOldWebKit || !supportOnload)) {
setTimeout(function() {
pollCss(node, callback)
}, 1) // Begin after node insertion
return
}

而在这款手机上安装的 UC 浏览器里其 ua 为 AppleWebkit/530+ ,这个也导致 seajs 判断 isOldWebKit 时错误

修改判断 isOldWebKit 的正则为/.*(?:AppleWebKit|AndroidWebKit)\/(\d+).*/后正常（其实是把 AndroidWebkit 低于 536 的也视为旧版本的 webkit，同时去掉了版本号后一定带小数点的限制），但是不知道这样改会不会造成其他问题