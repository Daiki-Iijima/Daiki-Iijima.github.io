---
title: 【env】anyenvでXXXenv系のバージョン管理
date: 2021-05-14 01:09:58
tags:
- anyenv
---
# 目次
<!-- toc -->
<!-- more -->

# xxxenvを管理できる「anyenv」を導入する
xxxenv系の導入をサポートするツール

# anyenvを導入する
## 1. githubからclone
- `~/.anyenv`に配置する
```bash
$ git clone https://github.com/riywo/anyenv ~/.anyenv
```

## 2. パスを通す
- zshを使用しているので、`.zshrc`に以下を追記(bashの場合は`.bashrc`)
```
if [ -d $HOME/.anyenv ] ; then
    export PATH="$HOME/.anyenv/bin:$PATH"
    eval "$(anyenv init -)"
    # tmux対応
    for D in `\ls $HOME/.anyenv/envs`
    do
        export PATH="$HOME/.anyenv/envs/$D/shims:$PATH"
    done
fi
```
## 3. anyenvを初期化する
```bash
$ anyenv install --init
$ source ~/.zshrc
```
# コマンド
|コマンド|内容|
|:-:|:-:|
|`$ anyenv`|ヘルプ|
|`$ anyenv init`|初期化|
|`$ anyenv envs`|インストールされている\*\*env一覧|
|`$ anyenv root`|anyenvのインストール先の絶対パス|
|`$ anyenv install -l`|インストールできる\*\*envの一覧|
|`$ anyenv install **env`|指定された\*\*env のインストール|
|`$ anyenv version`|\*\*envごとのシェルにおける実行環境|
|`$ anyenv versions`|\*\*envごとのインストールされている実行環境一覧|
|`$ anyenv global`|\*\*envごとのデフォルトの実行環境|

# ほぼ必須なプラグイン「anyenv-update」を導入する
## 1. プラグインを配置するディレクトリを作成
- phpenv以下に`plugins`フォルダを作成する
```bash
$ mkdir -p $(anyenv root)/plugins
```
## 2. アップデートを実行
```bash
$ anyenv update
```

# コマンド(anyenv-update)
|コマンド|内容|
|:-:|:-:|
|`$ anyenv update`|アップデート (anyenv-update)<br>※**envやそのプラグイン含む|
