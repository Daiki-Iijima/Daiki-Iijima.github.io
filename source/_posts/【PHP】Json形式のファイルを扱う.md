---
title: 【PHP】Json形式のファイルを扱う
date: 2021-06-07 23:43:41
tags:
- PHP
---
# 目次
<!-- toc -->
<!-- more -->

# 値をJson形式にエンコードする
`json_encode関数`を使用する

```php
<?php
$array =['name'=>'Daiki Iijima','age'=>23,'icon'=>null];

$json = json_encode($array);

echo $json;

// {"name":"Daiki Iijima","age":23,"icon":null}
```

## オプション
- `json_encode(obj,オプション)`のオプション部分に設定できる
- 複数設定したい場合は、`|`で区切る

| オプション                        | 効果                          | 
|------------------------------|-----------------------------| 
| JSON_HEX_TAG                 | 「>」「<」記号をエスケープする            | 
| JSON_HEX_AMP                 | 「$」記号をエスケープする               | 
| JSON_HEX_APOS                | 「'」記号をエスケープする               | 
| JSON_HEX_QUOT                |「"」記号をエスケープする  |                             | 
| JSON_FORCE_OBLECT            | 連想配列ではない値を強制的にオブジェクト型で出力する  | 
| JSON_NUMERIC_CHECK           | 数値が文字列型で表されていた場合、数値として出力する  | 
| JSON_BIGINT_AS_STRING        | 大きな整数値を文字列型として出力する          | 
| JSON_PRETTY_PRINT            | 改行とインデントを使って出力結果を見やすくする     | 
| JSON_UNESCAPED_SLASHES       | 「¥」記号をエスケープしない              | 
| JSON_UNESCAPED_UNICODE       | Unicode文字列を16進数にエスケープしない    | 
| JSON_PARTIAL_OUTPUT_ON_ERROR | エンコードできない値を代替値に置き換える        | 
| JSON_PRESERVE_ZERO_FRACTION  | float型の値を常にfloat値としてエンコードする | 

# Json形式の値をデコードする
`json_decode関数`を使用する

- `json_encode関数`の2つの目の引数の`true`は、オブジェクト型をi`連想配列型`に変換する
  - 何も指定しない場合、`false`になり、出力される型は`stdClass`になる

```php
<?php
$json ='{"name":"Daiki Iijima","age":23,"icon":null}';

$array = json_decode($json,true);

print_r($array);

//Array
//(
//    [name] => Daiki Iijima
//    [age] => 23
//    [icon] => 
//)
```

# デコード,エンコードのエラーを検知する
`json_last_error関数`を使用する

## 返される定数値一覧
| 定数                               | 意味                             | 
|----------------------------------|--------------------------------| 
| JSON_ERROR_NONE                  | 処理成功                           | 
| JSON_ERROR_DEPTH                 | $depthの指定階層より深い階層だった           | 
| JSON_ERROR_STATE_MISMATCH        | JSON形式が無効                      | 
| JSON_ERROR_CTRL_CHAR             | 制御文字エラー                        | 
| JSON_ERROR_SYNTAX                | 構文エラー                          | 
| JSON_ERROR_UTF8                  | UTF-8文字の形式が不正                  | 
| JSON_ERROR_UTF16                 | UTF-16文字の形式が不正                 | 
| JSON_ERROR_RECURSION             | エンコード対象の値が再起参照を含んでいる           | 
| JSON_ERROR_INF_OR_NAN            | エンコード対象の数値が「NaN」または「Inf」を含んでいる | 
| JSON_ERROR_UNSUPPORTED_TYPE      | エンコードできない方を含んでいる               | 
| JSON_ERROR_INVALID_PROPERTY_NAME | エンコードできないプロパティ名を含んでいる          | 

## 使用例
```php
<?php
$json ='{"name":"Daiki Iijima","age":23,"icon":null}';

$array = json_decode($json,true);

switch(json_last_error){
  case JSON_ERROR_NONE:
    echo "エラーはありませんでした";
    break;
}

```
