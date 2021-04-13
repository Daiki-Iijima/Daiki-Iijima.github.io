---
title: 【Git】rebaseを使うとき
date: 2021-04-19 07:57:51
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# ローカルリポジトリかつローカルブランチのときに使うようにしよう
リベースコマンドは、既存のコミットを書き換えることができる強力なコマンドで、書き換えたコミットのSHA1が書き換わってしまうので、すでにPushしてあるコミットに対してリベースを行ってしまうと、他の作業者ローカルリポジトリとの整合性が取れなくなってしまいとても面倒くさい事になってしまいます。

なので、リベースコマンドを使用するときは、影響範囲が狭い、ローカルリポジトリのローカルブランチ(開発用ブランチ)のみに使用する用にしましょう。

# 利用ケース1 : コミット履歴の整理
開発が終了して、マスターブランチにマージする前に今までのローカルブランチのコミット履歴の中で、冗長なコミットをスカッシュ(squash:潰して合成)するために使用します。

## 冗長なコミットとは？
- typeの修正
- コミット忘れの追加コミット
など

## 使用例
1. まとめたいコミットのSHA1を探す
今回は、`2,3の追加`に`4,5,の追加`をスカッシュするので、`2,3の追加`の１つ前のコミットSHA1を探す
```bash
$ git log --oneline

5b57433 (HEAD -> master) 4,5の追加
52f0632 2,3の追加
61e4e43 1の追加
```

2. リベースを行う
-i : interactive
```bash
$ git rebase -i 61e4e43
```

3. スカッシュする
以下のようなエディタ画面が表示される
```bash
pick 52f0632 2,3の追加
pick 5b57433 4,5の追加

# Rebase 61e4e43..5b57433 onto 61e4e43 (2 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
```

`pick 5b7433`の部分を`squash 5b7433`に書き換えて、保存終了(vimの場合、ZZ)

```bash
pick 52f0632 2,3の追加
squash 5b57433 4,5の追加

# Rebase 61e4e43..5b57433 onto 61e4e43 (2 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
```

4. コミットメッセージを編集する
squashするコミットを選択してエディタを終了すると、以下のような画面が表示される
```bash
# This is a combination of 2 commits.
# This is the 1st commit message:

2,3の追加

# This is the commit message #2:

4,5の追加

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Tue Apr 13 09:19:56 2021 +0900
#
# interactive rebase in progress; onto 61e4e43
# Last commands done (2 commands done):
#    pick 52f0632 2,3の追加
#    squash 5b57433 4,5の追加
# No commands remaining.
# You are currently rebasing branch 'master' on '61e4e43'.
#
# Changes to be committed:
#	new file:   2
#	new file:   3
#	new file:   4
#	new file:   5
#

```

`# This is the`となっている部分を消去して、新しいコミットメッセージを入力して、保存終了(vimの場合、ZZ)

```bash
# This is a combination of 2 commits.

2,3,4,5の追加

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Tue Apr 13 09:19:56 2021 +0900
#
# interactive rebase in progress; onto 61e4e43
# Last commands done (2 commands done):
#    pick 52f0632 2,3の追加
#    squash 5b57433 4,5の追加
# No commands remaining.
# You are currently rebasing branch 'master' on '61e4e43'.
#
# Changes to be committed:
#	new file:   2
#	new file:   3
#	new file:   4
#	new file:   5
#
```

5. git logでコミットを確認して１つになっていれば完了
```bash
$ git log --oneline

8a0979f (HEAD -> master) 2,3,4,5の追加
61e4e43 1の追加
```

### 中止したいとき
```bash
$ git rebase --abort
```

# 利用ケース2 : ブランチの親の変更を取り込む
ローカルブランチの開始地点を変更することで、更新のあった親ブランチの変更を取り込んむたくなるときに使用します。

```bash
$ git rebase master
```
