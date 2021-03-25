---
title: iframeについて
date: 2021-02-11 21:32:02
tags: HTML
---
# ページ上に複数のページから読み込んだページを表示する
# iframeタグを使用する
- iframe = Inline Frame(行内フレーム)
```html
<iframe src="table.html"></iframe>
```

# Youtubeの動画を埋め込む
1. youtubeで埋め込みたい動画を選択
2. 動画の再生画面から、`埋め込みコード`を取得
3. `埋め込みコード`は`iframe`で記述してあるので、そのままコピペする

取得した埋め込みコード例
```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/y4noU6qgJlc" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```
