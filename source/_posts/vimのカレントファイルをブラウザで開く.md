---
title: vimのカレントファイルをブラウザで開く
date: 2021-02-22 22:35:42
tags:
- Vim
---
## openコマンドを使う
- vimでは`%`でカレントファイルのパスを取得できる
- `!`はOS用のコマンド(`echo`や`pwd`など)の先頭につけることで`vimエディタ`上からOS用コマンドを実行することができる
- `open`はファイルのデフォルトで開くソフトに設定されているソフトで開かれる

```
:!open %
```

## 入力の手間を減らす
- これまでのコマンドをショートカットキーで呼び出せるように`.vimrc`に追記する

```
" スペースキーをショートカットのトリガーとして認識するように設定
let mapleader = "\<Space>" 

"	スペースキー + o で実行できる
nnoremap <Leader>o :!open %<CR>
```

## フォーカスを戻す(Mac)
- `open`コマンドを使うとフォーカスがブラウザになってしまうので、`AppleScript`を使ってフォーカスをVim(iTerm)に戻す
	- `terminal_focus`の対象アプリを変更すればiTerm以外のソフトにも対応可能

~/.vim/plugin/BrowserOpen.vim
```
command! -bar BrowserOpen !open % | osascript $HOME/bin/terminal_focus.scpt
```

~/bin/terminal_focus.scpt
```
tell application "iTerm" to activate
```

~/.vimrc
```
" スペースキーをショートカットのトリガーとして認識するように設定
let mapleader = "\<Space>" 

"	スペースキー + o で実行できる
nnoremap <Leader>o :BrowserOpen<CR>
```
