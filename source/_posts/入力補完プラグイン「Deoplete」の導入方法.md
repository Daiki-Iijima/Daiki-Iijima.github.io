---
title: 入力補完プラグイン「Deoplete」の導入方法
date: 2021-02-18 09:21:32
tags: 
- Vim
- VimPlugin
---
# vimにdeopleteを入れる

インストールに前提条件の多いPluginなので詰まるところが多かった

# 環境
- M1 Mac 
- macOS Big Sur(11.2)
- vim 8.2

## 公式の手順
- [Shougo/deoplete](https://github.com/Shougo/deoplete.nvim)

# 日本語訳
## 最初に
注意: `deoplete` は`Vim`で使用する場合でも `Neovim` (最新のものを推奨) が必要  
`Vimを使用する場合`Vimバージョン8.1以上 で `Python 3.6.1以上` と`timers`が有効になっている必要がある。

注意: deopleteはmsgpackパッケージ1.0.0+を必要とします。pipでmsgpackパッケージをインストール/アップグレードしてください。  
[msgpack/msgpack-python](https://github.com/msgpack/msgpack-python)

注意: どうしても古い msgpack を使う必要がある場合は、代わりに deoplete ver.5.2 を使ってください。  
[Shougo/deoplete.vim](https://github.com/Shougo/deoplete.nvim/releases/tag/5.2)

## 要件
- neovimをインストールしておく
	```
	pip3 install --user pyvim
	```

- neovimでpython3が有効かを確認
	- nvimを起動して以下のコマンドで`1`が出るか確認
	```
	:echo has("python3")
	```
 
## .vimrcに記述
1. 今回はプラグイン管理ツールの`Vundle`を使用する
	```
	Plugin 'Shougo/deoplete.nvim'
	Plugin 'roxma/nvim-yarp'
	Plugin 'roxma/vim-hug-neovim-rpc'
	```
	```
	" deopleteをVim起動時に有効にする
	let g:deoplete#enable_at_startup = 1
	```

2. `:PluginInstall`でインストール 

## トラブル対応
###  ファイルを開くとエラーが表示される
```
[deoplete] deoplete failed to load. Try the :UpdateRemotePlugins command and restart Neovim. See also :checkhealth.
```
- 参考サイト
[deoplete.nvimのエラー解消](https://blog.fakiyer.com/entry/2018/11/20/101826)
