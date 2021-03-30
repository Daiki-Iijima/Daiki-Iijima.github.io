---
title: 【Git】「waring/ LF will be replaced by CRLF in XXX」が出た時の対処法
date: 2021-03-19 01:16:07
tags:
- Git
---
## 目次
<!-- toc -->
<!-- more -->

## この警告はなにか
- Gitが`LF改行コード`を`CRLF改行コード`に自動変換したことによる警告
- WindowsでGitを使用している場合、`git add`したときに表示されることがある

### LF改行コードとCRLF改行コードとはなにか
- LF改行コード
	- LF = Line Feed(改行)
	- カーソルを新しい行に移動させる
	- `Unix`,`Linux`,`macOS(9以降)`などのOSで使用される改行コード

- CRLF改行コード
	- CRLF = CR + LF
	- カーソルを左端の位置に戻し、新しい行に移動すること
	- `Windows`OSで使用されている改行コード

- CR改行コード
	- CR = Carriage Return(復帰)
	- カーソルを左側に戻す
	- macOS(9以前)で使用されている改行コード

## 解決策
windows と widnowsのやり取りしかしない場合は、以下のコードで`waring`を出さないような設定にできるが、CRLF改行コードを使っていないOSとのやり取りがある場合、行末で問題が発生する可能性を検知できなくなる

- gitのconfigの`改行コード自動変換プロパティ`をオフにする

```
git config --global core.autoCRLF false
```

## 参考
- [LFをCRLFに置き換えてもいいのか](https://stackoverflow.com/questions/5834014/lf-will-be-replaced-by-crlf-in-git-what-is-that-and-is-it-important)
- [改行コードについて](https://vba-create.jp/vba-standard-cr-lf-crlf/)
- [LF will be reqlacedについて](https://normalblog.net/system/lf_replaced_crlf/)
