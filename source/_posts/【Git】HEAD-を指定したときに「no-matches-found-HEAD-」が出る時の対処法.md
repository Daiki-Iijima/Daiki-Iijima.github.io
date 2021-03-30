---
title: 【Git】HEAD^を指定したときに「no matches found/ HEAD^」が出る時の対処法
date: 2021-03-21 05:44:10
tags:
- Git
---
## 目次
<!-- toc -->
<!-- more -->

## 原因
zshの設定が問題らしく、設定ファイル(.zshrc)に`setopt extended_glob`を記述している場合に起こる。

### setopt extended_globとはなにか
除外パターン、大文字小文字同一視などの、拡張表記が可能になる。詳しくは以下リンク先のサイトがわかりやすかった。
- https://gihyo.jp/dev/serial/01/zsh-book/0004

## 解決策
### エスケープシーケンスを使用する

```shell-session
git checkout HEAD\^
```
