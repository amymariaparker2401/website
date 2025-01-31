# ✨ 生产环境\(Production\)

当需要绑定应用程序的时候，你可以使用 Parcel 的生产模式。

```bash
parcel build entry.js
```

这将关闭监听模式和热模块替换，所以它只会编译一次。它还会开启 minifier 来减少输出包文件的大小。Parcel 使用的 minifiers 有 JavaScript 的 [terser](https://github.com/fabiosantoscode/terser) ，CSS 的 [cssnano](http://cssnano.co) 还有 HTML 的 [htmlnano](https://github.com/posthtml/htmlnano)。

启动生产模式还要设置环境变量 `NODE_ENV=production` 。像 React 这种只用开发调试功能的大型库，通过设置这个环境变量来禁用调试功能，从而构建得更小更快。

