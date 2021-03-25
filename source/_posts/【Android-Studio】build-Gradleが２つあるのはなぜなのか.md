---
title: 【Android Studio】build.Gradleが２つあるのはなぜなのか
date: 2021-03-15 01:04:43
tags:
- Android Studio
---
AndroidStudioでプロジェクトを生成すると、「build.Gradle」というファイルが2つ生成される

### ルート直下の「build.gradle」(Project:プロジェクト名)

このファイルは、すべてのサブプロジェクトとモジュールに共通する設定項目を追加することができる最上位のビルドファイル

【例】 : サブプロジェクトにインストールしたいライブラリが含まれているリポジトリ

### appファイル直下の「build.gradle」(Module : app)

サブプロジェクトごとに必要な依存関係やビルド設定を記述する

【例】 : 使用したいライブラリのURI
