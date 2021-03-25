---
title: XcodeでVimキーバインドを使う「XVim2」
date: 2021-02-28 12:07:33
tags:
- Vim
- XCode
---

## 目次
1. 証明書の発行
2. XVim2のインストール
3. XcodeにXVim2を読み込ませる
4. .xvimrcでカスタマイズ　
5. 参考

## 1. 証明書の発行
1. アプリケーションの`Keychain Access(キーチェーンアクセス)`を起動
2. `Keychain Access`ウィンドウの左側のデフォルトチェーン内の`ログイン`を選択
3. 画面上部のメニューバーから、`キーチェーンアクセス->証明書アシスタント->証明書を作成`を選択

	![キーチェーン証明書作成](/2021/02/28/XcodeでVimキーバインドを使う「XVim2」/キーチェーン証明書作成.png "キーチェーン証明書作成")
4. 以下と`同じ情報`を設定して、`作成`ボタンを押下
	- 名前 : XcodeSigner
	- 固有名のタイプ : 自己署名ルート
	- 証明書のタイプ : コード署名

	![証明書作成時の入力内容](/2021/02/28/XcodeでVimキーバインドを使う「XVim2」/証明書作成時の入力内容.png "証明書作成時の入力内容")
5. 作成時の警告が出るが、`続ける`を選択

	![証明書作成時の警告](/2021/02/28/XcodeでVimキーバインドを使う「XVim2」/証明書作成時の警告.png "証明書作成時の警告")
6. 以下の画像のような画面が表示されれば証明書の発行は成功

	![証明書完成](/2021/02/28/XcodeでVimキーバインドを使う「XVim2」/証明書完成.png "証明書完成")

## 2. XVim2のインストール
この作業では、任意の場所にリポジトリをクローンして作業を行ますが、今回は`Desktop`で作業することとして解説します。

### Xcodeのパスの確認
インストール作業を行う前に、Xcodeが配置されているファイルパスの確認をします。

以下のコマンドで、`/Applications/Xcode.app/Contents/Developer`というパスが表示されればOKです。それ以外のパスが表示されてしまった場合は、以下コマンドで、パスを設定してください。
```
xcode-select -p
```

それ以外のパスが表示されてしまった場合は、以下コマンドで、パスを設定してください。
```
xcode-select -s /Applications/Xcode.app/Contents/Developer
```
### インストール
注意 : この作業を行うときは、Xcodeを完全に落として(タスクキル)から行ってください

1. ディレクトリを移動
```
cd ~/Desktop
```

2. リポジトリをクローン
```
git clone https://github.com/XVimProject/XVim2.git 
``` 

3. クローンしてきたリポジトリのディレクトリに移動
```
cd XVim2/
```

4. `makeコマンド`でプラグインをビルド
```
make
```

5. 出力がたくさん流れたあと、に以下のような文字が表示されれば成功
```
** BUILD SUCCEEDED **
```

## 3. XcodeにXVim2を読み込ませる
1. Xcodeを起動すると、以下の画像のようなウィンドウが表示されるので、`Load Bundle`を選択する
	![Xcode起動時の確認画面](/2021/02/28/XcodeでVimキーバインドを使う「XVim2」/Xcode起動時の確認画面.png "確認画面")
2. 上部メニューバーの`Edit`メニューの一番下に`XVim`が表示されて入れば導入成功

### 間違えて、`Skip Bundle`を選択してしまった場合
一度XCodeを閉じて(タスクキル)して、以下コマンドをターミナルで実行してから再度XCodeを実行するとまた確認ウィンドウが表示さる

X.X = 自分が使っているXcodeのバージョン 
```
defaults delete com.apple.dt.Xcode DVTPlugInManagerNonApplePlugIns-Xcod-X.X
```

## 4. .xvimrcでカスタマイズ
ホームディレクトリ直下に`.xvimrc`ファイルを作成して、`.vimrc`と同じように記述していく
```
vim ~/.xvimrc
```

## 5. 参考
- https://github.com/XVimProject/XVim2
- https://zenn.dev/ryo_kawamata/articles/intoroduce-xvim2
- https://qiita.com/ks-cap/items/91fb8578bbb930141a60
