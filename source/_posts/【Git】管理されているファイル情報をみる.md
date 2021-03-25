---
title: 【Git】管理されているファイル情報をみる
date: 2021-03-07 09:07:32
tags:
- Git
---
## リポジトリで「管理されている」ファイルのリストを取得する
`ls-files`コマンドの`-c`オプションを使用する

`ls-files`はデフォルトで`-c`オプションがついている
> -c, --cached<br>
	Show cached files in the output (default)

### 実行結果例
```shell-session
% git ls-files 
1
2
3
4
aaa
```

## リポジトリで「管理されていない」ファイルのリストを取得する
`ls-files`コマンドの`-o`オプションを使用する

> -o, --others<br>
	Show other (i.e. untracked) files in the output

### 実行結果例
```shell-session
% git ls-files -o
5
bbb
```
