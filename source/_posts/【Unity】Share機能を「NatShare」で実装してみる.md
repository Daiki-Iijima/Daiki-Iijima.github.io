---
title: 【Unity】Share機能を「NatShare」で実装してみる
date: 2021-04-28 14:10:55
tags:
- Unity
---
# 目次
<!-- toc -->
<!-- more -->

# Unityでシェア機能を実装する
## 環境
- Windows10
- Unity 2019.4.9f1
- Android 10

## NatShareとは
iOSおよびAndroid向けのシェア機能APIです。以下が今回使いそうな機能になります。
その
- ネイティブの共有UIを使用した、テキスト、画像、メディアファイルの共有
- 画像やメディアファイルのカメラロールへの保存

# 実装方法
## 公式ドキュメント
https://docs.natsuite.io/natshare/

## 1. NatShareをAssets Storeからインポート
https://assetstore.unity.com/packages/tools/integration/natshare-mobile-sharing-api-117705?aid=1101leVj4&utm_source=aff

## 2. 共有機能の実装
使用するネームスペースをインポート
```C#
using NatSuite.Sharing;
```

シェアするタイミングに以下の処理を記述
```C#
//  SNSへのシェア
var payload = new SharePayload();
payload.AddText("デフォルトテキスト、ここに記述した内容が書き込まれます。");
//payload.AddImage("画像");
var success = payload.Commit();
```

画像も添付したい場合は、`payload.AddImage("画像")`のコメントを外して`画像`部分に`Texture2D`を引数として渡してください。

## 3. 実行時の参考画像
シェア機能実行時
![シェア機能選択](/2021/04/28/【Unity】Share機能を「NatShare」で実装してみる/1.png "シェア機能選択")

Twitter選択時
![Twitter選択](/2021/04/28/【Unity】Share機能を「NatShare」で実装してみる/2.png "Twitter選択")
### NatShareを使用したスクリーンショットのサンプル
撮影された`screenshot`は`Texture2Dになります。
```C#
//  スクリーンショット撮影
var screenshot = ScreenCapture.CaptureScreenshotAsTexture();
```

### 注意
Editor上で実際の動きの確認はできないので、iOSかAndoridにBuildして試してみて下さい。
