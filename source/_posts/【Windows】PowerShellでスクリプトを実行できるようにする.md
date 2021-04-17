---
title: 【Windows】PowerShellでスクリプトを実行できるようにする
date: 2021-04-26 02:56:58
tags:
- Windows
- PowerShell
---
# 目次
<!-- toc -->
<!-- more -->

# スクリプトを実行するとエラーが表示される
何も設定されていない`Widnows PowerShell`でスクリプトを実行しようとすると、以下のようなエラーが出てしまいます。

このエラーは、今のPowerShellはスクリプトを実行できる権限がありませんよ。ということらしいです。マルウェアなどの危険なスクリプトの不用意な実行を防ぐというセキュリティ状の配慮によるものらしいです。

今回のケースでは、静的ブログを作成できるフレームワークの`hexo`を実行しようとしたときに起こりましたした。
```bash
hexo : このシステムではスクリプトの実行が無効になっているため、ファイル C:\Users\DaikiIijima\AppData\Roaming\npm\hexo.p
s1 を読み込むことができません。詳細については、「about_Execution_Policies」(https://go.microsoft.com/fwlink/?LinkID=135
170) を参照してください。
発生場所 行:1 文字:1
+ hexo new "test"
+ ~~~~
    + CategoryInfo          : セキュリティ エラー: (: ) []、PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess
```

# 解決策

## 全6種類のポリシー
- AllSigned : 署名付きのスクリプトのみ実行可能
- Bypass : 検査巡回
- RemoteSigned : ローカルスクリプトと署名追記のリモートスクリプトのみ実行可能
- Restricted : 全て実行不可
- Undefined : 未定義
- Unrestricted : 全て実効可能

## 1. 現在の状態を取得する
表示された、`Restricted`を`RemoteSigned`に変更することで、スクリプトを実行できる状態にします。
```bash
$ Get-ExecutionPolicy

Restricted
```

## 2. 設定を変更する
```bash
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process                                                         
```

再度状態を確認
```bash
$ Get-ExecutionPolicy

RemoteSigned
```
