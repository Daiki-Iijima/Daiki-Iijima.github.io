---
title: 【Zsh】Zsh拡張フレームワーク「Prezto」
date: 2021-03-09 22:16:00
tags:
- Zsh
---
## 参考
- https://github.com/sorin-ionescu/prezto
- https://qiita.com/s_of_p/items/33c9b18f0dc47ce29024
- https://qiita.com/yasudanaoya/items/8b928cfadbf702108ba3

## インストール方法
### 1. Zshを起動する
```shell-session
$ zsh
```

### 2. リポジトリをクローンする
- `${ZDOTDIR:-$HOME}`とは？
	- `$ZDOTDIR` : `.zshrc`の保存場所を設定する環境変数
	- `$HOME` : ホームディレクトリ
	- `:-` : 左辺の値が設定されていor空文字列であれば、右辺に設定されてる値が使用される
```shell-session
$ git clone --recursive https://github.com/sorin-ionescu/prezto.git "${ZDOTDIR:-$HOME}/.zprezto"
```

### 3. 今まで使っていた設定ファイルを移動させる
```shell-session
$ mkdir zsh_orig && mv zshmv .zlogin .zlogout .zprofile .zshenv .zshrc zsh_orig
```

### 4. 各コンフィグファイルへのシンボリックリンクを作成する
```shell-session
$ setopt EXTENDED_GLOB
for rcfile in "${ZDOTDIR:-$HOME}"/.zprezto/runcoms/^README.md(.N); do
  ln -s "$rcfile" "${ZDOTDIR:-$HOME}/.${rcfile:t}"
done
```

### 5. zshをデフォルトシェルに設定
- chsh : ログインシェルを変更する
```shell-session
$ chsh -s /bin/zsh
```

## テーマの設定
### テーマ一覧を見てみる
```
$ prompt -s
```

### テーマを設定する
```
$ prompt -s テーマ名
```
#### Macの場合
`prompt -s`だと、そのセッションではテーマが変更されるが、再起動ログインし直すとデフォルトのテーマになってしまうので、設定`~/.zshrc`に追記しておく必要がある
```
$ prompt -s powerline
Set and save not yet implemented.  Please ensure your ~/.zshrc
contains something similar to the following:

  autoload -Uz promptinit
  promptinit
  prompt powerline
```

#### powerlineを使用する場合、特殊なフォントが必要
1. 以下GitHubのリポジトリをダウンロード
https://github.com/powerline/fonts

- 適当なディレクトリに移動後
	```
	git clone https://github.com/powerline/fonts.git
	```

2. `install.sh`を叩く
	```
	$ cd fonts
	$ ./install.sh
	```

3. 使用しているターミナルでフォントを設定
- 文字列に`Powerline`が入っていれば使えるはず

