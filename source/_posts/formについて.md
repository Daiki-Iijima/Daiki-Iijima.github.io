---
title: formについて
date: 2021-02-10 08:59:29
tags: HTML
---
# 参考
[基本的なフォーム](https://www.kanzaki.com/docs/html/htminfo31.html)

# form(入力・送信フォーム)タグ
- どこに、どうやって送信するかを記述するタグ
- このタグセクションの中には、何を送信するかを示す

```html
<form></form>
```

## input(入力)タグ
- formタグの「何を」送信するかを記述するためのタグ
- formタグで囲む必要があるのは、入力した値を送信したい場合
	- 必ずformタグに記述する必要はない
- `type`属性を指定することで、入力インターフェイスを変更できる

### type属性の種類
[type属性の値](http://www.htmq.com/html5/input.shtml)
- type="hidden"
	- 画面上は表示されない隠しデータを指定する
- type="text"
	- 一行テキストボックスを作成する（初期値）
- type="search"
	- 検索テキストの入力欄を作成するHTML5から追加
- type="tel"
	- 電話番号の入力欄を作成するHTML5から追加
- type="url"
	- URLの入力欄を作成するHTML5から追加
- type="email"
	- メールアドレスの入力欄を作成するHTML5から追加
- type="password"
	- パスワード入力欄を作成する
- type="datetime"
	- UTC（協定世界時）による日時の入力欄を作成するHTML5から追加
- type="date"
	- 日付の入力欄を作成するHTML5から追加
- type="month"
	- 月の入力欄を作成するHTML5から追加
- type="week"
	- 週の入力欄を作成するHTML5から追加
- type="time"
	- 時間の入力欄を作成するHTML5から追加
- type="datetime-local"
	- UTC（協定世界時）によらないローカル日時の入力欄を作成するHTML5から追加
- type="number"
	- 数値の入力欄を作成するHTML5から追加
- type="range"
	- レンジの入力欄を作成するHTML5から追加
- type="color"
	- 色の入力欄を作成するHTML5から追加
- type="checkbox"
	- チェックボックスを作成する
- type="radio"
	- ラジオボタンを作成する
- type="file"
	- サーバーへファイルを送信する
- type="submit"
	- 送信ボタンを作成する
- type="image"
	- 画像ボタンを作成する
- type="reset"
	- リセットボタンを作成する
- type="button"
	- 汎用ボタンを作成する

```html
<form>
	<input type="text">
</form>
```

### ボタンにアクションを設定する
- `action`属性を設定することで、ボタンを押した時の挙動を指定できる

この例の場合、ボタンを押すと`action`で指定しているURLを開く
```html
<form action="http://www.google.co.jp">
	<input type="submit">
</form>
```

### テキストをデフォルトで設定しておく
- 入力された状態でデフォルト設定
	- `value`タグを使用する
```html
<input type="text" value="デフォルト"> 
```
- ガイドラインとして表示する
	- `placeholder`タグを使用する
```html
<input type="text" placeholder="デフォルト"> 
```

### チェックボックスをデフォルトでチェックした状態にする
- `checked`属性を使う
```html
<input type="checkbox" checked>
```

### ボタンの表示名を変える
- `value`属性を設定する

```
<input type="button" value="これはボタンです">
```

### 複数のラジオボタンの連携
- `name`属性をつけることで、グルーピングができる

```html
1<input type="radio" name="test">
2<input type="radio" name="test">
3<input type="radio" name="test">
```

### ラジオボタンをデフォルトでチェックした状態にする
- `checked`属性を使う
```html
<input type="checkbox" checked>
```


## ドロップダウンを生成する
- `<select></select>`タグを使用して、その中のセクションに`<option></option>`タグで項目を記述する
```html
<select>
 <option>塩ラーメン</option>
 <option>味噌ラーメン</option>
 <option>醤油ラーメン</option>
 <option>豚骨ラーメン</option>
</select>
```

### ドロップダウンのデフォルト選択項目を指定する
- デフォルトで選択させた状態にしたい`<option>`タグに、`selected`属性を付与する

```html
<select>
 <option>塩ラーメン</option>
 <option>味噌ラーメン</option>
 <option selected>醤油ラーメン</option>
 <option>豚骨ラーメン</option>
</select>
```
