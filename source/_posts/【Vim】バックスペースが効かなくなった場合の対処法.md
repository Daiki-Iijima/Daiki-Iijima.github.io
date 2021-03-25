---
title: 【Vim】バックスペースが効かなくなった場合の対処方
date: 2021-02-26 21:20:36
tags:
---
# 参考
https://qiita.com/omega999/items/23aec6a7f6d6735d033f

# 対処方法
- `.vimrc`に以下を記述する
```
set backspace=indent,eol,start
```
