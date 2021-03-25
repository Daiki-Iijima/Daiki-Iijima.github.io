---
title: 【Shell】コマンドラインのカーソル移動
date: 2021-03-10 22:59:26
tags:
- Shell
---
## 矢印キーを使用しないカーソルの移動
- `□`が現在カーソルのある位置

| コマンド     | 動作解説            | 動作前                  | 動作後                  |
|----------|-----------------|----------------------|----------------------|
| Ctrl + a | 行の先頭にカーソルを移動    | cd ~/Deskctop□/test/ | □cd ~/Deskctop/test/ |
| Ctrl + e | 行の末にカーソルを移動     | cd ~/Deskctop□/test/ | cd ~/Deskctop/test/□ |
| Ctrl + k | カーソルの右側を全て消去    | cd ~/Deskctop□/test/ | cd ~/Deskctop□       |
| Ctrl + h | カーソルの左側にある文字を消去 | cd ~/Deskctop□/test/ | cd ~/Deskcto□/test/  |
| Ctrl + d | カーソルの右側にある文字を消去 | cd ~/Deskctop□/test/ | cd ~/Deskctop□test/  |
| Ctrl + u | コマンドラインの文字を全て消去 | cd ~/Deskctop□/test/ |                      |
| Ctrl + y | Ctrl + kで消去した文字列を貼り付け | 								 |                      |

## コマンドの履歴を使用する
- 矢印キーの上下(↑,↓)で一つ前のコマンド、一つ後のコマンドを呼び出せる。

- 履歴を見たい場合は、`history`コマンドでみることのできる
	- 履歴番号　コマンド
	```shell-session
	$ history
	  679  ls
	  680  vim ~/.zshrc
	  681  source ~/.zshrc
	  682  ZDOTDIR
	  683  $ZDOTDIR
	  684  echo $ZDOTDIR
	```

- 行番号を指定して実行する
	- `!履歴番号`
	-	行番号のコマンドがコマンドラインに入力される
	```shell-session
	$ !679

	$ ls
	```

