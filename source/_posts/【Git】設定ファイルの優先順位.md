---
title: 【Git】設定ファイルの優先順位
date: 2021-04-22 23:33:03
tags:
- Git
---
# 目次
<!-- toc -->
<!-- more -->

# 設定ファイルの種類
- local : リポジトリ内
- global : ユーザー内
- system : PC全体

# 優先順位
設定ファイルの効果が出る

# 設定されている値を表示する
- local : `git config --local --list`
- global : `git config --global --list`
- system : `git config --system --list`
