<!-- front-matter
id: explaining-globs
title: Globs详解
hide_title: true
sidebar_label: Globs详解
-->

# Globs详解

glob 是由普通字符和(或)通配字符组成的字符串，用于匹配文件路径。可以利用一个或多个 glob 在文件系统中定位文件。

`src()` 方法接受一个 glob 字符串或由多个 glob 字符串组成的数组作为参数，用于确定哪些文件需要被操作。glob 或 glob 数组必须至少匹配到一个匹配项，否则 src() 将报错。当使用 glob 数组时，将按照每个 glob 在数组中的位置依次执行匹配 - 这尤其对于取反（negative） glob 有用。

## 字符串片段与分隔符

字符串片段（segment）是指两个分隔符之间的所有字符组成的字符串。在 glob 中，分隔符永远是 `/` 字符(不区分操作系统，即便是在采用 `\\` 作为分隔符的 Windows 操作系统中)。在 glob 中，`\\` 字符被保留作为转义符使用。

如下， * 被转义了，因此，* 将被作为一个普通字符使用，而不再是通配符了。
```js
'glob_with_uncommon_\\*_character.js'
```

避免使用 Node 的 `path` 类方法来创建 glob，例如 `path.join`。在 Windows 中，由于 Node 使用 `\\` 作为路径分隔符，因此将会产生一个无效的 glob。还要避免使用 `__dirname` 和 `__filename` 全局变量，由于同样的原因，`process.cwd()` 方法也要避免使用

```js
const invalidGlob = path.join(__dirname, 'src/*.js');
```
<!-- ads -->

## 特殊字符： * (一个星号)

在一个字符串片段中匹配任意数量的字符，包括零个匹配。对于匹配单级目录下的文件很有用。

下面这个 glob 能够匹配类似 `index.js` 的文件，但是不能匹配类似 `scripts/index.js` 或 `scripts/nested/index.js` 的文件。
```js
'*.js'
```

## 特殊字符： ** (两个星号)

在多个字符串片段中匹配任意数量的字符，包括零个匹配。 对于匹配嵌套目录下的文件很有用。请确保适当地限制带有两个星号的 glob 的使用，以避免匹配大量不必要的目录。

下面这个 glob 被适当地限制在 `scripts/` 目录下。它将匹配类似 `scripts/index.js`、`scripts/nested/index.js` 和 `scripts/nested/twice/index.js` 的文件。

```js
'scripts/**/*.js'
```

<small>在上面的示例中，如果没有 `scripts/` 这个前缀做限制，`node_modules` 目录下的所有目录或其他目录也都将被匹配</small>

## 特殊字符： ! (取反)

由于 glob 匹配时是按照每个 glob 在数组中的位置依次进行匹配操作的，所以 glob 数组中的取反（negative）glob 必须跟在一个非取反（non-negative）的 glob 后面。第一个 glob 匹配到一组匹配项，然后后面的取反 glob 删除这些匹配项中的一部分。如果取反 glob 只是由普通字符组成的字符串，则执行效率是最高的。

```js
['scripts/**/*.js', '!scripts/vendor/**']
```

如果任何非取反（non-negative）的 glob 跟随着一个取反（negative） glob，任何匹配项都不会被删除。

```js
['scripts/**/*.js', '!scripts/vendor/**', 'scripts/vendor/react.js']
```

取反（negative） glob 可以作为对带有两个星号的 glob 的限制手段。

```js
['**/*.js', '!node_modules/**']
```

<small>在上面的示例中，如果取反（negative）glob 是 `!node_modules/**/*.js`，那么各匹配项都必须与取反 glob 进行比较，这将导致执行速度极慢。如果要排除目录下的所有文件，只需要在目录名后添加`/**`即可</small>
<!-- ads -->

<span id="overlapping-globs"></span>
## 匹配重叠（Overlapping globs）

两个或多个 glob 故意或无意匹配了相同的文件就被认为是匹配重叠（overlapping）了。如果在同一个 `src()` 中使用了会产生匹配重叠的 glob，gulp 将尽力去除重叠部分，但是在多个 `src()` 调用时产生的匹配重叠是不会被去重的。

## Advanced resources

关于如何在 gulp 中使用 glob 的知识都已经在在上面的文档中讲解了。如果你还希望获取更多进阶资料，请参考下面列出的部分：

* [Micromatch Documentation][micromatch-docs]
* [node-glob's Glob Primer][glob-primer-docs]
* [Begin's Globbing Documentation][begin-globbing-docs]
* [Wikipedia's Glob Page][wikipedia-glob]

[micromatch-docs]: https://github.com/micromatch/micromatch
[glob-primer-docs]: https://github.com/isaacs/node-glob#glob-primer
[begin-globbing-docs]: https://github.com/begin/globbing#what-is-globbing
[wikipedia-glob]: https://en.wikipedia.org/wiki/Glob_(programming)
