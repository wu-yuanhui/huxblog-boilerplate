---

layout:     post
title:      "《PHP7新特性系列》之返回值类型声明"
subtitle:   "来学习PHP7吧~"
date:       2017-11-27 15:00:00
author:     "伍源辉"
header-img: "img/2017-11-26.jpg"
tags:
    - PHP7
    - 新特性
    - 标量类型声明
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

## 返回值类型声明

#### 两种模式:
- 强制模式 (默认)
- 严格模式

#### 返回值类型：
- PHP 7.0.0 -> string
- PHP 7.0.0 -> int
- PHP 7.0.0 -> float
- PHP 7.0.0 -> bool
- PHP 5.4.0 -> callable
- PHP 5.1.0 -> array
- PHP 5.0.0 -> class
- PHP 5.0.0 -> interface
- PHP 5.0.0 -> self

#### 错误：
- PHP 5 致命错误（可恢复）
- PHP 7 TypeError异常

## 强制模式
行为：强制转换类型

示例：

```
<?php
function sum($a, $b): float {
    return $a + $b;
}

// float(3)
var_dump(sum(1, 2));

```

## 严格模式
声明：declare(strict_types=1);

位置：文件顶部

级别：单文件级

行为：类型完全相符通过，否则抛出TypeError

影响：参数的类型声明，函数的返回值声明

示例：

```
<?php
declare(strict_types=1);

function sum($a, $b): int {
    return $a + $b;
}

try {
    var_dump(sum(1, 2));
    var_dump(sum(1.5, 2.5));
} catch (TypeError $e) {
    echo 'Error: '.$e->getMessage();
}

```
