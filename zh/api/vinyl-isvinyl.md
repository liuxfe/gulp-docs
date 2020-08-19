<!-- front-matter
id: vinyl-isvinyl
title: Gulp API Vinyl.isVinyl()方法
hide_title: true
sidebar_label: Vinyl.isVinyl()方法
-->

# Vinyl.isVinyl()方法

检测一个对象（object）是否是一个 Vinyl 实例。不要使用 `instanceof` 方法。

**注意：**此方法使用了 Vinyl 的一个内部属性，而这个属性在老版本的 Vinyl 中是不存在的，如果你使用的恰好时老版本，则会得到一个 fasle 结果。

## 用法(Usage)

```js
const Vinyl = require('vinyl');

const file = new Vinyl();
const notAFile = {};

Vinyl.isVinyl(file) === true;
Vinyl.isVinyl(notAFile) === false;
```
<!-- ads -->

## 原型(Signature)

```js
Vinyl.isVinyl(file);
```

### 参数(Parameters)

| 参数 | 类型 | 说明 |
|:--------------:|:------:|-------|
| file | object | 需要检查的对象 |

### 返回(Returns)

如果 `file` 对象是 Vinyl 实例则返回 true。
