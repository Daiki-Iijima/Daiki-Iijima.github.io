---
title: 【PHP】基本的な構文
date: 2021-06-06 18:28:16
tags:
- PHP
---
# 目次
<!-- toc -->
<!-- more -->

# この記事の目的
別の言語を触っていて、PHPに戻ってくるとクラスやメソッド、変数などの定義の仕方を忘れているときがあるのでメモとして、見返すことのできるように残しておく

# 変数,定数
## 変数
PHPでは型宣言は必要ないので、リテラルの値によって変数の型が変化する
```php
<?php
$data = "AAA";

echo $data;  //  AAA
```

## 定数
- 定数名は大文字で定義する
- 呼び出すときに変数のように`$`は必要ない
```php
<?php
define('TAX',0.08);

//  呼び出し
echo TAX;  //  0.08
```

# 配列
- PHPの配列は連想配列と同じ
- キーの部分を定義していない場合、0から数値の連番の値が入る
```php
<?php
//  空の配列を定義する
$emptyArray = [];

//  要素のみを登録して定義
$array = ['a','b','c'];

//  要素の追加
$array[] = 'd';

//  キーを指定して、連想配列っぽく定義
$dicArray = ['a'=>10,'b'=>20,'c'=>30];

//  キーを指定して要素を追加
$dicArray['d'] = 40;

//  配列をわかりやすいように表示
print_r($dicArray);

//  Array
//  (
//      [a] => 10
//      [b] => 20
//      [c] => 30
//  )
```

# 構文
## if文
```php
<?php

$data = "a";

if($data === "a"){
  //  処理
}else if($data === "b"){
  //  処理
}else{
  //  どの処理にも当てはまりませんでした
}
```

## for文
```php
<?php
for($i =0;i<100;i++){
  echo $i;
}
```

## foreach文
- C#とは違い、`配列 as 各要素`になる(C#とは順番が逆)

```php
<?php

$array = ['a','b','c'];

//  通常の配列
foreach($array as $data){
  echo $data;  // abc
}

//  連想配列のキーも取得したい場合
foreach($array as $key=>$data){
  echo $key;  // 123
  echo $data;  // abc
}
```

## switch文
```php
<?php

$data = "a";

switch($data){
  case "a":
    // $dataがaのときの処理
  break;
  case "b":
    // $dataがbのときの処理
  break;
  case "c":
    // $dataがcのときの処理
  break;
  default:
    // 上のどのケースにも当てはまらないときの処理
}
```

# 関数関係

## 関数
- 関数名は`小文字`
- 基本は引数の型宣言や戻り地の型宣言をしたほうがいい
```php
<?php

// 一番ベーシックな書き方
// 0を返す
function test($data){
  return $data * 2;
}

//  引数と戻り値の型を定義したバージョン(こっちを使ったほうがわかりやすい)
function test2(int $data):int{
  return $data * 2;
}

// 呼び出し
$value = test2(1);
echo $value;
```

## クロージャー(無名関数)
- 関数を変数として扱う
```php
<?php

// 一番ベーシックな書き方
$func = function (int $data){
  return $data * 2;
}

//  呼び出す
$func(4);
```

## クロージャーを関数の引数に渡す
`callable型`を引数にすることで関数を関数に引き渡せる
```php
<?php
function test(callable $endFunc):void{
  // 処理

  // 処理の終わりにクロージャーの処理をする
  $endFunc();
}
```

# クラス関係

## アクセス修飾子
- punlic
- private
- protected

## クラスの定義
- アッパーキャメル記法で定義する
```php
<?php
class Test
{
  // プロパティやメソッドを記述
}
```

## プロパティ(メンバ変数)
- ローワーキャメル記法で定義する
- PHP7.2以降から、データ型の指定ができる
- 同じクラス内で呼び出す場合`$this->プロパティ名`で呼び出す
```php
<?php
class Test
{
  // 7.2以前までの定義
  public $data1;

  // 7.2以降に使える定義
  public int $data2;

  // 初期値を定義する
  public int $data3 = 1;

  // クラス内のプロパティを呼び出す
  public function printFunc():void{
    echo $this->data;
  }
}
```

## メソッドの定義
- アクセス修飾子がついている以外は、関数と同じ
- アッパーキャメル記法で定義する
```php
<?php
class Test
{
  public function printFunc(int $value):void{
    echo $value;
  }
}
```

## オブジェクト定数の定義
- オブジェクト内固有の定数
- 同じクラス内で呼び出す場合、`self::`を付けて呼び出す
```php
<?php
class Test
{
  public const TAX = 0.08;

  // 同じクラス内での呼び出し例
  public function printConst(int $value):void{
    echo self::TAX;
  }
}
```

## インスタンス化
- `$インスタンス名 = new クラス名()`でインスタンス化する
```php
<?php
class Test
{
  // 処理
}

$instanceTest = new Test();
```

## インスタンスの要素へのアクセス
- プロパティ : `インスタンス名->プロパティ名`
- オブジェクト定数 : `インスタンス名::オブジェクト定数`
- メソッド : `インスタンス名->メソッド名();`

```php
<?php
class Test
{
  public const TAX = 0.08;
  public int $data = 1;

  public function printFunc():void{
    echo $this->data;
  }
}

// インスタンス化
$instanceTest = new Test();

// dataに10を代入
$instanceTest->data = 10;

// 定数を出力
echo $instanceTest::TAX;

// メソッドを呼び出す
$instanceTest->printFunc();
```

# 抽象クラス
- 定義 : `abstract class 抽象クラス名`
	- 抽象メソッドの定義にも`abstract`をつける
	- 抽象メソッドは中身を持たない
- 継承 : `class クラス名 extends 抽象クラス名`

```php
<?php

// 抽象クラスの定義
abstract class Parent
{
  // 抽象メソッドの定義
  abstract public test():void;

  // クラスの定義
  public test1():void
  {
    // 処理
  }
}

// 抽象クラスの継承
class Test extends Parent
{
}
```

# インターフェース
- 定義 : `interface インターフェース名`
- 実装 : `class クラス名 implements インターフェース名`

```php
<?php
// 定義
interface TestInterface
{
  public function test():void;
}

//  実装
class Test implements TestInterface
{
  // インターフェースにより実装を強制される
  public function test():void
  {
    //  処理
  }
}
```
