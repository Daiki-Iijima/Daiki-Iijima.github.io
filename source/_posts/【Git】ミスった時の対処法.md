---
title: 【Git】ミスった時の対処法
date: 2021-04-20 09:48:31
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# リベースやコミットを取り消したいとき
注意::このコマンドで戻すことができるのは、gitで管理しているファイルのみです。

1. `git reflog`を使用して、コマンドの履歴を取得する
`git reflog`は`HEAD`の参照の変更が行われた時の履歴を表示できるコマンドです。

```bash
$ git reflog

8a0979f (HEAD -> master) HEAD@{0}: rebase (finish): returning to refs/heads/master
8a0979f (HEAD -> master) HEAD@{1}: rebase (squash): 2,3,4,5の追加
52f0632 HEAD@{2}: rebase (start): checkout 61e4e43
5b57433 HEAD@{3}: rebase (abort): updating HEAD
61e4e43 HEAD@{4}: rebase (start): checkout 61e4e43
5b57433 HEAD@{5}: commit: 4,5の追加
52f0632 HEAD@{6}: commit: 2,3の追加
61e4e43 HEAD@{7}: commit (initial): 1の追加
```

2. `git reset --hard HEAD@{番号}`でリポジトリを巻き戻す
`--hard`スイッチを使用すると、ステージングエリアと作業ディレクトリの療法がリセットされ、リポジトリの状態が正しく戻されます。もし、gitで管理していないファイルが悪さをする場合は、`git clean -f`コマンドも併用するといいかもしれません。

- ここで、指定するのは、戻したいコマンドを使用する１つ前のHEAD番号です。今回使用しているリポジトリの`リベース前に戻したい場合`は`HEAD@{5}`を指定することになります。
```bash
$ git reset --hard HEAD@{5}
```
