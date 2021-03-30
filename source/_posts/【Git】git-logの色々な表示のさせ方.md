---
title: 【Git】git logの色々な表示のさせ方
date: 2021-03-26 00:42:00
tags:
- Git
---
## 目次
<!-- toc -->
<!-- more -->

## はじめに
ここで紹介しているスイッチ(--から始まる文節)はすべて組み合わせて使用する事ができるので、適時用途にあった表示のさせ方で組み合わせるといいと思います。

## この記事で紹介するスイッチ
- `--oneline` : 短く表示する
- `--stat` : 変更のあったファイル名と、ファイル数を表示する
- `--graph`	: 視覚的に表示する
- `--all` : すべてのブランチを表示する

## 普通に「git log」
### 表示される内容
- SHA1
- ブランチのHEADの場合、ブランチの情報
- コミットした`ユーザー名``メールアドレス`
- コミットした日付
- コミットメッセージ全文

```shell-session
$ git log 

commit c7cfec983e47d507b89726b1fcb8550ea71eee95 (HEAD -> master, beginning/master, beginning/HEAD)
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 23:20:18 2021 +0900

    A small update to readme.

commit 895ded5c28bfa9848f647eff1339dcc763f910d1
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 20:20:18 2021 +0900

    Adding printf.

    This is to make the output a little more human readable.

    printf is part of BASH, and it works just like C's printf()
    function.

commit 5ab2e41e28507359a1774e39be287406707d3ec8
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 09:20:18 2021 +0900

    Adding two numbers.

commit 004e3a3d1f942361d81ec6599e6bff0f6c0d7be9 (beginning/another_fix_branch)
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 08:20:18 2021 +0900

    Renaming c and d.

commit fd3bb1d565b69ca19832f8892030a40d6961076c
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 07:20:18 2021 +0900

    Removed a and b.

commit 6e0d6f43f601fac104439dd778160aeef0ab9910
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Thu Mar 11 09:20:18 2021 +0900

    Adding readme.txt

commit a343843ff5496451e855e4064a4c138cc7b3105e (tag: four_files_galore)
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Tue Mar 9 09:20:18 2021 +0900

    Adding four empty files.

commit 834601bc8cfa381dbb3ffc4a30245646194b297b
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Tue Mar 9 08:20:18 2021 +0900

    Adding b variable.

commit 68d38c6348b0cf53655e01ef9c8238457b709c71
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Tue Mar 9 07:20:18 2021 +0900

    This is the second commit.

commit d314c772bb58ed3d959bf658265986b7c50bcd61
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Tue Mar 9 05:20:18 2021 +0900

    This is the first commit.
```

## 短く表示させる「git log --oneline」
### 表示される内容
- ７桁に短縮された`SHA1`
- ブランチのHEADの場合、ブランチの情報
- コミットコメント(１行目のみ)

```shell-session
$ git log --oneline

c7cfec9 (HEAD -> master, beginning/master, beginning/HEAD) A small update to readme.
895ded5 Adding printf.
5ab2e41 Adding two numbers.
004e3a3 (beginning/another_fix_branch) Renaming c and d.
fd3bb1d Removed a and b.
6e0d6f4 Adding readme.txt
a343843 (tag: four_files_galore) Adding four empty files.
834601b Adding b variable.
68d38c6 This is the second commit.
d314c77 This is the first commit.
```

## 変更されたファイルを表示する「git log --stat」
### 表示される内容
- `git log`を使用したときに表示される情報
- 変更されたファイル名とカウント

