---
title: 【PHP】CGI版とCLI版の違いについて
date: 2021-05-24 00:15:36
tags:
- PHP
---
# 目次
<!-- toc -->
<!-- more -->

# CGI版
CGIとは`Common Geteway Interface`の略で、`Webサーバー`経由で実行される方式
- CGI版とは別に、Webサーバーにビルドインされている`モジュール版`というものもある。

## モジュール版とCGI版の違い
- CGI版:php.exeのような実行形式ファイルを実行しているイメージ(XAMPP,MAMP)
    - `php.ini`ファイルなどでディレクトリによって実行するPHPのバージョンを切り替える事ができる
    - 実行速度がモジュール版に比べて遅くなる
- モジュール版:Apach内部のプロセスとしてPHPを実行する(Apach内部から呼び出す)
    - 内部で処理できるので、処理がモジュール版と比べて高速
    - 実行するPHPのバージョンをディレクトリによって切り替えることはできない

# CLI版
CLIとは`Command Line Interface`の略で、`OSコマンド`として実行できる方式

以下のように、phpコマンドの引数にファイルを渡すことで実行結果が表示される
```bash
php test.php
```

# 主な違い
出力結果が主な違いとして挙げられます。

以下のようなPHPファイルを実行したときに
```php
<?
echo "test";
```

- CGI
    - ヘッダー情報が自動で付与される
    ```bash
    X-Powered-By: PHP/8.0.0
    Content-type: text/html
    
    test
    ```

- CLI
    ```bash
    test
    ```

# 今実行しているPHPがどっち版なのかを確認する
コマンドラインで、以下のコマンドを実行すると`CLI`なのか`CGI`なのか確認できる(`(cli)`の部分)

この実行結果の場合、CLI版
```bash
$ php -v
PHP 8.0.0 (cli) (built: Jun  7 2021 02:19:47) ( NTS )
Copyright (c) The PHP Group
Zend Engine v4.0.0-dev, Copyright (c) Zend Technologies
    with Zend OPcache v8.0.0, Copyright (c), by Zend Technologies
    with Xdebug v3.0.4, Copyright (c) 2002-2021, by Derick Rethans
```
