---
title: 【Git】タグの扱い方
date: 2021-03-13 04:03:54
tags:
- Git
---
## タグはなんのためにあるのか

コミットを指定するために`SHA 1ID`を使用するが、毎回選択するのは面倒くさいし間違える可能性があるので、よく使う可能性のあるコミットに命名することで、いちいち`SHA 1ID`を指定しなくてよくできる

## コミットにタグを追加する
### タグをつける
```shell-session
git tag タグ名 タグをつけたいSHA1
```

### タグをつけるときは、`-m`スイッチを使用すればメッセージをつけることもできる
```shell-session
git tag タグ名 -m "コメント" タグをつけたいSHA1
```

## タグを消去する
```shell-session
git tag -d タグ名
```

これが表示されれば成功
```shell-session
Deleted tag 'タグ名' (was SHA1)
```

## タグの一覧を表示する

```shell-session
git tag
```
