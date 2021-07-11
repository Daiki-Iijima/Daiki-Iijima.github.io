---
title: 【PHP】クラスのマジックメソッド一覧
date: 2021-06-05 14:23:27
tags:
- PHP
---
# 目次
<!-- toc -->
<!-- more -->

# 一覧
使うことが多いのは、`__construct`,`__toString`あたり

| 関数名                    | 呼ばれるタイミング                               | 
|------------------------|-----------------------------------------| 
| __construct            | インスタンスの生成時                              | 
| __destruct             | インスタンスが破棄される or exit命令が呼ばれたとき           | 
| __call                 | アクセス不能メソッドが呼び出されたとき                     | 
| __callStatic           | アクセス不能静的メソッドが呼び出されたとき                   | 
| __get                  | アクセス不能プロパティにアクセスされたとき                   | 
| __set                  | アクセス不能プロパティに値を代入されたとき                   | 
| __isset                | アクセス不能プロパティがisset関数またはempty関数の引数に渡されたとき | 
| __unset                | アクセス不能プロパティがunset関数の引数で指定されたとき          | 
| __sleep,__serialize    | serializeの実行前                           | 
| __wakeup,__unserialize | serializeの実行後                           | 
| __toString             | インスタンスの出力時                              | 
| __invoke               | インスタンスを関数として呼び出したとき                     | 
| __set_state            | インスタンスがvar_export関数の引数に指定されたとき          | 
| __clone                | cloneキーワードでインスタンスのクローンを作成するとき           | 
| __debugInfo            | インスタンスがvar_dump関数の引数に指定されたとき            | 

# 使用例
コンストラクタとechoで呼ばれた場合の処理を実装したクラス`Test`を作成

```php
<?php
class Test
{
  public function __construct()
  {
    //  コンストラクタ
  }

  public function __toString()
  {
    //  echo Testインスタンス;
    //  が呼ばれたときに呼ばれる
    //  return 文字列
  }
}
```
