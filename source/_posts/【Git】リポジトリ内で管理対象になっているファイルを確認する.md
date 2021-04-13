---
title: 【Git】リポジトリ内で管理対象になっているファイルを確認する
date: 2021-04-09 14:10:09
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# リポジトリ内で管理されているファイルを確認する
`ls-tree`を使用することでコミットに含まれる`ツリー(ファイル一覧)`を確認できます

## 基本構文
- ブランチ名を指定すると、そのブランチのHEADのコミットに含まれるファイル群が表示されます
- SHA1を指定すると、指定したSHA1のコミット内の含まれるファイル群が表示される

```shell-session
$ git ls-tree ブランチ名
$ git ls-tree SHA1
```

## 使用例
実行結果
```shell-session
$ git ls-tree master

100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    3
100644 blob 9f4d9b6328248146d622d475135476dd39543f36    "3.6\350\252\262\351\241\214.md"
100644 blob 3a6f51dce8200cbb4b00e8512cecf78de0d4c1b9    "7.5\350\252\262\351\241\214.md"
100644 blob 5f3cf6dbab2950c0b8fe5b6588e905047c06de1b    "8.5\350\252\262\351\241\214.md"
100644 blob 87b9d68a3644de01b90a511f5d680dc85d155433    "9.5\350\252\262\351\241\214.md"
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    another_rename
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    e
100644 blob 233721e585933377d91bdbb18556a991dcca8c47    math.sh
100644 blob 36de8a228bebca6e1d2d43e3fe7f2a260299a6d6    out.txt
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    test
```

表示される文字列の意味
```
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    3
```
- 100644 : 型(100644=通常ファイル,100755=実行可能ファイル)
- blob(ブロブ) : ファイルを表現するデータ構造名
- e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 : ファイルのSHA1
- 3 : ファイル名


