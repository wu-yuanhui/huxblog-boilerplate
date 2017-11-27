---

layout:     post
title:      "PHP7新特性系列 - use 分组声明"
subtitle:   "来一起学习PHP7吧~"
date:       2017-11-27 21:00:00
author:     "伍源辉"
header-img: "img/2017-11-26.jpg"
tags:
    - PHP7
    - 新特性
    - use
    - new features

---

## 前言

从下面的表格可以看到，PHP 目前的最新稳定版本是 PHP 7.1。PHP 7 相对于 PHP 5.x 版本增加了大量的新特性，并且重写了大部分的 PHP 引擎，使得 PHP 的运行速度有了极大的提升。

而 PHP 5.6 以下的版本已经不再提供安全更新支持，PHP 5.6.* 版本虽然应用还十分广泛，但也不再提供主流更新支持，目前仅提供安全更新支持，而且也时日不多了（剩下一年左右）。

综上所述，学习和升级 PHP 7 是大势所趋，而且 PHP 7 做了向下兼容支持，正常的升级不会造成太大的影响。

| 版本 | 发布时间 | 主流支持 | 安全支持 |
| - | - | - | - |
| 5.6 * | 2014-08-28 | 2017-01-19 | 2018-12-31 |
| 7.0 | 2015-12-03 | 2017-12-03 | 2018-12-03 |
| 7.1 | 2016-12-01 | 2018-12-01 | 2019-12-01 |

---

## use 分组声明

说明：在同一命名空间下的类、函数和常量可以通过单个 use 语句一次性导入。

示例：

```
// PHP 7 之前的代码
use some\namespace\ClassA;
use some\namespace\ClassB;
use some\namespace\ClassC as C;

use function some\namespace\fn_a;
use function some\namespace\fn_b;
use function some\namespace\fn_c;

use const some\namespace\ConstA;
use const some\namespace\ConstB;
use const some\namespace\ConstC;

// PHP 7+ 及更高版本的代码
use some\namespace\{ClassA, ClassB, ClassC as C};
use function some\namespace\{fn_a, fn_b, fn_c};
use const some\namespace\{ConstA, ConstB, ConstC};

```

> 这个特性还是很实用的。