---
title: 【Git】コマンドラインの構文
date: 2021-03-08 02:33:53
tags:
- Git
---
## コマンドラインの構文の概要
- git : 必須
- [スイッチ] : オプション
- <コマンド> : オプション
- <引数>: オプション
```
git [スイッチ]<コマンド><引数>
```

## ヘルプにも同じような構文の記述がされている
```
usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]
```

| コマンド                                                           | 説明                                                               | 参考                                                        | 
|----------------------------------------------------------------|------------------------------------------------------------------|-----------------------------------------------------------| 
| --version                                                      | バージョン確認                                                          |                                                           | 
| --help                                                         | 概要と最も一般的に使用されるコマンドのリストを出力                                        |                                                           | 
| -C <path>                                                      | カレントディレクトリではなく<path>に指定したディレクトリで`Git`実行する                        |                                                           | 
| -c <name>=<value>                                              | 設定ファイルの<name>に指定した項目の値を<value>で設定した値を上書きする                       |                                                           | 
| --exec-path[=<path>]                                           | Gitのコアファイルのパスを出力する。パスを設定することもできる。                                |                                                           | 
| --html-path                                                    | ドキュメントファイルの補完されているパスを出力する                                        |                                                           | 
| --man-path                                                     | Gitのmanファイルが格納されているパスを出力する                                       |                                                           | 
| --info-path                                                    | Gitのドキュメントを文書かしたファイルがあるパスを出力する(私の環境ではパスは表示されたが、パスが存在しなかった)       |                                                           | 
| -P \| --paginate                                               | ページャーに出力をパイプする                                                   |                                                           | 
| -p \| --no-paginate                                            | ページャーに出力をパイプしないようにする                                             |                                                           | 
| --no-replace-objects                                           | Gitオブジェクトを置換しない                                                  | https://git-scm.com/docs/git-replace                      | 
| --bare                                                         | ベアリポジトリとして扱う                                                     | https://qiita.com/devzooiiooz/items/56a02342d9d65d79f6c3<br>https://cpplover.blogspot.com/2015/04/git10linus-torvals.html |                                                                  |                                                           | 
| --git-dir=<path>                                               | リポジトリへのパスを設定する(環境変数 GIT_DIR を設定するのと同じ)                           |                                                           | 
| --work-tree=<path>                                             | 作業ツリーへのパスを設定する(環境変数 GIT_WORK_TREE や設定変数 core.worktree を設定するのと同じ) |                                                           | 
| --namespace=<path>                                             | Gitの名前空間を設定する(環境変数 git_namespace を設定するのと同じ)                      |                                                           | 


## ダッシュ(-)1個とダッシュ(--)の使い分け
- 1つ(-) : １文字のスイッチ(省略型)
- 2つ(--) : 略さずに完全に記述する長いスイッチ
