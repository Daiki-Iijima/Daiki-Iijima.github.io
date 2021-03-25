---
title: zshとaliasについて
date: 2021-02-16 09:44:35
tags: 
- zsh
- alias
---
# zshとは
- 読み方: ズィーシェル
- シェルの一種で`bash`の進化版

https://ja.wikipedia.org/wiki/Z_Shell

## シェルとは
- カーネルと対話するためのインターフェイス
	- シェルの名前の由来は、カーネルを包み込んでいることに由来する
- カーネルの中に入力機能を入れない理由
	- シェル(ロジック)とカーネル(インターフェイス)を分けることでインターフェイスを他のカーネルでも使いまわすことができるようになる
	- インターフェイスのエラーでカーネルをクラッシュする可能性を排除できる

https://recruit.cct-inc.co.jp/tecblog/os/shell/

# aliasとは
- シェル上で、長いコマンドや一連のコマンドをまとめて、ひとまとめにすることのできる機能

# 使い方(zshの場合)
1. `~/.zshrc`に記述する
	```zsh
	alias 別名='本来のコマンド'
	```
2. 保存して`.zshrcL`の再読み込みをする
	```zsh
	source ~/.zshrc
	```
3. `別名`で指定したコマンドを打って期待通り動けばOK

## 使用例
- 長いパスのフォルダに移動`cd`したい場合
	- このコマンド`bc`を打つだけで記述した`cd`コマンドが実行される
	```zsh
	alias bc='cd /Users/daiki/Desktop/Blog/Daiki-Iijima.github.io/source/_posts'
	```

# 複数のコマンドを1つのaliasにまとめる
- 各コマンドを`;`で区切ることで連続したコマンドを記述できる
	```zsh
	alias 別名='コマンド1;コマンド2'
	```
## 使用例
- デスクトップへ移動して、`test`フォルダを生成する
	```zsh
	alias cdmk='cd /Users/daiki/Desktop;mkdir test'
	```

# 引数を渡す
- `$`+`数字`を本来の引数があるはずの位置に記述することで、引数を渡すことができる
	```zsh	
	alias 別名='mkdir $1'
	```
	- 使用する場合
		```zsh
		別名 引数
		```
- 複数の引数を渡したい場合は、`$`の後の`数字を`繰り上げていく
	```zsh
	alias 別名='mkdir $1;mkdir $2'
	```
	- 使用する場合
		```zsh
		別名 引数 引数
		```

## 使用例
- メモをとるためにディレクトリとディレクトリの中にディレクトリと同名の`.md`ファイルをvimで編集する
```zsh
alias memo='(){cd /Users/daiki/Desktop/memo;mkdir $1;vim $1.md}'
```
# 参照リンク
- [シェルの設定ファイルを再読み込み](http://norizo333.hatenablog.com/entry/20090921/1253523438)
- [bashで複数のコマンドエイリアス](https://qiita.com/mikakane/items/ac27582e8e52228adced)
- [zsh環境で引数を持ったコマンドを作る](https://qiita.com/sayama0402/items/46241c07c30e431fe38f)
- [【時短】zshでエイリアスを設定する方法](https://qiita.com/terufumi1122/items/1bbb1cf96e376e30e9fc)
