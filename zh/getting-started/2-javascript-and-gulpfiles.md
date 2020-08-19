<!-- front-matter
id: javascript-and-gulpfiles
title: JavaScript 和 Gulpfiles
hide_title: true
sidebar_label: JavaScript 和 Gulpfiles
-->

# JavaScript 和 Gulpfiles

Gulp 允许你使用现有 JavaScript 知识来书写 gulpfile 文件，或者利用你所掌握的 gulpfile 经验来书写普通的 JavaScript 代码。虽然gulp 提供了一些实用工具来简化文件系统和命令行的操作，但是你所编写的其他代码都是纯 JavaScript 代码。

## Gulpfile 详解

gulpfile 是项目目录下名为 `gulpfile.js` （或者首字母大写 `Gulpfile.js`，就像 `Makefile` 一样命名）的文件，在运行 gulp 命令时会被自动加载。在这个文件中，你经常会看到类似 `src()`、`dest()`、`series()` 或 `parallel()` 函数之类的 gulp API，除此之外，纯 JavaScript 代码或 Node 模块也会被使用。任何导出（export）的函数都将注册到 gulp 的任务（task）系统中。

## Gulpfile 转译

你可以使用需要转译的编程语言来书写 gulpfile 文件，例如 TypeScript 或 Babel，通过修改 gulpfile.js 文件的扩展名来表明所用的编程语言并安装对应的转译模块。

* 对于 TypeScript，重命名为 `gulpfile.ts` 并安装 [ts-node][ts-node-module] 模块
* 对于 Babel，重命名为 `gulpfile.babel.js` 并安装 [@babel/register][babel-register-module] 模块。

__Most new versions of node support most features that TypeScript or Babel provide, except the `import`/`export` syntax. When only that syntax is desired, rename to `gulpfile.esm.js` and install the [esm][esm-module] module.__

针对此功能的高级知识和已支持的扩展名的完整列表，请参考 [gulpfile 转译][gulpfile-transpilation-advanced] 文档。


##  Gulpfile 分割

大部分用户起初是将所有业务逻辑都写到一个 gulpfile 文件中。随着文件的变大，可以将此文件重构为数个独立的文件。

每个任务（task）可以被分割为独立的文件，然后导入（import）到 gulpfile 文件中并组合。这不仅使事情变得井然有序，而且可以对每个任务（task）进行单独测试，或者根据条件改变组合。

Node 的模块解析功能允许你将 `gulpfile.js` 文件替换为同样命名为 `gulpfile.js` 的目录，该目录中包含了一个名为 `index.js` 的文件，该文件被当作 `gulpfile.js`使用。并且，该目录中还可以包含各个独立的任务（task）模块。

[gulpfile-transpilation-advanced]: ../documentation-missing.md
[ts-node-module]: https://www.npmjs.com/package/ts-node
[babel-register-module]: https://www.npmjs.com/package/@babel/register
[esm-module]: https://www.npmjs.com/package/esm
