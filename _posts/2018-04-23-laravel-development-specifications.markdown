---
layout:     post
title:      "Laravel 开发规范"
subtitle:   "好好写代码"
date:       2018-04-23 11:00:00
author:     "伍源辉"
header-img: "img/home-bg.jpg"
tags:
    - Laravel
    - 开发规范
    - 数据库
    - 事务
    - 异常
---


# 开发规范

## 数据库

### 数据库事务

为避免暴露数据库结构和 SQL 语句，在系统的异常处理类 `Handler.php` 中增加了以下代码：

```php
public function render($request, Exception $exception)
{
    if ($exception instanceof QueryException) {
        $message = 'PDO query error.';
        $status  = empty($exception->getCode()) ? 999 : $exception->getCode();

        return $request->expectsJson()
            ? response()->json([
                'message' => $message,
                'status'  => $status,
                /* 'file'    => $exception->getFile(), */
                /* 'line'    => $exception->getLine(), */
            ])
            : redirect()->back();
    }

    /* ... */
}
```

在系统开发过程中，建议使用 `Closure` 的方式处理数据库事物，会自动捕获异常、回滚及返回错误信息：

```php
use Illuminate\Support\Facades\DB;

DB::transaction(function () {
    DB::table('users')->update(['votes' => 1]);
    DB::table('posts')->delete();
});
```


不建议使用手动操作事务的方式，如需使用，必须先对 `QueryException` 进行处理后再返回错误信息：

```php
DB::beginTransaction();
try {
    DB::table('users')->update(['votes' => 1]);
    DB::table('posts')->delete();
    DB::commit();
} catch(\Illuminate\Database\QueryException $e) {
    /* 此处不能直接通过 $e->getMessage() 抛出 AppException() 异常， */
    /* 必须先处理错误信息后再抛出，避免暴露数据库结构和 SQL 语句。 */
    
    DB::rollback();
    /* do something... */
} catch (\Throwable $t) {
    DB::rollback();
    throw new AppException($t->getMessage());
}
```

> * 注意，`DB::beginTransaction();` 需要放置于 `try` 代码块**外部**。
> * 另外，在 `catch` 代码块中无需使用 `\Log::info();` 等方式记录日志，系统底层已经自行记录。
