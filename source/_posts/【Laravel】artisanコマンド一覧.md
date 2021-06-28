---
title: 【Laravel】artisanコマンド一覧
date: 2021-05-27 18:29:22
tags:
- Laravel
---
# 目次
<!-- toc -->
<!-- more -->

# この記事のLaravelバージョン
```bash
$ php artisan -V
Laravel Framework 8.46.0
```

# コマンド一覧を表示するコマンド
自作コマンドもこのコマンドで一緒に表示されます。
```
php artisan list
```

## 使用方法
```
php artisan コマンド オプション 引数
```

# コマンド
|コマンド|説明|
|---|---|
|clear-compiled      | コンパイル済みクラスファイルの削除|
|db                  | 新規データベースCLIセッションの開始|
|down                | アプリケーションをメンテナンス／デモモードにする|
|env                 | 現在のフレームワーク環境を表示|
|help                | コマンドのヘルプを表示する|
|inspire             | 感動的な言葉を表示する(ジョーク機能)|
|list                | コマンドリストを表示する|
|migrate             | データベースマイグレーションの実行|
|optimize            | フレームワークのブートストラップファイルのキャッシュ|
|test                | アプリケーション・テストの実行|
|tinker              | アプリケーションを操作する|
|up                  | アプリケーションのメンテナンス・モードの解除|

## Auth
|コマンド(ショート,フル)|説明|
|---|---|
|auth:clear-resets    |期限切れのパスワード・リセット・トークンのフラッシュ

## cache
|コマンド|説明|
|---|---|
|cache:clear         |アプリケーションのキャッシュを消去する|
|cache:forget        |キャッシュからアイテムを削除する|
|cache:table         |キャッシュデータベーステーブルのマイグレーションの作成|

## config
|コマンド|説明|
|---|---|
|config:cache         |設定の読み込みを高速化するためのキャッシュファイルの作成|
|config:clear         |設定キャッシュファイルの削除|

## db
|コマンド|説明|
|---|---|
|db:seed              |データベースにレコードを格納する|
|db:wipe              |すべてのテーブル、ビュー、およびタイプを削除する|

## event
|コマンド|説明|
|---|---|
|event:cache          |アプリケーションのイベントとリスナーの検出とキャッシュ|
|event:clear          |キャッシュされたイベントとリスナーをすべて消去する|
|event:generate       |登録に基づいて不足しているイベントとリスナーを生成する|
|event:list           |アプリケーションのイベントとリスナーをリストアップする|

## key
|コマンド|説明|
|---|---|
|key:generate         |アプリケーションキーの設定|

## make
|コマンド|説明|
|---|---|
|make:cast            |新しいカスタムEloquentキャストクラスの作成|
|make:channel         |新しいチャンネルクラスの作成|
|make:command         |Artisanコマンドの新規作成|
|make:component       |新しいビューコンポーネントクラスを作成します|
|make:controller      |新しいコントローラクラスの作成|
|make:event           |新しいイベントクラスの作成|
|make:exception       |新しいカスタム例外クラスの作成|
|make:factory         |新しいモデルファクトリの作成|
|make:job             |新しいジョブクラスの作成|
|make:listener        |新しいイベントリスナークラスの作成|
|make:mail            |新しいEメールクラスの作成|
|make:middleware      |新しいミドルウェアクラスの作成|
|make:migration       |新しいマイグレーションファイルの作成|
|make:model           |新しいEloquentモデルクラスの作成|
|make:notification    |新しい通知クラスの作成|
|make:observer        |新しいオブザーバークラスの作成|
|make:policy          |新しいポリシークラスの作成|
|make:provider        |新しいサービスプロバイダクラスの作成|
|make:request         |新しいフォームリクエストクラスの作成|
|make:resource        |新しいリソースの作成|
|make:rule            |新しい検証ルールの作成|
|make:seeder          |新しいシーダークラスの作成|
|make:test            |新しいテストクラスの作成|

## migrate
|コマンド|説明|
|---|---|
|migrate:fresh        |すべてのテーブルを削除し、すべてのマイグレーションを再実行する|
|migrate:install      |移行リポジトリの作成|
|migrate:refresh      |すべての移行のリセットと再実行|
|migrate:reset        |すべてのデータベース移行のロールバック|
|migrate:rollback     |最後のデータベース移行のロールバック|
|migrate:status       |各移行のステータスの表示|

