---
title: 【Git】基本的なマージの手順
date: 2021-04-24 23:14:29
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# 手順
今回は`master`に`t`ブランチを取り込む

## 1. マージを取り込みたいブランチに移動する
`master`ブランチに移動
```bash
$ git checkout master
```

移動できたか確認、`master`の左側に`*`がついていればOK
```bash
$ git branch

* master
t
```
## 2. マージコマンドを実行する
`master`に`t`を取り込む(mergeする)
```bash
$ git merge t
```
## 3.1 正常に完了した場合
### 表示される内容のサンプル
```bash
Updating d71dc36..bc5d29e
Fast-forward
 1 | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

正常にマージできているか確認する。このような表示が出ればOK
```bash
$ git status

On branch master
nothing to commit, working tree clean
```
## 3.2 コンフリクトが発生した場合
### 表示される内容のサンプル
```bash
Auto-merging 1
CONFLICT (content): Merge conflict in 1
Automatic merge failed; fix conflicts and then commit the result.
```

### 現在の状態を確認
`Unmerged paths`の部分のファイルがコンフリクトを起こしているファイルです。
今回のサンプルだと、`1` というファイルがコンフリクトを起こしています。
```bash
$ git status

On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   1

no changes added to commit (use "git add" and/or "git commit -a")
```

### コンフリクトを解決するには
コンフリクトを起こしているファイルを開きます。そうすると、以下のような表記の部分があるはずです。

```bash
これはテスト文章です0
<<<<<<< HEAD
これはテスト文章です2
=======
これはテスト文章です3
>>>>>>> t
これはテスト文章です2
```

この`<<<<<<<<<<< HEAD`から`=========`までが`変更を取り込むブランチの変更`、`==========`から`>>>>>>>>>>> t`までが`変更を取り込まれるブランチの変更`です。

変更を`取り込まない`方の変更点を消して、`>>>`,`<<<`,`===`のgitによって追加された部分をすべて消去します。

`変更を取り込むブランチ`(masterブランチ)の変更を適応する場合のファイルの編集例
```bash
これはテスト文章です0
これはテスト文章です2
これはテスト文章です2
```

編集後、編集したファイルを`git add`してから、コミットします。

add
```bash
$ git add 1
```

commit、マージのコミットの場合、`git commit`のみで自動的にコミットメッセージが生成されます。`git commit`を実行するとエディタが開くので(Vimの場合)`ZZ`をタイプして、エディタを抜けます。
```bash
$ git commit 
```

開かれたエディタ画面のサンプル
```bash
Merge branch 't'

# Conflicts:
#	1
#
# It looks like you may be committing a merge.
# If this is not correct, please run
#	git update-ref -d MERGE_HEAD
# and try again.


# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# All conflicts fixed but you are still merging.
#
```

最後に正常にマージできているか`git status`で確認して、以下のような表示になればOK
```bash
$ git status

On branch master
nothing to commit, working tree clean
```
