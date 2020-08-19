<!-- front-matter
id: quick-start
title: 快速开始
hide_title: true
sidebar_label: 快速开始
-->

# 快速开始

如果你先前将 gulp 安装到全局环境中了，请执行 `npm rm --global gulp` 将 gulp 删除再继续以下操作。更多信息请参考 Sip。

## 检查 node、npm 和 npx 是否正确安装
```sh
node --version
```
![Output: v8.11.1][img-node-version-command]
```sh
npm --version
```
![Output: 5.6.0][img-npm-version-command]
```sh
npx --version
```
![Output: 9.7.1][img-npx-version-command]

如果上述工具还没安装，请参考 [这里][node-install]。
<!-- ads -->

## 安装 gulp 命令行工具
```sh
npm install --global gulp-cli
```

## 创建项目目录并进入
```sh
npx mkdirp my-project

cd my-project
```

## 在项目目录下创建 package.json 文件
```sh
npm init
```

这条命令将引导你设置项目的名名、版本、描述等信息

## 安装 gulp，作为开发时依赖项
```sh
npm install --save-dev gulp
```

## 检查你的 gulp 版本

```sh
gulp --version
```

确保输出与下面的屏幕截图匹配，否则你可能需要执行本指南中的上述步骤。

![Output: CLI version 2.0.1 & Local version 4.0.0][img-gulp-version-command]

## 创建 gulpfile 文件
利用任何文本编辑器在项目大的根目录下创建一个名为 gulpfile.js 的文件，并在文件中输入以下内容:
```js
function defaultTask(cb) {
  // place code for your default task here
  cb();
}

exports.default = defaultTask
```
<!-- ads -->

## 测试
在项目根目录下执行 gulp 命令:
```sh
gulp
```
如需运行多个任务（task），可以执行 `gulp <task> <othertask>`。

## 输出结果
默认任务（task）将执行，因为任务为空，因此没有实际动作。
![Output: Starting default & Finished default][img-gulp-command]

[sip-article]: https://medium.com/gulpjs/gulp-sips-command-line-interface-e53411d4467
[node-install]: https://nodejs.org/en/
[img-node-version-command]: https://gulpjs.com/img/docs-node-version-command.png
[img-npm-version-command]: https://gulpjs.com/img/docs-npm-version-command.png
[img-npx-version-command]: https://gulpjs.com/img/docs-npx-version-command.png
[img-gulp-version-command]: https://gulpjs.com/img/docs-gulp-version-command.png
[img-gulp-command]: https://gulpjs.com/img/docs-gulp-command.png
