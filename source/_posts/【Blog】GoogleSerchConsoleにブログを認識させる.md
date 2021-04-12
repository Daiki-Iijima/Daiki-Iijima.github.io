---
title: 【Blog】GoogleSerchConsoleにブログを認識させる
date: 2021-04-01 23:30:12
tags:
- Hexo
---
# 目次
<!-- toc -->
<!-- more -->

# サイトからHTMLファイルをダウンロードする
[Google Serch Console](https://search.google.com/search-console/about?hl=ja)

![GoogleSerchConsole](/2021/04/01/【Blog】GoogleSerchConsoleにブログを認識させる/1.png "GoogleSerchConsole")

URLプレフィックスを選択して、入力欄に自分のブログを入力

![入力画面](/2021/04/01/【blog】googleserchconsoleにブログを認識させる/2.png "入力画面")

所有権の確認ウィンドウが表示されるので、htmlファイル内のファイルをダウンロードで表示されているファイルをダウンロードする

![ダウンロード](/2021/04/01/【blog】googleserchconsoleにブログを認識させる/3.png "ダウンロード")

# (hexo)ダウンロードしたファイルを配置する
hexoの場合は、以下ディレクトリに配置する

```bash
リポジトリ/public/ダウンロードした.html
```

# ファイルをアップロードする
ブログを更新するのと同じ用に、デプロイする

# google serch consoleで認識する
もう一度、
[Google Serch Console](https://search.google.com/search-console/about?hl=ja)に戻り、確認ボタンを押して、確認が取れました画面が出ればOK
