---
title: 【Git】Git独自のaliasを設定して長いコマンドを短くする
date: 2021-03-31 23:13:35
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# 設定方法
## 1. コマンドから設定する
コマンドラインから、`git config`を使用して設定する方法

```
git config --global alias.設定したいコマンド名 "短くしたいコマンド"
```

今回は、コミット履歴(log)をグラフ表示(--graph)しながら、一行(--oneline)ですべてのブランチ(--all)のコミットを表示するコマンドを`loga`として登録します。
```shell-session
$ git config --global alias.loga "log --graph --oneline --all"
```

## 2. configファイルを編集する
設定ファイルを開くこまどで`.gitconfig`を開きます。

```shell-session
$ git config --global --edit 
```

`[alias]`という記述がなければ一緒に追記してください。

```shell-session
[alias]
	loga = log --graph --oneline --all
```
