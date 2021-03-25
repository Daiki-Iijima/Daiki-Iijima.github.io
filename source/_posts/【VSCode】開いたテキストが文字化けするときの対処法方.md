---
title: 【VSCode】開いたテキストが文字化けするときの対処法方
date: 2021-03-10 00:44:32
tags:
- VSCode
---
## 設定の「自動文字コード識別設定」をONにする

### 1. Settings画面を開く
`Code -> Preferences -> Settings`の順でSettings画面を開く
	- `Cmd + ,(カンマ)`でも開ける

![Settings](/2021/03/10/【VSCode】開いたテキストが文字化けするときの対処法方/Settings.png "Settings")


### 2. 自動文字コード識別設定を探す
検索欄から、「autoGuessEncoding」を検索

![Search](/2021/03/10/【VSCode】開いたテキストが文字化けするときの対処法方/Search.png "Search")

### 3.「Files:Auto Guess Encoding」にチェックを入れる
再度ファイルを開き直せば、文字化けが解消されているはず
