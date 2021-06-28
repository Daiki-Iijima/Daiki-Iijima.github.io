---
title: 【PHP】クラス、メソッド、プロパティの動的コール
date: 2021-05-18 01:16:15
tags:
- PHP
---
# 目次
<!-- toc -->
<!-- more -->

# 動的アクセス
## プロパティに対しての動的アクセス
通常の場合、複数あるプロパティの変数にアクセスしたい場合、以下のように書きます。

```php
$インスタンス名->{$プロパティ名}
```

### 例
以下のようなアイテムクラスの一覧を列挙したい
```php
class Item{
  //  名前
  public string $name;
  //  値段
  public int $price;
  //  重さ
  public int $weight;

  function __construct(string $name,int $price,int $weight){
    $this->name = $name;
    $this->price = $price;
    $this->weight = $weight;
  }
}
```

表示するには、１つずつのプロパティを呼び出して記述する必要がある
```php
$item = new Item('チーズ',300,100);

//  表示
echo '名前' ,':', $item->name,'<br>';
echo '値段' ,':', $item->price,'<br>';
echo '重さ' ,':', $item->weight,'<br>';
```

問題点は2つ
- プロパティ名と表示したい名前の結びつきがわかりにくい
- プロパティ数が多いと行が増えていき可読性が下がる


### 動的アクセスを使った場合
使うクラスは、最初のItemクラスと同じものを使う。

このように、Itemクラスに変数が増えたとしても、properties連想配列に組み合わせを追加するだけで、表示を追加できる様になる
```php
//  最初にプロパティを定義する
$properties=[
  'name' => '商品名',
  'price' => '金額',
  'weight' => '重さ'
];

$item = new Item('チーズ',300,100);

//  プロパティのループ
foreach($properties as $propertie=>$label){
  //  $インスタンス名->{$プロパティ名を持つ変数名}
  echo $label ,':', $item->{$propertie},'<br>';
}
```

## メソッドの動的コール
```php
$インスタンス名->{$メソッド名}(引数1,引数２...);
```

メソッドの動的コールを行う際は、`method_exists`を使用して呼び出したいメソッドをインスタンス化したクラスが持っているかをチェックしたほうがいい

```php
if(!method_exists($インスタンス名,$呼び出したいメソッド名){
  //  含まれていないときはここに入る
}
```

## クラスの動的コール
通常のクラスのインスタンス化との違いは、クラス名の前に`$`があること
```php
$newInstance = new $メソッド名();
```

クラスの動的コールを行う際は、`class_exists`を使用してインスタンス化したいクラス存在しているかチェックしたほうがいい

```php
if(!class($インスタンス化したいクラス名)){
  //  含まれていないときはここに入る
}
```

