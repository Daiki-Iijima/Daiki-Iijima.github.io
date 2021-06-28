---
title: 【Laravel】SQLiteを使用する
date: 2021-05-01 23:11:45
tags: 
- PHP
- Laravel
---
# 目次
<!-- toc -->
<!-- more -->

# DBの設定項目
`config`->`database.php`ファイルが必要

`18行目`あたり(たぶん最初)にある、`default`
- env : Laravelの環境変数を取得する
  - 今回のケースだと、`DB_CONNECTION`環境変数が取得できない場合、`mysql`という値を返す

```php
'default' => env('DB_CONNECTION', 'mysql'),
```

これを、以下のように変更する

```php
'default' => env('DB_CONNECTION', 'sqlite'),
```

# 設定項目の解説
`connections`という配列の中の`sqlite`配列に`sqlite`の設定があります。
```php
'sqlite' => [
    'driver' => 'sqlite',
    'url' => env('DATABASE_URL'),
    'database' => env('DB_DATABASE', database_path('database.sqlite')),
    'prefix' => '',
    'foreign_key_constraints' => env('DB_FOREIGN_KEYS', true),
]
```

- `'driver' => 'sqlite'` : ドライバー名
- `'url' => 'env('DATABASE_URL')'` : `DATABASE_URL`環境変数を取得する
- `'database' => env('DB_DATABASE', database_path('database.sqlite'))` : データベースの値を変更する
- `'foreign_key_constraints' => env('DB_FOREIGN_KEYS', true)` : `DB_FOREIGN_KEYS`環境変数が取得して、ない場合、`true`を返す

# 環境変数の設定
`アプリのルートディレクトリ`内の、`.env`ファイルを編集する
- .envフィいるとは? : Laravelの環境変数が記述してあるファイル

`DB_CONNECTION`という項目を探して以下のように修正する

初期状態だとこの様になっている
```php
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=dbpractice
DB_USERNAME=root
DB_PASSWORD=
```

DB_XXXと表示された項目は、メントアウトするか消去して、`DB_CONNECTION=sqlite`を追記する
```php
DB_CONNECTION=sqlite
```

# 参考
- https://readouble.com/laravel/5.5/ja/helpers.html#method-env
