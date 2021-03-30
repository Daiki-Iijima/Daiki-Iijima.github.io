---
title: 【Unity】ディレクティブを使用しているときに発生するwarning対策
date: 2021-03-28 23:18:17
tags:
- Unity
- Visual Studio
---
# 目次
<!-- toc -->
<!-- more -->

# ディレクティブとはなにか
Unityは`プラットフォーム依存コンパイル`という機能を持っています。これは、Unityで作成したゲームやアプリを複数のプラットフォームで動かしたい場合に、各プラットフォームに依存したコード(ファイルの保存領域、Bluetoothの使用)を１つのスクリプト内で書けるようにする仕組みです。

## 参考リンク
[Unityドキュメント](https://docs.unity3d.com/ja/2018.4/Manual/PlatformDependentCompilation.html)

# なぜwarningが発生するのか
原因はプラットフォームに依存(ディレクティブ指定)しているコードは、Unity Editor上のコンパイルでは無視されることにあります。

無視されるということは、宣言した変数をEditor上で実行するときは使用していないと見られるケースが発生します。

## 例
この例では、スマホ用OS向けにビルドすることを考えてディレクティブを設定しています。記述上は`Number`を使用してしますが、`UnityEditor`から見ると、`Number`は使用されていない変数になります。
```c#
//	この変数はUityEditor上では使用していないことになるのでwaringが発生する
int Number = 9;
	
private void test()
{
	//	ここはAndroid用にビルドしたときに初めて有効になる
#if UNITY_ANDROID
	Number = 100;
#endif

	//	ここはiOS用にビルドしたときに初めて有効になる
#if UNITY_iOS
	Number = 300;
#endif

...
}
```

# 対策方法
## 1. エディタ用のダミー処理を作る
上の例はEditor用の処理が書いてありませんでした。何かしらのダミー処理で変数を使うようにすれば`warning`の発生を抑える事ができます。それと同時にテストを書くときのことを考えても、内部処理はダミーでも実装しておいたほうがいいかと思います。

```c#

//	ダミー処理で使っているのwarningは発生しない
int Number = 9;
	
private void test()
{
	//	ここはAndroid用にビルドしたときに初めて有効になる
#if UNITY_ANDROID
	Number = 100;
#endif

	//	ここはiOS用にビルドしたときに初めて有効になる
#if UNITY_iOS
	Number = 300;
#endif

	//	Unity Editor用のダミー処理
#if UNITY_EDITOR
	Number = 0;
#endif

...
}
```

## 2. 1つのスクリプト内だけ特定のwarningを発生させない
プリプロセス命令をファイルの先頭に書くことによってコンパイル時の処理を指定する方法です。

以下のような`warning`表示が表示された場合、これを解決するには`CS0149`というwarningを発生させないプリプロセス命令が必要になります。
```c#
test.cs(59,48): warning CS0149: xxxx
```

`CS0149`のwarningを発生させないようにするための記述は以下のようになります。
```c#
#pragma warning disable 0149
```

## 3. プロジェクト全体に対して発生させたくないwarningを指定する
この方法を取ると、指定したすべての条件に一致するものが表示されなくなってしまうので、設定する場合は慎重に行ってください。

### .rspとは
MSBuild.exeのコマンドラインスイッチを含むテキストファイル。詳しくは以下リンクを参照。

[MSBuild応答ファイル](https://docs.microsoft.com/ja-jp/visualstudio/msbuild/msbuild-response-files?view=vs-2019)

### 設定手順
1. `Assetsフォルダ`下に`csc.rsp`というファイルを作成してください。(Assets/csc.rsp)
	- UnityEditorでファイルを作成すると見た目上は、`csc.rsp`に見えますが、拡張子が`cs`になってしまうので、エクスプローラーから作成する
2. `csc.rsp`内に`-nowarn:xxxx`と記述する
	- `xxx`の部分は`warning時に表示される数字の部分です。
	- 複数指定したい場合は、記述した部分の下に追記してく

### 設定例
```c#
//	warning CS0149: xxxxの場合
-nowarn:0149
//	warning CS0031: yyyyの場合
-nowarn:0031
```
