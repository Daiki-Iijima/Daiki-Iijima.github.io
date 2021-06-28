---
title: 【Vim】phpファイルにHTMLを記述した際にオートインデントが効かないので対策する
date: 2021-05-03 21:21:19
tags:
- PHP
- Vim
---
# 目次
<!-- toc -->
<!-- more -->

# 現象
オートインデントが適応されずに、全て同じインデントでになる
```php
<html>
<head>
<title>hello</title>
<style>
</style>
</head>
<body>
</body>
</html>
```

# 対策
ここのサイトに乗っている方法を実行すればいい感じにオートレイアウトしてくれた。　
- https://vim.fandom.com/wiki/Better_indent_support_for_php_with_html

# 日本語訳すると

## 1. php.vimを作成する
### Mac and Linuxの場合
  - `~/.vim/indent/php.vim`
### Windowsの場合
  - `$HOME/vimfiles/indent/php.vim`

## 2. php.vimに処理を記述する
```vim
" Better indent support for PHP by making it possible to indent HTML sections
" as well.
if exists("b:did_indent")
  finish
endif
" This script pulls in the default indent/php.vim with the :runtime command
" which could re-run this script recursively unless we catch that:
if exists('s:doing_indent_inits')
  finish
endif
let s:doing_indent_inits = 1
runtime! indent/html.vim
unlet b:did_indent
runtime! indent/php.vim
unlet s:doing_indent_inits
function! GetPhpHtmlIndent(lnum)
  if exists('*HtmlIndent')
    let html_ind = HtmlIndent()
  else
    let html_ind = HtmlIndentGet(a:lnum)
  endif
  let php_ind = GetPhpIndent()
  " priority one for php indent script
  if php_ind > -1
    return php_ind
  endif
  if html_ind > -1
    if getline(a:lnum) =~ "^<?" && (0< searchpair('<?', '', '?>', 'nWb')
          \ || 0 < searchpair('<?', '', '?>', 'nW'))
      return -1
    endif
    return html_ind
  endif
  return -1
endfunction
setlocal indentexpr=GetPhpHtmlIndent(v:lnum)
setlocal indentkeys+=<>>
```

## コメント
> 個人的には、HTMLブロックの編集中に :set ft=html とする方がわかりやすいと思います。
>このプラグインは新しいテキストを入力するときには機能しますが、選択範囲に=を使うときには機能しませんよね？これも同じように修正する方法があるのでしょうか？
>この方法をよりすっきりと使いたい人のために、プラグインとしてまとめてみました。

