# Detect methods

## Detect module

该检测方法可以在不同的环境中微调你的站点或者应用程序，并帮助你识别手机和平板；以及不同的浏览器和操作系统。

```
// The following boolean flags are set to true if they apply,
// if not they're either set to `false` or `undefined`.
// We recommend accessing them with `!!` prefixed to coerce to a boolean. 

// general device type
$.os.phone
$.os.tablet

// specific OS
$.os.ios
$.os.android
$.os.webos
$.os.blackberry
$.os.bb10
$.os.rimtabletos

// specific device type
$.os.iphone
$.os.ipad
$.os.ipod // [v1.1]
$.os.touchpad
$.os.kindle

// specific browser
$.browser.chrome
$.browser.firefox
$.browser.safari // [v1.1]
$.browser.webview // (iOS) [v1.1]
$.browser.silk
$.browser.playbook
$.browser.ie // [v1.1]

// 此外，版本信息是可用的。
// 下面是运行??iOS 6.1 的 iPhone 所返回的。
!!$.os.phone         // => true
!!$.os.iphone        // => true
!!$.os.ios           // => true
$.os.version       // => "6.1"
$.browser.version  // => "536.26" 
```