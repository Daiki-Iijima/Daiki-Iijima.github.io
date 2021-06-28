---
title: 【HTML】手っ取り早くセンタリングする
date: 2021-05-10 23:52:11
tags:
- HTML
---
# 目次
<!-- toc -->
<!-- more -->

# pタグを使用してセンタリングする
`css`の属性の`text-align`に`center`を設定する

## pタグ内に直接記述
```html
<p style="text-align:center">センタリングされる</p>
```

## styleタグに分離
```html
<style>
 #center{
  text-align:center;
 }
</style>

<p id=center>センタリングされる</p>
```


# divタグを使用してセンタリングする
`align`属性に`center`を設定する

```html
<div align="center">
 <p>センタリングされる</p>
</div>
```
