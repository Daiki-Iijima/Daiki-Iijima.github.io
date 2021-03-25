---
title: 【Linuxコマンド】よく使うlsコマンドオプション
date: 2021-02-28 11:22:41
tags:
- Linux
- Linuxコマンド
---
## 目次
1. 隠しファイル`.ファイル`まで表示させる
2. ファイル詳細を表示させる
3. １列１ファイルで表示させる
4. カンマ区切りで表示させる 

## 普通に`ls`を使った場合
```
% ls
Memo_App           Memo_App.xcodeproj README.md
```

## 1. 隠しファイル`.ファイル`まで表示させる
オプション`-a`をつける
```
ls -a
```

### 実行例
```
%ls -a
.                  .DS_Store          .gitignore         Memo_App.xcodeproj
..                 .git               Memo_App           README.md
```
## 2. ファイル詳細を表示させる
lsコマンドのオプションに`-l`をつける

```
ls -l
```

### 実行例
```
% ls -l
total 8
drwxr-xr-x  12 daiki  staff  384  2 28 01:39 Memo_App
drwxr-xr-x@  5 daiki  staff  160  2 28 02:03 Memo_App.xcodeproj
-rw-r--r--   1 daiki  staff   10  2 27 22:39 README.md
```

## 3. １列１ファイルで表示させる
lsコマンドのオプションに`-1`をつける

```
ls -1
```

### 実行例
```
% ls -1
Memo_App
Memo_App.xcodeproj
README.md
```

## 4. カンマ区切りで表示させる  
lsコマンドのオプションに`-m`をつける
```
ls -m
```

### 実行例
```
% ls -m
Memo_App, Memo_App.xcodeproj, README.md
```
