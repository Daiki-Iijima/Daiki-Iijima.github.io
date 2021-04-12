---
title: 【Git】コミットメッセージのテンプレートを設定する
date: 2021-04-13 22:05:47
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# コミットテンプレートとは
git のコミット時に自動で生成されるコメントを設定することができる機能です。プロジェクト内でコミットメッセージのフォーマットを統一したい場合に使用することがありました。

# テンプレートファイルの用意
任意の場所にテンプレートファイルを用意し、git config でそのファイルをセットする

```bash
$ touch ~/.gitmessage.txt
$ git config --global commit.template ~/.gitmessage.txt
```

```bash
$ touch ~/.gitmessage.txt
$ git config --global commit.template ~/.gitmessage.txt
```

```:.gitmessage.txt
[ticket: #xxxx][Task/Bug] Subject line

what happened
ref : ticket link
```


# 使用例

```
$ git commit

[ticket: #xxxx][Task/Bug] Subject line

what happened
ref : ticket link

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
# modified:   hoge/test.txt
#
```
