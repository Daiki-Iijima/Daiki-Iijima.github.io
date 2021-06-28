---
title: 【Laravel】8.x系のルーティングとコントローラーの使い方
date: 2021-05-04 23:27:42
tags:
- PHP
- Laravel
---
# 目次
<!-- toc -->
<!-- more -->

# シンプルなコントローラー
## 1. 作成
手動でファイルを作成することもできるが、`Laravel`には作成用のコマンドが用意されているので、そのコマンドを使ったほうが、名前空間や最低限必要な記述をしてくれるので便利

以下のコマンドを使用すると、`app/Http/Controllers/`ディレクトリに`xxxController.php`というファイルが生成される
```bash
php artisan make:controller xxxController
```

## 2. アクションメソッドを記述する
1で作成したコードを見ると、以下のようなコードになっているはず。

このコードを見ると、
```php
<?php

namespace App\Http\Controllers;

class xxxController extends Controller
{
  //
}
```

このコードに`ルーティング`されたときに呼ばれるコードを記述する

今回のケースだと、`index`をルーティング先として設定すると、`Hello`と画面に表示されるメソッドを作成した
```php
<?php
namespace App\Http\Controllers;

class xxxController extends Controller
{
    public function index()
    {
        return  "Hello";
    }
}
```

## 3. ルーティングの設定
`Route`クラスの`get`スタティックメソッドを使用する
- アクセスURL:`/XXX`と設定すると`http://アプリURL/XXX`でアクセスできる
- アクションメソッド名:Controllerクラスに記述したメソッド
```php
<?php
use app\Http\Controller名;

Route::get('アクセスURL',[Controller名::class,'アクションメソッド名']);
```

`2`のコードをアクセスURL`/hello`で設定すると以下のようになる
```php
<?php
use app\Http\Controller名;

Route::get('/hello',[xxxController::class,'index']);
```

# シングルアクションコントローラー
## 1. 作成
シンプルなコントローラー作成コマンドに、`--invokable`オプションを付けることで、`__invoke`メソッドを含んだクラスを作成することができる

```bash
php artisan make:controller xxxController --invokable
```

## 2. __invokeメソッドは基本的にアクションメソッドと同じ
シングルアクションの特徴として、アクションコントローラーには複数のアクションメソッドを記述したのに対して、シングルアクションは１つだけのアクションしか記述しません。

1の`--invokable`オプションで作成すると以下のようなものが自動生成されます。

自動生成された`__invoke`は`Laravel`が用意したメソッドではなく、`PHP`に標準でビルドインされているメソッドです。

以下は`SingleActionController`を作成した例です。
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class SingleActionController extends Controller
{
    public function __invoke()
    {
    }
}
```

この`__invoke`メソッド内に`ルーティング`されたときに呼ばれるコードを記述します。

今回のケースだと、`SingleActionController`をルーティング先として設定すると、`hello`と画面に表示されます。
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class SingleActionController extends Controller
{
    public function __invoke()
    {
      return "hello";
    }
}
```

## 3. ルーティングの設定
基本的には、基本のコントローラーと同じ記述ですが、今回は、`シングルアクションコントローラー`なので呼び出すアクションメソッドクラスの記述が必要ありません。

```php
<?php
use app\Http\Controller名;

Route::get('アクセスURL',Controller名::class);
```

`2`のコードをアクセスURL`/single`で設定すると以下のようになる
```php
<?php
use app\Http\Controller名;

Route::get('/single',SingleActionController::class);
```
