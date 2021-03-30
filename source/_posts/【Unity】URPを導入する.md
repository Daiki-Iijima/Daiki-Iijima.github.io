---
title: 【Unity】URPを導入する
date: 2021-03-27 21:09:55
tags:
- Unity
---
# 目次
<!-- toc -->
<!-- more -->

# 導入方法

## 1. プロジェクト作成時に選択する

## 注意

Unity2019.3以上のバージョンから使用できます。正確には、2019.2以前にはLightweight Render Pipeline(LWRP)というものが名称が違うだけで存在はしています。細かい仕様が違う可能性があるので、本記事は、Unity2019.3以上の環境のプロジェクト向けになります。

## 手順

新規プロジェクト作成時にUniversal Render Piplineを選択する

![1](/2021/03/27/【Unity】URPを導入する/1.png "1")

## 2. 既存のプロジェクトに追加する

### 1. Package Managerを開く

Widnow → Package Managerを選択

![2](/2021/03/27/【Unity】URPを導入する/2.png "2")

### 2. RPを選択してInstall

表示されるパッケージの設定をUnity Registryに変更しておく

![3](/2021/03/27/【Unity】URPを導入する/2.png "3")

検索窓にRPと入力してUniversal RPを検索する

Universal RPを選択後、Installをクリックで導入完了

![4](/2021/03/27/【Unity】URPを導入する/4.png "4")

### 設定方法

### 1. Pipeline Assetを作成する

Create → Rendering → Universal Render Pipeline → Pipline Asset(Forward Rendeer)の順で選択して、作成

![5](/2021/03/27/【Unity】URPを導入する/5.png "5")

### 2. セットする

Edit → Project Settings...で、Project Setting Windowを開く

![6](/2021/03/27/【Unity】URPを導入する/6.png "6")

先ほど作成したPipeline AssetをGraphics内のScriptable Render Pipeline Settingsにセットする

![7](/2021/03/27/【Unity】URPを導入する/7.png "7")

## ピンクマテリアルになるときの対処法

既存のプロジェクトに、URPを導入すると、モデルがピンク色になるときがあります。

これは、新しく導入したレンダリングシステムに既存のレンダリングシステム向けに作ったマテリアルが対応できていないことが原因で起こります。

解決するには、URP用のマテリアルに変換してあげる必要があります。

## 手順

Edit → Render Pipeline → Universal Render Pipeline → Upgrade Project Materials to UniversalRP Materials

の順で選択してあげれば、自動で変換をしてくれます。

![8](/2021/03/27/【Unity】URPを導入する/8.png "8")
