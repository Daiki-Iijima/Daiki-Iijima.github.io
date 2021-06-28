---
title: 【Laravel】「Target class [XXXController] does not exist.」エラーは8.x系のルーティング仕様の変化が原因
date: 2021-05-07 22:42:11
tags:
- PHP
- Laravel
---
# 目次
<!-- toc -->
<!-- more -->

# はじめに
コントローラーとURLのルーティングを設定するときに以下のようなエラーが出たのでその対応策と原因を調べた。

# エラー
```
Target class [xxxController] does not exist.
```
# 対応策
## 公式ドキュメントの方法
`xxx/usr`のURLにアクセスされた際に、`UserController`の`index`アクションメソドをルーティングしたい場合、以下のような記述になる
```php
use App\Http\Controllers\UserController;

Route::get('/user', [UserController::class, 'index']);
```

## 7.xより前の方法を踏襲する
namespaceのフルパスを追記する形で以前と同じような記述で設定もできる
```php
Route::get('/hello','App\Http\Controllers\HelloController@index')
```
`use`でnamespaceを切り出すこともできる
```php
use App\Http\Controllers\UserController;

Route::get('/hello','HelloController@index')
```

# 参考リンク
- 公式ドキュメント
  - https://readouble.com/laravel/8.x/ja/routing.html
- Qiitaの同じような解決策
  - https://qiita.com/norichintnk/items/34a04cd17bfe4014313a