```shell-session
$ git log --stat

commit c7cfec983e47d507b89726b1fcb8550ea71eee95 (HEAD -> master, beginning/master, beginning/HEAD)
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 23:20:18 2021 +0900

    A small update to readme.

 readme.txt | 1 +
 1 file changed, 1 insertion(+)

commit 895ded5c28bfa9848f647eff1339dcc763f910d1
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 20:20:18 2021 +0900

    Adding printf.

    This is to make the output a little more human readable.

    printf is part of BASH, and it works just like C's printf()
    function.

 math.sh | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

commit 5ab2e41e28507359a1774e39be287406707d3ec8
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 09:20:18 2021 +0900

    Adding two numbers.

 math.sh | 4 +++-
 1 file changed, 3 insertions(+), 1 deletion(-)

commit 004e3a3d1f942361d81ec6599e6bff0f6c0d7be9 (beginning/another_fix_branch)
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 08:20:18 2021 +0900

    Renaming c and d.

 c => another_rename | 0
 d => renamed_file   | 0
 2 files changed, 0 insertions(+), 0 deletions(-)

commit fd3bb1d565b69ca19832f8892030a40d6961076c
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 07:20:18 2021 +0900

    Removed a and b.

 a | 0
 b | 0
 2 files changed, 0 insertions(+), 0 deletions(-)

commit 6e0d6f43f601fac104439dd778160aeef0ab9910
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Thu Mar 11 09:20:18 2021 +0900

    Adding readme.txt

 readme.txt | 1 +
 1 file changed, 1 insertion(+)

commit a343843ff5496451e855e4064a4c138cc7b3105e (tag: four_files_galore)
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Tue Mar 9 09:20:18 2021 +0900

    Adding four empty files.

 a | 0
 b | 0

...
```

## 短く表示させつつ、変更されたファイルを表示する「git log --oneline --stat」
### 表示される内容
- `git log --oneline`を使用したときに表示される情報
- 変更されたファイル名とカウント

```shell-session
$  git log --oneline --stat

c7cfec9 (HEAD -> master, beginning/master, beginning/HEAD) A small update to readme.
 readme.txt | 1 +
 1 file changed, 1 insertion(+)
895ded5 Adding printf.
 math.sh | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
5ab2e41 Adding two numbers.
 math.sh | 4 +++-
 1 file changed, 3 insertions(+), 1 deletion(-)
004e3a3 (beginning/another_fix_branch) Renaming c and d.
 c => another_rename | 0
 d => renamed_file   | 0
 2 files changed, 0 insertions(+), 0 deletions(-)
fd3bb1d Removed a and b.
 a | 0
 b | 0
 2 files changed, 0 insertions(+), 0 deletions(-)
6e0d6f4 Adding readme.txt
 readme.txt | 1 +
 1 file changed, 1 insertion(+)
a343843 (tag: four_files_galore) Adding four empty files.
 a | 0
 b | 0
 c | 0
 d | 0
 4 files changed, 0 insertions(+), 0 deletions(-)
834601b Adding b variable.
 math.sh | 1 +
 1 file changed, 1 insertion(+)
68d38c6 This is the second commit.
 math.sh | 1 +
 1 file changed, 1 insertion(+)
d314c77 This is the first commit.
 math.sh | 1 +
 1 file changed, 1 insertion(+)
```

## 視覚的にわかりやすく表示する「git log --graph」
### 表示される内容
- `git log`を使用したときに表示される情報
- コミットやブランチの流れを`ASCII`文字で表現する

