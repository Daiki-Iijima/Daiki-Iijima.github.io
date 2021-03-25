---
title: VimにPluginマネージャー「Vundle」を入れる
date: 2021-02-17 22:33:59
tags: Vim
---
# 環境
- Mac MacBook Air (M1, 2020) 
- OS Big Sur v11.0.1
- VIM - Vi IMproved 8.2 (2019 Dec 12, compiled Oct 29 2020 23:33:57)

# 手順
## 1. ホームディレクトリにフォルダを作る
```
mkdir -p ~/.vim/bundle/Vundle.vim
```
## 2. GitHubからダウンロード
```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

## 3. .vimrcにの先頭に設定を記述
```
set nocompatible
filetype off
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

Plugin 'VundleVim/Vundle.vim'

" 導入したいプラグインを以下に列挙
" Plugin '[Github Author]/[Github repo]' の形式で記入
Plugin 'airblade/vim-gitgutter'

call vundle#end()
filetype plugin indent on

"　その他のカスタム設定を以下に書く
```

## 4. vimを開いた状態でコマンドを打ってインストール
```
:PluginInstall
```
