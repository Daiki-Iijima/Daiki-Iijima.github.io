---
title: '【Git&Unity】UnityYAMLMerge使用してシーンファイルをマージをする'
date: 2021-04-25 02:56:11
tags:
- Git
- Unity
---
# 目次
<!-- toc -->
<!-- more -->

# SceneファイルのマージにはSmartMergeを使おう
Unityので使用するシーンファイルのgit管理時のコンフリクト対応を手動で行うことは可能ではありますが、１つ間違えると、シーンが開けなくなる可能性があるので、基本的には、Unityが提供してくれている`UnityYAMLMerge`というツールを使うことをおすすめします。

# 設定方法
以降の解説はGit(CUI)を使用して、SmartMergeを使用するための手順です。

## 1. どのレベルに設定するか
UnityYAMLMergeをどの程度の範囲で利用したいかを考慮して、以下のディレクトリにある`config`ファイルに追記していきます。

- local : `$GIT_DIR/config`
- global : `$HOME/.gitconfig`
- system : 
	- Windows : `C:/Program File (x86)/Git/etc/gitconfig`
	- Mac : `/Applications/Xcode.app/Contents/Developer/usr/etc/gitconfig/`
	- Unix/Linux : `/etc/gitconfig`

## 2. 設定を追記する
以下設定を`config or .gitconfig`ファイルに追記します。

```bash
[merge]
    tool = unityyamlmerge
[mergetool "unityyamlmerge"]
    trustExitCode = false
    cmd = '[Unityフォルダのパス]/Editor/Data/Tools/UnityYAMLMerge.exe' merge -p "$BASE" "$REMOTE" "$LOCAL" "$MERGED"
```

## 3. UnityYAMLMergeが手に負えない場合の、手動マージツールを設定する
UnityYAMLMergeが全てのコンフリクトを解消してくれるとは限らないので、最終手段として人間がコンフリクトを解決する必要があります。

コンフリクト解消に使用するツール(fallbackツール)を設定するためには`auto`ファイルをプロジェクトのルートディレクトリに配置しておく必要があります。

今回は、vimdiffを使用します。

ファイル名: auto
```bash
* use "fallbackツールのディレクトリ" -c "wincmd J" "%d" "%l" "%b" "%r"
```

# 使用方法
以下コマンドをコンフリクトした状態のGitディレクトリで実行します。

```bash 
$ git mergetool
```

動かない場合は、明示的にマージツールを指定してみて下さい。


```bash 
$ git mergetool -t unityyamlmerge
```
