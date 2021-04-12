---
title: 【Git】リモート関係のブランチの操作
date: 2021-04-10 11:03:07
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# ブランチをプッシュする
ブランチをプッシュするには、pushコマンドに`--set-upstream`スイッチをつけます。

## set-upstreamをつけない場合エラー表示
リモートブランチにクローンしたリポジトリで作成した`test`をpushします。

すでにエラー文に解決方法が書いてあるのでそれ通りのコマンドを実行します。
```bash
$ git push

fatal: The current branch test has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin test

```

## 実行結果

```bash
$ git push --set-upstream origin test

Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 206 bytes | 206.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To /Users/daiki/Desktop/git/testRp/../bearRp/bare
 * [new branch]      test -> test
Branch 'test' set up to track remote branch 'test' from 'origin'.
```

# リモートブランチを消去する

リモートブランチ消去する場合`git push origin :消去したいブランチ名`コマンドを使用します。このコマンドだけでは、ローカルブランチは消去されません。

ローカルブランチも消去するには２つのコマンドを使う必要があります。１つはローカルブランチの消去のための`git branch -d`、2つめはリモートブランチを消去するための`git push origin :`です。

1. ローカルブランチ消去 : git branch -d 消去したいブランチ名
2. リモートブランチ消去 : git push origin :消去したいブランチ名

## リモートブランチを消去するときの「:消去したいブランチ名」とはなにか
refspec(リファレンス指定)と呼ばれるもので、`ソース側ブランチ(src):ディスティネーション側ブランチ(dest)の対応を表しています。

通常の`git psuh`コマンドでも、複雑な構文が隠されているだけで、正式な記述をすると`git push origin ローカルブランチ:リモートブランチ`となります。

## 実行例
`testブランチ`を消去します。

リモートブランチのみを消去する場合
```bash
$ git push origin :test
```

ローカルブランチとリモートブランチどちらも消去する場合
```bash
$ git branch -d test
$ git push origin :test
```
