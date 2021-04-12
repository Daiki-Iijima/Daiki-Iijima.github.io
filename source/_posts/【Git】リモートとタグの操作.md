---
title: 【Git】リモートとタグの操作
date: 2021-04-05 00:35:53
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# リモートにタグをプッシュする
`git push origin タグ名`コマンドを使用します。

## 実行例
`test`タグをプッシュします。

```bash
$ git push origin test
```

# リモートのタグを消去する
`git push origin :タグ名`コマンドを使用します。

ブランチの消去の仕方と同じ用に、リファレンスを指定しないことでタグを消去しています。

## 実行例
`test`タグを消去します。

```bash
$ git push origin :test
```
