---
title: 【Git】直前のコミットを修正する
date: 2021-04-08 23:01:42
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# --amendスイッチを使用する
`amend`とは、日本語で`修正する`という意味。修正するというものの、できないこともあるので注意する必要がある

## できること
- 直前のコミットメッセージの修正
- 直前のコミット内容へのファイルの追加

## できないこと
- 2つ以上前のコミットを修正する
	 - `git rebase -i`と組み合わせて行う
- コミットからファイルを消去する
	- `git reset`を使う必要がある

# コミットメッセージの編集の仕方
以下コマンドを実行する 
```shell-session
$ git commit --amend
```

Gitに設定してあるエディタが開き、以下のような編集画面が表示される
```shell-session

1.txtの追加

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Fri Mar 12 14:22:29 2021 +0900
#
# On branch master
# Changes to be committed:
#	new file:   "1.txt"
#
```

この一番上のメッセージを編集して、保存してエディタを閉じれば自動で１つ前のコミットを書き換えてくれる

# ファイルを追加する
追加したいファイルを`git add`してステージングしてから、`git commit --amend`を使用する

```shell-session
$ git add テスト2.txt
$ git commit --ammend --no-edit
```

`--no-edit`スイッチは、直前のコミットのメッセージを変更せずにそのまま使い回すスイッチ
	-	コメントも編集したい場合は、`--no-edit`スイッチをつけなければ編集できる
