---
title: 【PHP】useを使う場面
date: 2021-05-20 01:18:52
tags:
- PHP
---
# 目次
<!-- toc -->
<!-- more -->

# 1. クロージャ
クロージャでuseを使用する場合、クロージャの外で定義された変数をクロージャ内に引き継ぐときに使用される

$eを呼ぶとHTMLの改行文字を付加してechoをするサンプル
```php
$eol = '<br>';

//  １行前で定義した改行文字をクロージャ内で使用する
$e = function($message) use ($eol){
  echo $message,$eol;
};

$e('TEST');
```

# 2. トレイト
コピーアンドペーストして使用しているような汎用的なメソッドを`trait`というクラスのようなものに括りだしていろいろなところで使おうというもの

トレイトを使用したいクラスで`use トレイト名`として使用する

注意 : トレイトは密結合になるので、オブジェクト指向的には使用しないほうがいい

```php
trait test
{
  private function echoTest()
  {
    echo 'test';
  }
}

class main
{
  use test;

  public function __construct()
  {
    $this->echoTest();
  }
}

$m = new main();
```

# 3. 使用するnamespaceのインポート
事前に`use 名前空間の完全修飾名\クラス名`を定義しておくことで、別のnamespaceにあるクラスをnew(インスタンス化)するときに、名前空間を繰り返し書かなくていいようにする

## useを使用しない場合
名前空間 : MyApp\Controller\Test
クラス名 : TestController
```php
//  インスタンス化する
$testController = new MyApp\Controller\Test\TestController();
```

## useを使用している場合
名前空間 : MyApp\Controller\Test
クラス名 : TestController
```php
//  ネームスペースのインポート
use MyApp\Controller\Test\TestController;

//  インスタンス化する
$testController = new TestController();
```
