---
title: 【PHP】PHPUnitを使って単体テスト
date: 2021-05-15 01:11:15
tags:
- PHP
- PHPUnit
---
# 目次
<!-- toc -->
<!-- more -->

# composerを使用してPHPUnitを導入する
```bash
composer require --dev phpunit/phpunit "^8.5.5"
```

# テストを記述する
- `phpunit`を使用するには、作成する`ファイル名`、`クラス名`は末尾が`Test`である必要があります。

今回はサンプルのために、`MyAppTest.php`というファイルを作成します。
## 1. MyAppTest.phpにMyAppTest classを作成する

- 以下のコードをファイルの先頭に記述して、phpunitを使用できるようにする
  ```php
  //  composerに自動生成された、autoloadファイルを読み込み
  require_once dirname(__FILE__) . '/vendor/autoload.php';
  //  テストフレームワークを読み込む
  use PHPUnit\Framework\TestCase;
  ```

## 2. functionにテストを記述していく
- `assertXXX`メソッドに記述することでテストケースを記述していく

```php
//  配列の数が期待通りかテストする
public function test1()
{
  $arr = [100,200,300];
  $this->assertCount(3,$arr);
}
```

## 3. テストの実行
- composerでインストールしたphpunitのテスト用の実行ファイルは以下のディレクトリにある

```bash
vendor/bin/phpunit
```

- phpunitの実行ファイルにテストしたい(今回の場合はMyAppTest.php)ファイルを渡す

```php
vendor/bin/phpunit MyAppTest.php
```

## 4. 実行結果のみかた
- `.` : 成功
- `F` : 失敗

```bash
PHPUnit 8.5.15 by Sebastian Bergmann and contributors.

.                                         1 / 1 (100%)

Time: 44 ms, Memory: 4.00 MB

OK (1 test, 1 assertion)
```


