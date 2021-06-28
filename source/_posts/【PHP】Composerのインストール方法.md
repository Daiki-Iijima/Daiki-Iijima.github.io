---
title: 【PHP】Composerのインストール方法
date: 2021-05-17 01:14:38
tags:
- PHP
- Composer
---
# 目次
<!-- toc -->
<!-- more -->

# Composerとは
ライブラリの依存関係を自動で解決してくれるパッケージ管理ツール

`オートローダー`という機能が便利
- `autoload.php`を１つ読むだけで自動でライブラリが読み込まれる

# インストール手順
Macの場合は、コマンドでインストール、Windowsの場合はexeファイルを叩いてインストールする

公式サイトの`Download`を参考にするといい
- https://getcomposer.org/download/

## Windows
1. `Download and run Composer-Setuup.exe -it will install the lastest composer version whenever it is executed.`
と書いてある部分のリンクから、実行ファイルをダウンロードする。

2. `Developer mode`にはチェックを入れない

3. `php.exe`のインストールされているパスを設定する

4. プロキシの設定がない場合はスルー

5. `Install`を押す

6. パスを反映させるために、Windowsを再起動して以下のコマンドをコマンドプロンプトに入力して同じような表示になれば導入完了
```bash
> composer about
Composer - Dependency Manager for PHP
以下略....
```

## Mac

1. Download Composerの少し下に書いてある4行のコマンドを実行する
```bash
$ php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

2. `Composer successfully installed...` が表示されたらインストールは完了

3. 以下のコマンドを実行してパスを通す
```bash
$mv composer.phar /usr/local/bin/composer
```

4. パスが通ったか確認する。以下のようなAAが出れば導入完了
```bash
❯ composer -v
   ______
  / ____/___  ____ ___  ____  ____  ________  _____
 / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
/ /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
\____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                    /_/
Composer version 2.0.14 2021-05-21 17:03:37
```