## otifications
|コマンド|説明|
|---|---|
|notifications:table  |通知テーブルのマイグレーションを作成する|

## optimize
|コマンド|説明|
|---|---|
|optimize:clear       |キャッシュされたブートストラップ・ファイルを削除する|

## package
|コマンド|説明|
|---|---|
|package:discover     |キャッシュされたパッケージマニフェストを再構築する|

## queue
|コマンド|説明|
|---|---|
|queue:batches-table  |batchesデータベーステーブルのマイグレーションを作成する|
|queue:clear          |指定されたキューからすべてのジョブを削除する|
|queue:failed         |失敗したキューのジョブをすべてリストアップする|
|queue:failed-table   |失敗したキューのジョブ・データベース・テーブルのマイグレーションを作成する|
|queue:flush          |失敗したキューのジョブをすべてフラッシュする|
|queue:forget         |失敗したキューのジョブを削除する|
|queue:listen         |指定されたキューをリッスンする|
|queue:prune-batches  |バッチ・データベースから古いエントリを削除する|
|queue:prune-failed   |失敗したジョブ・テーブルから古いエントリを削除する|
|queue:restart        |現在のジョブの後にキューワーカーデーモンを再起動する|
|queue:retry          |失敗したキューのジョブを再試行する|
|queue:retry-batch    |バッチの失敗したジョブを再試行する|
|queue:table          |キューのジョブ・データベース・テーブルのマイグレーションを作成する|
|queue:work           |デーモンとしてキューのジョブ処理を開始する|

## route
|コマンド|説明|
|---|---|
|route:cache          |ルート登録を高速化するためのルートキャッシュファイルの作成|
|route:clear          |ルートキャッシュファイルの削除|
|route:list           |登録されているすべてのルートを一覧表示する|

## sail
|コマンド|説明|
|---|---|
|sail:install         |Laravel SailのデフォルトのDocker Composeファイルのインストール|
|sail:publish         |Laravel SailのDockerファイルを公開する|

## schedule
|コマンド|説明|
|---|---|
|schedule:list        |スケジュールされたコマンドの一覧表示|
|schedule:run         |スケジュールされたコマンドの実行|
|schedule:test        |スケジュールされたコマンドの実行|
|schedule:work        |スケジュールワーカーの起動|

## schema
|コマンド|説明|
|---|---|
|schema:dump          |与えられたデータベーススキーマをダンプする|

## session
|コマンド|説明|
|---|---|
|session:table        |セッションデータベーステーブルのマイグレーションの作成|

## storage
|コマンド|説明|
|---|---|
|storage:link         |アプリケーション用に設定されたシンボリックリンクの作成|

## stub
|コマンド|説明|
|---|---|
|stub:publish         |カスタマイズ可能なすべてのスタブの公開|

## vendor
|コマンド|説明|
|---|---|
|vendor:publish       |ベンダー・パッケージからパブリッシュ可能なアセットをすべてパブリッシュする|

## view
|コマンド|説明|
|---|---|
|view:cache           |アプリケーションのすべてのBladeテンプレートをコンパイルする。|
|view:clear           |コンパイルされたすべてのビュー・ファイルの消去|
|serve                |PHP開発用サーバーでアプリケーションを動作させる|

# オプション
|コマンド(ショート,フル)|説明|
|---|---|
|-h, --help           | 指定されたコマンドのヘルプを表示します。コマンドが指定されていない場合は、コマンドリストのヘルプを表示します|
|-q, --quiet          | メッセージを出力しない|
|-V, --version        | このアプリケーションのバージョンを表示する|
|    --ansi|--no-ansi | ANSI出力を強制する（または--no-ansiを無効にする）|
|-n, --no-interaction | インタラクティブな質問をしないこと|
|    --env[=ENV]      | コマンドを実行するための環境|
|1:-v,2:-vv,3:-vvv, --verbose | メッセージの冗長性を高めます。1:通常のログ、2:冗長度が高い出力、3:デバッグレベルの出力|
