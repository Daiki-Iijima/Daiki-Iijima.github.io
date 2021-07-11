---
title: 【Laravel】マイグレーションの手順
date: 2021-06-08 01:23:02
tags:
- PHP
- Laravel
---
# 目次
<!-- toc -->
<!-- more -->

# 環境
- PHP : 8.0.0
- Laravel : 8.47.3

# マイグレーションとはなにか
マイグレーションとは、データベースのテーブルを作成、消去などの操作をコマンド1つ実行するだけで自動的に構築できるようにする機能です。

# 0. データベースファイルの保存
今回は、sqliteファイルを作成しておきます。

`「アプリケーションディレクトリ/database/」`ディレクトリ内で
```
touch databese.sqlite
```

# 1. スクリプトの作成
以下のコマンドを実行して、マイグレーションスクリプトファイルを作成します。

ここでつけるファイル名は、`create_テーブル名_table`のような形式にしておくと、公式が用意しているファイルと同じような記述でファイルを作成できあます。
```bash
php artisan make:migration 【create_テーブル名_table】
```

実行すると、`「アプリケーションディレクトリ/database/migrations/」`ディレクトリ内に以下のような形式でファイルが生成されているはずです。

```
作成した日付_create_テーブル名_table.php
```

# 2. マイグレーションスクリプトファイルの解説
## メソッド
- up : テーブル生成時の処理を記述する
- down : テーブル消去時の処理を記述する

## デフォルトの処理について
### upメソッド
- id() : プライマリキーを追加する。
- timestamps() : 作成時と更新日時を保存する2つのフィールドを追加する
  - `created_at`と`updated_at`というフィールドが追加される

```php
public function up()
{
  Schema::create('people', function (Blueprint $table) {
    $table->id();
    $table->timestamps();
  });
}
```

### downメソッド
テーブルが存在したら消去する

```php
public function down()
{
    Schema::dropIfExists('people');
}
```

## 3. フィールドの追加
`up`メソッド内に処理を追記することで追加できます。

利用可能なカラムタイプは、公式のドキュイメントを読むとわかりやすいと思います。
- https://readouble.com/laravel/8.x/ja/migrations.html
```php
public function up()
{
  Schema::create('people', function (Blueprint $table) {
    $table->id();
    $table->string("name");
    $table->integer("age");
    $table->timestamps();
  });
}
```

## 4. コマンドを実行して、テーブルを作成する
envファイルに設定したデータベースに対して、テーブルを作成します。

```bash
php artisan migrate
```
