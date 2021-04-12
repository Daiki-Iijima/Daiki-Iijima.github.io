---
title: 【Git】マージの中止の仕方
date: 2021-04-04 02:30:38
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# 他のブランチを今いるブランチに取り込む(マージを実行する)
`merge`コマンドを使用して、`今いるブランチ`に他のブランチを取り込みます

この実行結果は一例です。
```shell-session
$ git merge test

Updating ace754e..e187324
Fast-forward
 test4 | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test4
```

# マージ時のFast-forwardを行わないようにする
`merge`コマンドを使用して、特定の条件を満たすと、gitはデフォルトで`Fast-foward`というマージを行う
- Fast-forwardとは端的に説明すると、コミットをマージ履歴を残さずに、マージを行うこと


`--no-ff`スイッチを使用することで、`Fast-foward`を行わないように指定することができる
```shell-session
$ git merge --no-ff test

Merge made by the 'recursive' strategy.
 ttt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 ttt
```

# マージを中断する
`--abort`スイッチを使うことでマージを中断できる

```shell-session
$ git merge --abort
```

# 現在のマージ状態を確認する
`--abort`スイッチで中断する前に、`diff`コマンドで現状をチェックすることをおすすめする

```shell-session
$ git diff

diff --cc test.txt
index 5584d95,928dd0d..0000000
--- a/test.txt
+++ b/test.txt
@@@ -1,1 -1,1 +1,5 @@@
++<<<<<<< HEAD
 +テスト次郎
++=======
+ 侍ミーテスト太郎
++>>>>>>> test
```

# マージするブランチとの共通の親を表示させる
ブランチはどこかで共通祖先(the common ancestor)になるコミットがある

ブランチの共通祖先を見つけるには`merge-base`コマンドを使用する

```shell-session
$ git merge-base

ebfae41584feeb6055f2257e9eb409d97e76b9b9
```
