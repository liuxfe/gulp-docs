<!-- front-matter
id: registry
title: Gulp API registry()方法
hide_title: true
sidebar_label: registry()方法
-->

# registry()方法

允许将自定义的注册表插入到任务系统中，以期提供共享任务或增强功能。

**注意：** 只有用 `task()` 方法注册的任务才会进入自定义注册表中。直接传递给 `series()` 或 `parallel()` 的任务函数（task functions）不会进入自定义任务注册表 - 如果你需要自定义注册表的行为，请通过字符串引用的方式将任务（task）组合在一起。

分配新注册表时，将传输当前注册表中的每个任务，并将用新注册表替换当前注册表。这允许按顺序添加多个自定义注册表。

有关详细信息，请参考 [创建自定义注册表][creating-custom-registries] 。



## 用法(Usage)

```js
const { registry, task, series } = require('gulp');
const FwdRef = require('undertaker-forward-reference');

registry(FwdRef());

task('default', series('forward-ref'));

task('forward-ref', function(cb) {
  // body omitted
  cb();
});
```

## 原型(Signature)

```js
registry([registryInstance])
```

### 参数(Parameters)

| 参数 | 类型 | 说明 |
|:--------------:|:-----:|--------|
| registryInstance | object | 自定义注册表的实例(而不是类)。 |

### 返回(Returns)

如果传递了 `registryInstance`，则不会返回任何内容。如果没有传递参数，则返回当前注册表实例。

### 错误(Errors)

当一个构造函数(而不是一个实例)作为 `registryInstance` 传递时，抛出一个错误，并提示 "Custom registries must be instantiated, but it looks like you passed a constructor"（必须实例化自定义注册表，但它看起来像您传递了一个构造函数）。

当传入的 `registryInstance` 没有 `get` 方法时，将抛出一个错误，提示 "Custom registry must have `get` function"。

当传入的 `registryInstance` 没有 `set` 方法时，将抛出一个错误，提示 "Custom registry must have `set` function"。

当传入的 `registryInstance` 没有 `init` 方法时，将抛出一个错误，提示 "Custom registry must have `init` function"。

当传入的 `registryInstance` 没有 `tasks` 方法时，将抛出一个错误，提示 "Custom registry must have `tasks` function"。

[creating-custom-registries]: ../documentation-missing.md
