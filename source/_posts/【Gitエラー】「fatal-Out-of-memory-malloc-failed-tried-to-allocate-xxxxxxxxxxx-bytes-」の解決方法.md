---
title: >-
  【Gitエラー】「fatal: Out of memory, malloc failed (tried to allocate xxxxxxxxxxx
  bytes)」の解決方法
date: 2021-02-25 22:48:44
tags:
- Git
---
## 原因
ファイル容量の大きいGitリポジトリをチェックアウトしようとしたら起きたので、Gitの解凍処理でメモリが食い尽くされているのが原因らいしい

## 解決策
解凍処理を小分けにする

`~/.gitconfig`に以下を追記する
```
[core]
packedGitLimit = 128m
packedGitWindowSize = 128m

[pack]
deltaCacheSize = 128m
packSizeLimit = 128m
windowMemory = 128m
```
