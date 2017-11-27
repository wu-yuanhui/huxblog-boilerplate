---

layout:     post
title:      "PHP7新特性系列 - 组合比较符"
subtitle:   "来一起学习PHP7吧~"
date:       2017-11-27 20:00:00
author:     "伍源辉"
header-img: "img/2017-11-26.jpg"
tags:
    - PHP7
    - 新特性
    - 组合比较符
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

## 组合比较符

使用：$a <=> $b

说明：
 - $a < $b 返回 -1
 - $a = $b 返回 0
 - $a > $b 返回 1

示例：

```
<?php
// 整数
echo 1 <=> 1; // 0
echo 1 <=> 2; // -1
echo 2 <=> 1; // 1

// 浮点数
echo 1.5 <=> 1.5; // 0
echo 1.5 <=> 2.5; // -1
echo 2.5 <=> 1.5; // 1
 
// 字符串
echo "a" <=> "a"; // 0
echo "a" <=> "b"; // -1
echo "b" <=> "a"; // 1

```


#### 使用 PHP 函数对变量 $x 进行比较

| 表达式 | gettype() | empty() | is_null() | isset() | boolean : if($x) |
| - | - | - | - | - | - |
| $x = ""; | string | TRUE | FALSE | TRUE | FALSE |
| $x = null; | NULL | TRUE | TRUE | FALSE | FALSE |
| var $x; | NULL | TRUE | TRUE | FALSE | FALSE |
| $x is undefined | NULL | TRUE | TRUE | FALSE | FALSE |
| $x = array(); | array | TRUE | FALSE | TRUE | FALSE |
| $x = false; | boolean | TRUE | FALSE | TRUE | FALSE |
| $x = true; | boolean | FALSE | FALSE | TRUE | TRUE |
| $x = 1; | integer | FALSE | FALSE | TRUE | TRUE |
| $x = 42; | integer | FALSE | FALSE | TRUE | TRUE |
| $x = 0; | integer | TRUE | FALSE | TRUE | FALSE |
| $x = -1; | integer | FALSE | FALSE | TRUE | TRUE |
| $x = "1"; | string | FALSE | FALSE | TRUE | TRUE |
| $x = "0"; | string | TRUE | FALSE | TRUE | FALSE |
| $x = "-1"; | string | FALSE | FALSE | TRUE | TRUE |
| $x = "php"; | string | FALSE | FALSE | TRUE | TRUE |
| $x = "true"; | string | FALSE | FALSE | TRUE | TRUE |
| $x = "false"; | string | FALSE | FALSE | TRUE | TRUE |

#### 松散比较 ==

| 值 | TRUE | FALSE | 1 | 0 | -1 | "1" | "0" | "-1" | NULL | array() | "php" | "" |
| - | - | - | - | - | - | - | - | - | - | - | - | - |
| TRUE | TRUE | FALSE | TRUE | FALSE | TRUE | TRUE | FALSE | TRUE | FALSE | FALSE | TRUE | FALSE |
| FALSE | FALSE | TRUE | FALSE | TRUE | FALSE | FALSE | TRUE | FALSE | TRUE | TRUE | FALSE | TRUE |
| 1 | TRUE | FALSE | TRUE | FALSE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE |
| 0 | FALSE | TRUE | FALSE | TRUE | FALSE | FALSE | TRUE | FALSE | TRUE | FALSE | TRUE | TRUE |
| -1 | TRUE | FALSE | FALSE | FALSE | TRUE | FALSE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE |
| "1" | TRUE | FALSE | TRUE | FALSE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE |
| "0" | FALSE | TRUE | FALSE | TRUE | FALSE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE | FALSE |
| "-1" | TRUE | FALSE | FALSE | FALSE | TRUE | FALSE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE |
| NULL | FALSE | TRUE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE | TRUE | TRUE | FALSE | TRUE |
| array() | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | TRUE | TRUE | FALSE | FALSE |
| "php" | TRUE | FALSE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | TRUE | FALSE |
| "" | FALSE | TRUE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE | TRUE | FALSE | FALSE | TRUE |

#### 严格比较 ===

| 值 | TRUE | FALSE | 1 | 0 | -1 | "1" | "0" | "-1" | NULL | array() | "php" | "" |
| TRUE | TRUE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE |
| FALSE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE |
| 1 | FALSE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE |
| 0 | FALSE | FALSE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE |
| -1 | FALSE | FALSE | FALSE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE |
| "1" | FALSE | FALSE | FALSE | FALSE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE |
| "0" | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE | FALSE |
| "-1" | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | TRUE | FALSE | FALSE | FALSE | FALSE |
| NULL | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | TRUE | FALSE | FALSE | FALSE |
| array() | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | TRUE | FALSE | FALSE |
| "php" | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | TRUE | FALSE |
| "" | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | FALSE | TRUE |

