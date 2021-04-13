---
title: 【GitHub】既存のローカルリポジトリをGitHubで管理する
date: 2021-04-21 23:55:38
tags:
- Git
- GitHub
---
# 目次
<!-- toc -->
<!-- more -->

# 操作手順

今回は、解説のために`test`リポジトリをGitHub上に作成します。

## 1. GitHubで管理用リポジトリを作成する
GitHubからクローンしてくるときのURLを取得する

![GitHub画面](/2021/04/21/【GitHub】既存のローカルリポジトリをGitHubで管理する/GitHub画面.png "GitHub画面")

## 2. ローカルリポジトリにリモートリポジトリを追加する
`git remote add origin URL`を使用してローカルリポジトリにベアリポジトリを紐付ける

```bash
$ git remote add origin https://github.com/Daiki-Iijima/test.git
```
## 3. ブランチをGitHubに合わせる
現在いるブランチをmaster(main)ブランチに変更すします。これは、GitHubの仕様変更で、デフォルトブランチが`master`から`main`に変わったことによる対応です。

`-M`: 今いるブランチ名を強制的に`main`に変更します。
```bash
$ git branch -M main
```

## 4. ローカルリポジトリのブランチをpushする
ブランチをリモートリポジトリに反映しながら`push`します。

```bash
$ git push -u origin main
```

