---
title: 【Unity】2018.4以前バージョンから、2019.xへの更新時に「NetworkBehaviour is not found」が出た時の対処法
date: 2021-03-29 21:51:08
tags:
- Unity
---
# 目次
<!-- toc -->
<!-- more -->

# 原因
2019.1から非推奨になったことが原因で、デフォルトでUnity内のライブラリには存在しなくなってしまいました。

非推奨なので、別の手段でネットワーク機能を実装したほうがいいのですが、とりあえず今はUNetを使いたいという方向けの対処法になります。

[Evolving multiplayer games beyound UNet](https://blogs.unity3d.com/2018/08/02/evolving-multiplayer-games-beyond-unet/?_ga=2.252022665.1606307406.1556038404-136028431.1556038404)

# 手順
## 1. PackageManagerを開く
Window -> Package Manager

![1](/2021/03/29/【Unity】2018-4以前バージョンから、2019-xへの更新時に「NetworkBehaviour-is-not-found」が出た時の対処法/1.png "1")

## 2. Unity Registryを選択してから、「Multiplayer HLAPI」「XR Legacy InputHelpers」をインストール
ウィンドウ左上のプルダウンを`Unity Registry`に設定

![2](/2021/03/29/【Unity】2018-4以前バージョンから、2019-xへの更新時に「NetworkBehaviour-is-not-found」が出た時の対処法/2.png "2")

検索窓から、「Multiplayer HLAPI」「XR Legacy InputHelpers」を検索してインストールする

![3](/2021/03/29/【Unity】2018-4以前バージョンから、2019-xへの更新時に「NetworkBehaviour-is-not-found」が出た時の対処法/3.png "3")

![4](/2021/03/29/【Unity】2018-4以前バージョンから、2019-xへの更新時に「NetworkBehaviour-is-not-found」が出た時の対処法/4.png "4")

