---
title: 【Gif】Gitで使えるgrepコマンド
date: 2021-04-15 06:57:38
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# 特定のコミットメッセージのコミットを探す
特定の文字列にマッチするコミットメッセージだけを表示させるには、`git log --grep`スイッチを使います。

## 使用例
`Fix`の文字列が含まれているコミットを見つける
- `--grep=検索したい文字列`
```bash
$ git log --grep=Fix

commit b93d9bcf41deefc93306cbc1d77b049ac044db6f
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Sat Apr 3 10:18:57 2021 +0900

    Fix EnemyInfo.cs to Load Json

commit 9dab8e9f4d6c49c912b138a6e0a7d53f210762c7
Author: daiki_iijima <daiki.applecreate@gmail.com>
Date:   Tue Mar 30 08:54:42 2021 +0900

    Fix EnemyManager.cs Downcast Error

commit 9140b13f20ee6aa20a1c7d519fce99f1dca447cf
Author: daiki_iijima <daiki.applecreate@gmail.com>
Date:   Tue Mar 30 08:54:01 2021 +0900

    Fix Mat_Orca.mat

```

# 特定の文字列を含むファイルを探す
特定の文字列を含むファイルを探している場合は、`git grep`コマンドを使います。

## 使用例
`Orca`を含むファイルを探す
- 検索するファイル名を指定する必要はなく、リポジトリ内のすべてのファイルから検索してくれる
- 表示される内容 = ファイル名:指定した文字列を含んでいる１行
```bash
$ git grep Orca

GitHubでブログを作成する.md:title: GitHubでブログを作成する(Hexo)
GitHubでブログを作成する.md:- [GitHub]
GitHubでブログを作成する.md:## 3. HexoにGit操作用ツールを追加
GitHubでブログを作成する.md:# GitHubでブログ用のリポジトリを作成する
GitHubでブログを作成する.md:username = GitHubのユーザー名
```
