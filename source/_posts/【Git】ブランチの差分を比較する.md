---
title: 【Git】ブランチの差分を比較する
date: 2021-04-06 00:41:04
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# ブランチ間の差分をみる

`masterブランチ`と`testブランチ`の差分を比較します。
- `master`と`test`の間の`.`は2つ

比較したブランチをマージする場合、比較した結果通りの結果のマージが行われます。

```shell-sesshion
$ git diff master..test
```

このときに重要なのは、`..`の両端にあるブランチ名の順序です。この順序を変えることで、どちらを元にした差分を表示させるかを決めることができます。

先(左側)に指定した方のブランチを基準に差分を表示します。

## サンプル
masterブランチとtestブランチの比較を基準になるブランチを入れ替えて行います。

以下の手順で差分を発生させた状態を作り比較します。
1. masterブランチでファイル作成コミット(test.txtを作成して1追記)
2. testブランチをHEADから作成
3. testブランチ内でファイルを編集コミット(test.txtに2を記述)
4. masterブランチでファイルを編集コミット(test.txtに3を記述)
5. 比較

### master..test
```shell-sesssion
$ git diff master..test


diff --git a/test.txt b/test.txt
index 2b2f2e1..1191247 100644
--- a/test.txt
+++ b/test.txt
@@ -1,2 +1,2 @@
 1
-3
+2
```

### test..master

```shell-sesssion
$ git diff test..master


diff --git a/test.txt b/test.txt
index 1191247..2b2f2e1 100644
--- a/test.txt
+++ b/test.txt
@@ -1,2 +1,2 @@
 1
-2
+3
```

# ファイル単位でブランチ間の違いをみる
`git diff master...test`を使用するとファイル内のどこがどう違うかを表示できるが、ざっくりとどのファイルに差分があるかだけをみたい場合は、`--name-status`スイッチを使用すれば見ることができる。

```shell-session
$ git diff --name-status master..test

M       test.txt
```

このときにファイル名の右側に表示される文字の意味は以下になる

| 文字 | 意味(英語)   | 意味(日本語) | 
|----|----------|---------| 
| A  | Added    | 追加      | 
| C  | Copied   | コピー     | 
| D  | Deleted  | 消去      | 
| M  | Moudifed | 変更      | 
| R  | Renamed  | リネーム    | 

