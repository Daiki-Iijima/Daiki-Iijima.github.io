---
title: 【PHP】PHPDocumenterの使い方
date: 2021-05-11 23:53:43
tags:
- PHP
- PHPDocumenter
---
# 目次
<!-- toc -->
<!-- more -->

# PHPDocumenterとは
ソースコード内に記述されているコメントから、ドキュメントを自動生成してくれるツール

# PHPDocコメントをドキュメント化してくれる
PHPには複数種類のコメントの書き方があります。しかし、PHPDocumenterはそれら既存のコメントではドキュメントを生成してくれません。

PHPDocumenterがドキュメントを生成するために用いるのは、`PHPDocコメント`と言われる、以下のような形式のコメント記法を使用する必要があります。

```php
/**
* PHPDocコメント
*/
```

## PHPDocコメントにならないコメント
特に、3つめのコメントはPHPDocコメントと似ているので注意が必要です。
```php
// コメント

# コメント

/*
* コメント
*/
```

# PHPDocで使用できるタグを使用してコメント行に意味をもたせる
- 対象欄の`-`になっている場所は、どんな項目にも使えるタグです。

| タグ          | 対象       | 意味                         | 
|-------------|----------|----------------------------| 
| @author     | -        | プログラムを書いた人                 | 
| @copyright  | -        | 著作権                        | 
| @deprecated | -        | 将来的に使われなくなる予定のものであることを表す   | 
| @param      | メソッド,関数  | 引数の説明                      | 
| @return     | メソッド,関数  | 戻り値の説明                     | 
| @see        | -        | 参考URL,参考クラス                | 
| @throws     | メソッド,関数  | スローする例外クラス                 | 
| @todo       | -        | 今後やるべきことや追加予定の処理           | 
| @package    | ファイル,クラス | パッケージ(そのクラスが所属するnamespace) | 

# 使用までの手順
## 1. composerを使用してインストールする
ドキュメントを作成したいプロジェクトにcomposerを使用してphpdocumntorを導入する
```bash
composer require --dev phpdocumentor/phpdocumentor
```
## 2. ドキュメントを生成する
今回は以下のソースコード単体のドキュメントを作成してみます。
```php
<?php
declare(strict_types = 1);

/**
 *  整数型の計算を行うクラス
 */
class IntegerCalculate
{
  /**
   * 内部で保持計算結果
   */
  private int $Value;

  /**
   * コンストラクタ
   * @param int $defaultValue 計算を始める初期値
   */
  public function __construct(int $defaultValue)
  {
    $this->Value = $defaultValue;
  }

  /**
   * 値を加算する
   * @param int $value 加算する値
   * @return IntegerCalculate 整数型計算クラス
   */
  public function Add(int $value):IntegerCalculate
  {
    $this->Value += $value;
    return $this;
  }

  /**
   * 値を減算する
   * @param int $value 減算する値
   * @return IntegerCalculate 整数型計算クラス
   */
  public function Sub(int $value):IntegerCalculate
  {
    $this->Value -= $value;
    return $this;
  }

  /**
   * 計算結果を取得する
   * @return int 計算結果
   */
  public function Result(int $value):int
  {
    return $this->Value;
  }
}
```
プロジェクトのルートディレクトリから、以下のようなコマンドを実行します。
- -d : ディレクトリを指定する場合
- -f : ファイルを指定する場合
- -t : 出力先のフォルダ名を指定します。
  - 省略可能とドキュメントには書いてあるが、省略するとどこに出力されるかわからない
```bash
./vendor/bin/phpdoc -f IntegerCalculate.php -t out
```

複数ファイルでドキュメントを作成する場合は、ファイル指定(-f)している部分をフォルダディレクトリ(-d)とかにすると楽です。

## 3. ドキュメントの確認 
- 出力されたフォルダ内の`index.html`がドキュメントの内容になっています。

# 参考
- 公式のドキュメント
  - https://docs.phpdoc.org/3.0/
- コマンドオプションも公式のドキュメントに載っています。テンプレート変更機能とかもあるらしいです。
  - https://docs.phpdoc.org/3.0/guide/guides/running-phpdocumentor.html

