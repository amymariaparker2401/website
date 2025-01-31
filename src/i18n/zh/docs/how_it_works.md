# 🛠 它如何运作

Parcel 将 **资源** 树转换成 **bundle** 树。许多其它的打包工具基本上是基于 JavaScript 资源，还有附加在其上的其它格式的资源。例如，在 JS 文件中内联成字符串。 Parcel 是对文件类型无感知的，它能按你所期待的方式那样与任意类型的资源工作，且毋须配置。Parcel 的打包流程共有三个步骤。

## 1. 构建资源树

Parcel 接受单个入口资源作为输入，可以是任意类型：一个 JS 文件、HTML、CSS 和图片等等。有许多不同的[资源类型](https://github.com/amymariaparker2401/website/tree/574adba7f88c1181c822d553056158f78247bbe7/src/i18n/zh/docs/asset_types.html)在 Parcel 中被定义，它知道如何去处理特定的文件类型。资源会被解析，资源的依赖会被提取，资源会被转换成最终编译好的形态。此过程创建了一个资源树。

## 2. 构建 bundle 树

一旦资源树被构建好，资源会被放置在 bundle 树中。首先一个入口资源会被创建成一个 bundle，然后动态的 `import()` 会被创建成子 bundle ，这引发了代码的拆分。

当不同类型的文件资源被引入，兄弟 bundle 就会被创建。例如你在 JavaScript 中引入了 CSS 文件，那它会被放置在一个与 JavaScript 文件对应的兄弟 bundle 中。

如果资源被多于一个 bundle 引用，它会被提升到 bundle 树中最近的公共祖先中，这样该资源就不会被多次打包。

## 3. 打包

在 bundle 树被构建之后，每个 bundle 都会被 [packager](https://github.com/amymariaparker2401/website/tree/574adba7f88c1181c822d553056158f78247bbe7/src/i18n/zh/docs/packagers.html) 写到一个特定文件类型的文件中。packagers 知道如何从每个资源中将代码合并起来，生成到最终被浏览器加载的文件中。

