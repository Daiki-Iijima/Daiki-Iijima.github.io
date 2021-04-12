---
title: 【Git】小分けにcommitするために使えるコマンド
date: 2021-04-07 23:58:29
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# 「git add .」したらどのファイルがステージングされるかをチェックする
- `git add --dray-run .`
	- 実際には、コミットされず`git add .`をしたらどうなるのかを表示してくれる

```shell-session
$ git add --dray-run .
```

# ハンクを活用する
## ハンクとは
ハンクとはハンドピック(handpick)の略語で、同じファイル内で１つの修正のみの場合は、ファイルをそのまま`add->commit`すればいいが、実際は１つのファイル内で１つ以上の修正を行うケースが多い。それをステージング時に選択してコミットできるようにする機能。

## 実際に使ってみる
サンプルのために以下の内容が記述されている`hunkテスト`ファイルを作成した。
このファイルは事前にコミットしておく。

```
これは元からあった文章1
これは元からあった文章2
これは元からあった文章3
これは元からあった文章4
これは元からあった文章5
これは元からあった文章6
これは元からあった文章7
```

### 1. ファイルの編集
以下の内容に`hunkテスト`を編集する
```
これは元からあった文章1
これは元からあった文章22
これは元からあった文章3
これは元からあった文章4
これは元からあった文章5
これは元からあった文章66
これは元からあった文章7
```

### 2. 1箇所の変更だけをコミットする
今回は`これは元からあった文章です22`の変更だけをコミットしてみる
```
$ git add -p

diff --git "a/hunk\343\203\206\343\202\271\343\203\210" "b/hunk\343\203\206\343\202\271\343\203\210"
index 5c85024..af74fd5 100644
--- "a/hunk\343\203\206\343\202\271\343\203\210"
+++ "b/hunk\343\203\206\343\202\271\343\203\210"
@@ -1,7 +1,7 @@
 これは元からあった文章1
-これは元からあった文章2
+これは元からあった文章22
 これは元からあった文章3
 これは元からあった文章4
 これは元からあった文章5
-これは元からあった文章6
+これは元からあった文章66
 これは元からあった文章7
(1/1) Stage this hunk [y,n,q,a,d,s,e,?]?
```

一番下の行の、`(1/1) Stage this hunk [y,n,q,a,d,s,e,?]?`の小文字たちの意味を以下にまとめています。
| 文字 | 解説                            | 
|----|-------------------------------| 
| y  | このハンクはステージングする                | 
| n  | このハンクはステージングしない               | 
| q  | 終了する                          | 
| a  | このファイルのハンクを含むすべてのハンクをステージングする | 
| d  | このファイルのハンクを含む全てのハンクをステージングしない | 
| s  | 現在のハンクをもっと小さなハンクに分割する         | 
| e  | 現在のハンクを手動で編集する                | 
| ?  | ヘルプを表示する                | 

今回は手動で細かく選択するので、`e`を選択する。選択すると次のような編集画面が現れる
```
# Manual hunk edit mode -- see bottom for a quick guide.
@@ -1,7 +1,7 @@
 これは元からあった文章1
-これは元からあった文章2
+これは元からあった文章22
 これは元からあった文章3
 これは元からあった文章4
 これは元からあった文章5
-これは元からあった文章6
+これは元からあった文章66
 これは元からあった文章7
# ---
# To remove '-' lines, make them ' ' lines (context).
# To remove '+' lines, delete them.
# Lines starting with # will be removed.
# 
# If the patch applies cleanly, the edited hunk will immediately be
# marked for staging.
# If it does not apply cleanly, you will be given an opportunity to
# edit again.  If all lines of the hunk are removed, then the edit is
# aborted and the hunk is left unchanged.
```

一番左の列が１文字分空間が空いていて。そこの変更があった行に文字が書かれている。今回は、`2`を`22`に書き換えた履歴だけを残したいので、以下のような内容に書き換える
- 下の方に書いてある操作方法の日本語訳
	- `-`の行を消すには、その行を` `(スペース)に変える
	- `+`の行を消すには、その行を消去する
	- #で始まる行は、消される。(#から始まる行は気にしなくていい)

```
# Manual hunk edit mode -- see bottom for a quick guide.
@@ -1,7 +1,7 @@
 これは元からあった文章1
-これは元からあった文章2
+これは元からあった文章22
 これは元からあった文章3
 これは元からあった文章4
 これは元からあった文章5
 これは元からあった文章6
 これは元からあった文章7
# ---
# To remove '-' lines, make them ' ' lines (context).
# To remove '+' lines, delete them.
# Lines starting with # will be removed.
# 
# If the patch applies cleanly, the edited hunk will immediately be
# marked for staging.
# If it does not apply cleanly, you will be given an opportunity to
# edit again.  If all lines of the hunk are removed, then the edit is
# aborted and the hunk is left unchanged.
```

変更内容を保存して、編集ツールを抜けると、自動で残しておいた部分がステージングされる

### 3. git diff --stagedでステージングされている変更を見てみる
```shell-session
$ git diff --staged

diff --git "a/hunk\343\203\206\343\202\271\343\203\210" "b/hunk\343\203\206\343\202\271\343\203\210"
index 5c85024..cc9784e 100644
--- "a/hunk\343\203\206\343\202\271\343\203\210"
+++ "b/hunk\343\203\206\343\202\271\343\203\210"
@@ -1,5 +1,5 @@
 これは元からあった文章1
-これは元からあった文章2
+これは元からあった文章22
 これは元からあった文章3
 これは元からあった文章4
 これは元からあった文章5
```

