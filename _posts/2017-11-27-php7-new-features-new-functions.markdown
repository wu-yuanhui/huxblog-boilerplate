---

layout:     post
title:      "PHP7新特性系列 - 新函数"
subtitle:   "来一起学习PHP7吧~"
date:       2017-11-27 22:00:00
author:     "伍源辉"
header-img: "img/2017-11-26.jpg"
tags:
    - PHP7
    - 新特性
    - 函数
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

## 新函数

#### int intdiv ( int $dividend , int $divisor )

说明：对除法结果取整。
异常：
 - DivisionByZeroError （除数为0时）
 - ArithmeticError （被除数是 PHP_INT_MIN 并且 除数是 -1 时）

示例：

```
<?php
var_dump(intdiv(3, 2));
```

> 跟 floor() 函数的作用差不多，区别是 intdiv() 参数和返回值都是 int 类型，而 floor() 参数和返回值都是 float 类型。

#### preg_replace_callback_array()

说明：使用 [正则 => 回调函数] 形式的数组对参数进行搜索替换。
返回值：array | string | NULL

示例：

```
<?php
$subject = 'Aaaaaa Bbb';

preg_replace_callback_array(
    [
        '~[a]+~i' => function ($match) {
            echo strlen($match[0]), ' matches for "a" found', PHP_EOL;
        },
        '~[b]+~i' => function ($match) {
            echo strlen($match[0]), ' matches for "b" found', PHP_EOL;
        }
    ],
    $subject
);
```

#### string random_bytes ( int $length )

说明：生成一串指定长度的适合用于密码的随机字符串。
异常：
 - Exception （无随机来源时）
 - TypeError （传入错误参数时）
 - Error （传入错误长度时）

示例：

```
<?php
$bytes = random_bytes(5);
var_dump(bin2hex($bytes));
```


#### int random_int ( int $min , int $max )

说明：生成一串指定长度的适合用于密码的随机整形。
异常：
 - Exception （无随机来源时）
 - TypeError （传入错误参数时）
 - Error （max 小于 min 时）

示例：

```
<?php
var_dump(random_int(100, 999));
var_dump(random_int(-1000, 0));
```

