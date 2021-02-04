---
title: HTMLの概要
date: 2021-02-05 00:21:18
tags: HTML
---
# HTMLの特徴

全てのコードはタグで囲まれている

```html
<body>
  <title>タイトル</title>
</body>
```

## HTMLのサンプルサイト
[サンプルサイト](http://example.com)

# タグ
## 基本
```
- <html></html>      : HTMLの内容
```
## 文章関係
```
- <body></body>      : 文章の本文
- <div></div>        : division(領域)画面上の領域を分ける
- <h~></h~>          : Header(タイトル)~部分は数字が入り、数字によってタイトルのサイズが変わる
- <p></p>            : Paragraf(段落)
- <a href="xxx"></a> : リンク
```

## レイアウト関係
```
- <head></head>      : レイアウトの記述
- <title></title>    : ブラウザのタブに表示される名前
- <style></style>    : 文字やレイアウトの装飾を指定する部分
	- body{}           : <body></body>に対するレイアウト設定
	- div{}            : <div></div>に対するレイアウト設定
	- a:link,a:visited : リンクに対する書式設定
	- @media           : メディアクエリー（デバイスによって切り替える)レスポンシブデザインのための記述
```
### メタ
```
- <meta charset=""/>    : 文字コードの指定
- <meta http-equiv="" content=""/>	: ページの種類の指定 
- <meta name=""content=""/>         : 
```
