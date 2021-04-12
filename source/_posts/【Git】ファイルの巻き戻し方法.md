---
title: 【Git】ファイルの巻き戻し方法
date: 2021-03-30 22:12:24
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# ステージングエリアの変更を取り消す
git addの反対のことをする必要があるので、`git reset`を使用する。ステージングの取り消しなので、作業ディレクトリのファイルは変化しない。

git reset を使ってファイルのステージングを取り消す
```shell-session
$ git add test.txt
$ git reset test.txt
```

# ファイルを最後に変更(commit)した状態に戻す
git commitしたということは、ファイルの状態を保存してあるので、`git checkout`を使えば戻すことができる。

git checkout を使用して、ファイルの中身を最後に変更した状態に戻す
```shell-session
$ git checkout ファイル名
```

作業エリアすべてのファイルを最後のコミットの状態に戻す
```shell-session
$ git checkout .
```
