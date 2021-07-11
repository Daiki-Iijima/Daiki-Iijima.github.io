---
title: 【Laravel】シーディング機能を使用してダミーデータを作成する
date: 2021-06-10 02:46:20
tags:
- PHP
- Laravel
---
# 目次
<!-- toc -->
<!-- more -->

# シーティングとは
ダミーのレコードを登録する処理を記述しておく機能

# 1. シーダーファイルの作成
以下のコマンドを実行します。

```php
php artisan make:seeder 【テーブル名TableSeeder】
```

# 2. ダミーデータの追記
1の手順で作成したファイルは、`「アプリケーションディレクトリ/database/seeders/」`ディレクトリ内に生成されています。

`use Illuminate\Support\Facades\DB;`の追記が必要が必要です

処理としては、連想配列を`クエリビルダー`で挿入するだけです。
```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\DB;

class PeopleTableSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        //  ここに処理を記述します
        DB::table('テーブル名')->insert([
            [
                'キー' => '値',
                'キー' => '値',
            ],
            [
                'キー' => '値',
                'キー' => '値',
            ],
            [
                'キー' => '値',
                'キー' => '値',
            ],
        ]);
    }
}
```

# 3. シーダーファイルの登録
作成した、シーディングファイルは、そのままでは実行されません。コマンドでシーディングが実行されるように、`DatabaseSeeder`に登録する必要があります。

`「アプリケーションディレクトリ/database/seeders/」`ディレクトリ内にLaravelのイニシャライズ時に生成されていたファイル`DatabaseSeeder.php`を編集します

はじめに開くと、以下のような内容になっていると思います。
```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    /**
     * Seed the application's database.
     *
     * @return void
     */
    public function run()
    {
        // \App\Models\User::factory(10)->create();
    }
}
```

`runメソッド`に以下のように追記していきます。

`callメソッド`は設定されたクラスの`runメソッド`を呼び出します。
```php
namespace Database\Seeders;

use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    /**
     * Seed the application's database.
     *
     * @return void
     */
    public function run()
    {
        // \App\Models\User::factory(10)->create();
        $this->call(シーダークラス名::class);
    }
}
```

# 4. シーディングの実行
```bash
php artisan db:seed
```
