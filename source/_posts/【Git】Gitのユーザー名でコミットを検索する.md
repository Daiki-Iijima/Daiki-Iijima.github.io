---
title: 【Git】Gitのユーザー名でコミットを検索する
date: 2021-05-16 01:12:22
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# 2通りの方法がある
`author`,`committer`オプションのどちらかを使用するオプションがある

- `author` : オリジナルのコードを記述した人
- `committer` : コミットを適応した人

## author
```bash
git log --author="ユーザー名"
```

## committer 
```bash
git log --committer="ユーザー名"
```

## authorとcommiterの違い
`author`はコードの変更を実際に行った人を示していて、基本的にすべてのコミットは、`author`を検索すれば誰が変更したかを探せる。

`committer`を使用すると、`amend`オプションや、`rebase`オプションをしようした場合に、書き換わってしまうので、実際の変更をしている人を探す場合には向かない。

`author`を書き換える事もできるので、これをされたらすべての手柄を持っていかれる

## 普段のgit logはコミットauthorを表示している
`committer`と`author`のどちらも表示したい場合、`pretty`オプションに`fuller`を設定する

```bash
git log --pretty=fuller
```
