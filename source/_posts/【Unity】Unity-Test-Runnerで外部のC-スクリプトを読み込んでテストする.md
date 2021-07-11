---
title: 【Unity】Unity Test Runnerで外部のC#スクリプトを読み込んでテストする
date: 2021-06-16 03:17:12
tags:
- Unity
- Test Runner
---
# 目次
<!-- toc -->
<!-- more -->

# 手順
## 1. アセンブリファイルを作成する
テストコード内で読み込みたいスクリプトのあるディレクトリで以下の操作を行い、アセンブリファイルを作成します。

```
ディレクトリ内で右クリック -> Create -> Assembly Definition
```
![手順1](/2021/06/16/【Unity】Unity-Test-Runnerで外部のC-スクリプトを読み込んでテストする/手順1.png "手順1")

## 2. 紐付け
作成したアセンブリファイルをテスト用のアセンブリファイルと紐付ける必要があります。

テスト用のフォルダ内にある、`xxx.asmdef`を選択して、`Inspector`の`Assembly Definition Reference`の項目に手順1で作成したアセンブリファイルを設定します。

![手順2](/2021/06/16/【Unity】Unity-Test-Runnerで外部のC-スクリプトを読み込んでテストする/手順2.png "手順2")
