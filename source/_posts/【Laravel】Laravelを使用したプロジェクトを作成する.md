---
title: 【Laravel】Laravelを使用したプロジェクトを作成する
date: 2021-05-08 23:24:52
tags:
- PHP
- Laravel
---

# 目次
<!-- toc -->
<!-- more -->

# 手順
## 1. Laravel Installerを導入する
このときのカレントディレクトリはどこでも大丈夫です。
```bash
$ composer global laravel/Installer
```

## 2. パスを通す
echoを使って書き込むか、テキストエディタで`""`の中の部分を追記してください。
  - bash
    ```bash
    $ echo "export PATH=~/.composer/vender/bin:$PATH" >> ~/.bash_profile
    ```
  - zsh
    ```bash
    $ echo "export PATH=~/.composer/vender/bin:$PATH" >> ~/.zshrc
    ```

パスの設定ができたか確認します。
- 設定の読み込み
  - bash
  ```bash
  $ source ~/.bash_profile
  ```
  - zsh
  ```bash
  $ source ~/.zshrc
  ```
 - バージョンチェックができるかで設定が正常にできているか確認します。以下のような出力がされればパスは通っています。
   ```bash
   $ laravel -V
   Laravel Installer 4.2.7
   ```

### composer globalについて
composerは`global`オプションを使用すると、`

### Laravel Installerとはなにか
composerを使用して、Laravelを使用できるようにしますが、Laravelは、ライブラリではなくフレームワークなので、プロジェクトで使用するというよりは、プロジェクトをLaravelで作成するというニュアンスになります。

なので、まずはLaravelプロジェクトを作成できるツールを導入する必要があります。

## 3. プロジェクトの作成
作成したいプロジェクト用の格納フォルダに移動
```bash 
$ cd ~/Dev/PHP/Laravel
```

`laravel new プロジェクト名`でプロジェクトを生成
  - 今回は、`LaravelFirstApp`というプロジェクトを作成します。
```bash
$ laravel new LaravelFirstApp
```

以下のような出力最後にされれば作成完了です。
```
...
Application key set successfully.

Application ready! Build something amazing.
```

作成したプロジェクトのフォルダ構造はこのようになります。
```
└── LaravelFirstApp
    ├── README.md
    ├── app
    ├── artisan
    ├── bootstrap
    ├── composer.json
    ├── composer.lock
    ├── config
    ├── database
    ├── package.json
    ├── phpunit.xml
    ├── public
    ├── resources
    ├── routes
    ├── server.php
    ├── storage
    ├── tests
    ├── vendor
    └── webpack.mix.js
```
