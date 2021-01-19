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
$ git clone https://github.com/creationix/nvm ~/.nvm
$ source ~/.nvm/nvm.sh
$ echo "source ~/.nvm/nvm.sh" >> ~/.bashrc
$ nvm install 10.16.3
```

## 2. Hexoをインストールする
node.jsに付属してくる、nmpを使用する

```bash
$ npm install -g hexo
```

# GitHubでブログ用のリポジトリを作成する
リポジトリ名はなんでも良いわけではなく、特定の記述規則に従う必要があります。
```
username.github.io

username = GitHubのユーザー名
```