```shell-session
$ git log --graph
* commit c7cfec983e47d507b89726b1fcb8550ea71eee95 (HEAD -> master, beginning/master, beginning/HEAD)
| Author: Daiki-Iijima <daiki.applecreate@gmail.com>
| Date:   Fri Mar 12 23:20:18 2021 +0900
|
|     A small update to readme.
|
* commit 895ded5c28bfa9848f647eff1339dcc763f910d1
| Author: Daiki-Iijima <daiki.applecreate@gmail.com>
| Date:   Fri Mar 12 20:20:18 2021 +0900
|
|     Adding printf.
|
|     This is to make the output a little more human readable.
|
|     printf is part of BASH, and it works just like C's printf()
|     function.
|
* commit 5ab2e41e28507359a1774e39be287406707d3ec8
| Author: Daiki-Iijima <daiki.applecreate@gmail.com>
| Date:   Fri Mar 12 09:20:18 2021 +0900
|
|     Adding two numbers.
|
* commit 004e3a3d1f942361d81ec6599e6bff0f6c0d7be9 (beginning/another_fix_branch)
| Author: Daiki-Iijima <daiki.applecreate@gmail.com>
| Date:   Fri Mar 12 08:20:18 2021 +0900
|
|     Renaming c and d.
|
* commit fd3bb1d565b69ca19832f8892030a40d6961076c
| Author: Daiki-Iijima <daiki.applecreate@gmail.com>
| Date:   Fri Mar 12 07:20:18 2021 +0900
|
|     Removed a and b.
|
* commit 6e0d6f43f601fac104439dd778160aeef0ab9910
| Author: Daiki-Iijima <daiki.applecreate@gmail.com>
| Date:   Thu Mar 11 09:20:18 2021 +0900
|
|     Adding readme.txt
|
...
```

## 短く視覚的に表示する「git log --oneline --graph」
### 表示される内容
- `git log --oneline`を使用したときに表示される情報
- コミットやブランチの流れを`ASCII`文字で表現する

```shell-session
$ git log --oneline --graph

* c7cfec9 (HEAD -> master, beginning/master, beginning/HEAD) A small update to readme.
* 895ded5 Adding printf.
* 5ab2e41 Adding two numbers.
* 004e3a3 (beginning/another_fix_branch) Renaming c and d.
* fd3bb1d Removed a and b.
* 6e0d6f4 Adding readme.txt
* a343843 (tag: four_files_galore) Adding four empty files.
* 834601b Adding b variable.
* 68d38c6 This is the second commit.
* d314c77 This is the first commit.
```

## すべてのブランチを見る「git log --all」
### 表示される内容
- `git log`を使用したときに表示される情報
- カレントブランチ以外のブランチのlogを一緒に表示する

```shell-session
$ git log --oneline --graph

commit c7cfec983e47d507b89726b1fcb8550ea71eee95 (HEAD -> master, beginning/master, beginning/HEAD)
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 23:20:18 2021 +0900

    A small update to readme.

commit 91d6184f4c6da852bbcddf9d3c4155983a416d35 (beginning/new_feature)
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 22:20:18 2021 +0900

    Starting a second new file

commit af9aa8ef34be4a5f1c36eb06a560638cc730c814
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 21:20:18 2021 +0900

    Adding a new file to a new branch

commit 895ded5c28bfa9848f647eff1339dcc763f910d1
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 20:20:18 2021 +0900

    Adding printf.

    This is to make the output a little more human readable.

    printf is part of BASH, and it works just like C's printf()
    function.

commit 5ab2e41e28507359a1774e39be287406707d3ec8
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 09:20:18 2021 +0900

    Adding two numbers.

commit 004e3a3d1f942361d81ec6599e6bff0f6c0d7be9 (beginning/another_fix_branch)
Author: Daiki-Iijima <daiki.applecreate@gmail.com>
Date:   Fri Mar 12 08:20:18 2021 +0900

    Renaming c and d.
...
```

## 短く視覚的に表示する「git log --oneline --all」
### 表示される内容
- `git log --oneline`を使用したときに表示される情報
- カレントブランチ以外のブランチのlogを一緒に表示する

```shell-session
$ git log --oneline --all

c7cfec9 (HEAD -> master, beginning/master, beginning/HEAD) A small update to readme.
91d6184 (beginning/new_feature) Starting a second new file
af9aa8e Adding a new file to a new branch
895ded5 Adding printf.
5ab2e41 Adding two numbers.
004e3a3 (beginning/another_fix_branch) Renaming c and d.
fd3bb1d Removed a and b.
6e0d6f4 Adding readme.txt
a343843 (tag: four_files_galore) Adding four empty files.
834601b Adding b variable.
68d38c6 This is the second commit.
d314c77 This is the first commit.
```
