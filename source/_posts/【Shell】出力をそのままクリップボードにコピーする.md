---
title: 【Shell】出力をそのままクリップボードにコピーする
date: 2021-03-04 02:40:23
tags:
- Shell
---
# 出力をクリップボードにコピーする
`|(パイプ)`+`pbcopy`
- `pb`とは`past board`の略

# 使用例
## カレンとディレクトリのパスをクリップボードにコピーする
```shell
pwd | pbcopy
```

## ファイルの内容をクリップボードにコピー
```shell
cat ファイル名 | pbcopy
```

# 追記
## 2021/3/6 
zshには、aliasで`pbc`が設定されているらしく、こっちの方が短くかける
- 動作的には、aliasなので`pbcopy`と同じ
```shell-session
cat ファイル名 | pbc
```
