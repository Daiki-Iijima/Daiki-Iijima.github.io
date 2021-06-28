---
title: 【Mac】Finderで隠しファイル(.ファイル)を表示させる
date: 2021-05-19 01:17:09
tags:
- Mac
---
# 目次
<!-- toc -->
<!-- more -->

# 永続的に表示させる場合
1. ターミナルで、以下のコマンドを実行する
  ```
  $ defaults write com.apple.finder AppleShowAllFiles TRUE
  ```
2. Finderのプロセスを再起動する
  ```
  $ killall Finder
  ```

## 余談
- Macの環境設定をコマンドで変更する事のできるdefaultsコマンドについて

https://amasuda.xyz/post/2016-10-23-mastering-mac-defaults-command/

# 一時的に表示させる場合

finderを選択している状態で、`⌘` + `Shift` + `.`

