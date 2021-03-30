---
title: 【Mac】ツールのバージョンのチェック方法
date: 2021-03-25 22:59:57
tags:
- Mac
---
## 目次
<!-- toc -->
<!-- more -->

## Swiftバージョン確認
- `swift -version`

```shell-session
$ swift -version

Apple Swift version 5.3.2 (swiftlang-1200.0.45 clang-1200.0.32.28)
Target: x86_64-apple-darwin20.3.0
```

## OSバージョン確認
- `sw_vers`

```shell-session
$ sw_vers

ProductName:    macOS
ProductVersion: 11.2
BuildVersion:   20D64
```

## XCodeバージョン確認
- `xcodebuild -version`

```shell-session
$ xcodebuild -version

Xcode 12.4
Build version 12D4e
```

## 色々バージョン確認
- `system_profiler > ファイル名.txt`
	- かなり待つ必要がある

```shell-session
$ system_profiler > ver.txt
```
