---
title: 【Git】ログに更新情報も一緒に表示させる
date: 2021-04-11 11:03:52
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# ファイル名とどれくらい変更されたかを知りたいとき
`git log --stat`を使うと、ファイル名と変更量(追加or消去)を表示する
- 変更が0でファイル名が表示されている場合は、中身のないファイルが新規に作成されている

```shell-session
ファイル名 | 変更点カウント 変更箇所の概要(+ or -)
何個のファイルが変更されたか、追記された行数(+),消去された行数(-)
```

## 実際の実行画面
```shell-session
$ git log --stat

commit 24f2afa3e2e06e33a912525ad7c85b2791e07de7
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Thu Mar 4 12:43:41 2021 +0900

    Adding two numbers

 math.sh | 4 +++-
 1 file changed, 3 insertions(+), 1 deletion(-)
``` 
