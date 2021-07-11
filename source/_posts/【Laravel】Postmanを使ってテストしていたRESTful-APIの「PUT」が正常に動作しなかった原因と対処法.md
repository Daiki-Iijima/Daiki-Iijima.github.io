---
title: 【Laravel】Postmanを使ってテストしていたRESTful APIの「PUT」が正常に動作しなかった原因と対処法
date: 2021-06-12 03:23:06
tags:
- Laravel
- Postman
---

# 目次
<!-- toc -->
<!-- more -->

# 原因
Postmanそのものの問題ではなく、HTMLが`PUT(POST,GET以外)`のメソッドをサポートしていないことが原因でした。

具体的な設定として、`form-data`でbodyにデータを設定していました。`form-data`は`HTML`の`formタグ`の動作を再現するので、このような現象になるようです。

![formdata設定](/2021/06/12/%E3%80%90Laravel%E3%80%91Postman%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%A6%E3%83%86%E3%82%B9%E3%83%88%E3%81%97%E3%81%A6%E3%81%84%E3%81%9FRESTful-API%E3%81%AE%E3%80%8CPUT%E3%80%8D%E3%81%8C%E6%AD%A3%E5%B8%B8%E3%81%AB%E5%8B%95%E4%BD%9C%E3%81%97%E3%81%AA%E3%81%8B%E3%81%A3%E3%81%9F%E5%8E%9F%E5%9B%A0%E3%81%A8%E5%AF%BE%E5%87%A6%E6%B3%95/formdata%E8%A8%AD%E5%AE%9A.png "formdata設定")

# 対処法
bodyのデータ形式を、`form-data`から、`raw`に変更して、json形式でデータを記述すれば`PUT`メソッドを使用しても正常に動作します。

![raw設定](/2021/06/12/%E3%80%90Laravel%E3%80%91Postman%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%A6%E3%83%86%E3%82%B9%E3%83%88%E3%81%97%E3%81%A6%E3%81%84%E3%81%9FRESTful-API%E3%81%AE%E3%80%8CPUT%E3%80%8D%E3%81%8C%E6%AD%A3%E5%B8%B8%E3%81%AB%E5%8B%95%E4%BD%9C%E3%81%97%E3%81%AA%E3%81%8B%E3%81%A3%E3%81%9F%E5%8E%9F%E5%9B%A0%E3%81%A8%E5%AF%BE%E5%87%A6%E6%B3%95/raw%E8%A8%AD%E5%AE%9A.png "raw設定")

