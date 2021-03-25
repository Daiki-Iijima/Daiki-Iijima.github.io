---
title: AppleScriptでVimの保存時のファイル更新を取得してブラウザを更新する
date: 2021-02-21 11:41:11
tags: 
- Vim
- AppleScript
- 自動化
---
# 概要
Vimでファイルを保存した時にファイルをブラウザで開いている場合(HTMLを書いている場合など)、いちいちブラウザにフォーカスを当てて、ブラウザ再読み込みを行うのは面倒くさいので、

1. ブラウザにフォーカスを当てる
2. `command + r`イベントを発行
3. フォーカスをターミナルに戻す

の動作を自動化する

## Vimで使用するコマンドを実装する
1. `/Users/daiki/.vim/plugin`に`chrome.vim`を配置
	- ディレクトリがない場合は作成する
2. 以下のコードを`chrome.vim`に書き込んで保存

`chrome.vim`
```
command! -bar ChromeReload silent !osascript $HOME/bin/chrome_reload.scpt && osascript $HOME/bin/terminal_focus.scpt
command! -bar ChromeStartObserve ChromeStopObserve | autocmd BufWritePost <buffer> ChromeReload
command! -bar ChromeStopObserve autocmd! BufWritePost <buffer>
```

## ブラウザにフォーカスを当ててリロードするコマンドを実装
1. `/Users/daiki/bin`に`chrome_reload.scpt`を配置
	- ディレクトリがない場合は作成する 
2. 以下のコードを`chrome_reload.scpt`に書き込んで保存
### カスタマイズ
- 1行目:`tell application "safari" to activate`の`safari`の部分を別のブラウザの名前に変更すると開くブラウザを変更できる

`chrome_reload.scpt`
```
tell application "safari" to activate
tell application "System Events" to keystroke "r" using {command down}
```

## ターミナルにフォーカスを戻すコマンド 
1. `/Users/daiki/bin`に`terminal_focus.scpt`を配置
	- ディレクトリがない場合は作成する 
2. 以下のコードを`terminal_focus.scpt`に書き込んで保存
### カスタマイズ
- `"Terminal"`の部分を書き換えると別アプリにフォーカスを当てられる

`terminal_focus.scpt`
```
tell application "Terminal" to activate
```

## Vimで使用するには
vimを開いて、ブラウザで更新したいファイルに対して以下のコマンドを打つ

- `:ChromeReload`:１回ブラウザをリロードする
- `:ChromeStartObserve`:Vimで保存するたびにブラウザをリロードする
- `:ChromeStopObserve`:`ChromeStartObserve`の保存時の自動リロードを停止する

# 参考
https://lukesilvia.hatenablog.com/entry/20101023/p2
