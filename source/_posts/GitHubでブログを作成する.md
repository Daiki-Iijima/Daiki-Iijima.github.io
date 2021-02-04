---
title: GitHubでブログを作成する(Hexo)
categories: Blog
tags: 
- [Hexo]
- [GitHub]
---

# 環境
- Macbook Air 2020 M1
- Big Sur 11.0.1

#	前準備
1. node.jsをインストールする
2. Hexoをインストールする

## 1. node.jsをインストールする
``` bash
git clone https://github.com/creationix/nvm ~/.nvm
source ~/.nvm/nvm.sh
nvm install 10.16.3
```

## 2. Hexoをインストールする
node.jsに付属してくる、nmpを使用する

```bash
npm install -g hexo
```

## 3. HexoにGit操作用ツールを追加
hexoでdeployするときにgitを使用する
```
npm install hexo-deployer-git --save
```

# GitHubでブログ用のリポジトリを作成する
リポジトリ名はなんでも良いわけではなく、特定の記述規則に従う必要がある
```
username.github.io

username = GitHubのユーザー名
```

# 作成したリポジトリをCloneして移動
```
git clone [リポジトリ]
cd [リポジトリ]
```

# Hexoでプロジェクトを作成
ここで作成するプロジェクトは後で消去するので（必要なのは作成されるフォルダの中のファイル)、適当でOK
```
hexo init [プロジェクト名]
```

# ファイル名の中身をCloneしたリポジトリに移動させる
```
mv ./<任意のプロジェクト名>/* ./
mv ./<任意のプロジェクト名>/.* ./
rm -r <任意のプロジェクト名>
```

# Hexoプロジェクトの設定を書き換える
## 書き換え対象ファイル
```
_config.yml
```
## 書き換える設定
- language: -> language: ja
- url: -> url: https://<username>.github.io/

## 「deploy:」 以下を書き換え&追記
- 書き換え前
```
deploy:
  type: ''
```

- 書き換え後
```
deploy:
	type: git
	repo: https://github.com/<username>/<username>.github.io
	branch: master
	message: コミット時のメッセージ
```
