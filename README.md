<!--
    需要填充的占位符：
    
    README.md
    
        龙哥盟 JavaScript 中文文档汇总给：文档中文名
        {nameEn}：文档英文名
        {urlEn}：文档原始链接
        jsdoc：域名前缀
        飞龙：负责人名称
        wizardforcel：负责人 Github 用户名
        562826179：负责人 QQ
        flygon-js-docs-zh：ApacheCN 的 Github 仓库名称
        flygon-js-docs-zh：DockerHub 仓库名称
        flygon-js-docs-zh：PYPI 包名称
        flygon-js-docs-zh：NPM 包名称
    
    CNAME
    
        jsdoc：域名前缀

    index.html
    
        龙哥盟 JavaScript 中文文档汇总给：文档中文名
        #009d9c：显示颜色
        flygon-js-docs-zh：ApacheCN 的 Github 仓库名称

    asset/docsify-flygon-footer.js
    
        flygon-js-docs-zh：ApacheCN 的 Github 仓库名称
-->

# 龙哥盟 JavaScript 中文文档汇总给

> 协议：[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)
> 
> 真相一旦入眼，你就再也无法视而不见。——《黑客帝国》

* [在线阅读](https://jsdoc.flygon.net)

## 下载

### Docker

```js
docker pull apachecn0/flygon-js-docs-zh
docker run -tid -p <port>:80 apachecn0/flygon-js-docs-zh
# 访问 http://localhost:{port} 查看文档
```

### NPM

```js
npm install -g flygon-js-docs-zh
flygon-js-docs-zh <port>
# 访问 http://localhost:{port} 查看文档
```
