---
title: iframeのaline属性について
date: 2021-02-12 23:14:32
tags: HTML
---
# alineとは
- `iframe(インラインフレーム)`に並ぶテキスト位置を指定できる
- `iframe(インラインフレーム)`をフロートさせられる
	- フロート : 左右どちらかに寄せて、後続のテキストを回り込ませる

## 指定可能文字列
- left : 左に配置して、後続の内容を右側に回り込ませる
- right: 右に配置して、後続の内容を左側に回り込ませる
```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/DrDm7uO4Fu0" align ="right"></iframe>
```
