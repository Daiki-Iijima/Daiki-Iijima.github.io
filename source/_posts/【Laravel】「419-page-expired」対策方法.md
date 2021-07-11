---
title: 【Laravel】「419 page expired」対策方法
date: 2021-06-09 01:26:26
tags:
- PHP
- Laravel
---
# 目次
<!-- toc -->
<!-- more -->

# 「419 paeg expired」の原因
このエラーコードは、Bladeファイル内で、`クロスサイトリクエストフォージェリ(Cross Site Request Forgery)`対策がされていない、フォームの送信を行ったときに表示されます。

# 解決策
`@csrf`をフォーム内に記述する

```html
<form action="/hoge/add" method="post">
  @csrf
  <p><input type="text" name="name"></p>
  <p><input type="submit" name="送信"></p>
</form>
```

## @csrfはなにか
- CSRF(Cross Site Request Forgery)対策のために用意された、Bladeディレクティブ
- トークンと呼ばれるランダムな文字列を非表示フィールドとして追加してトークンの値が正しいフォームだけを受けつけるようにする
