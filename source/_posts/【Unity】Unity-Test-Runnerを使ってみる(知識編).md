---
title: 【Unity】Unity Test Runnerを使ってみる(知識編)
date: 2021-06-14 03:41:35
tags:
- Unity
- Test Runner
---
# 目次
<!-- toc -->
<!-- more -->

# 環境
- Unity 2019.4.9

# Unity Test Runnerとは
Unityでテストを実行するための仕組みです。

NUnitという.NETで使用できるテストフレームワークが使用されています。

# 主な特徴と注意点
Unity Test Runnerは、`EditMode`と`PlayMode`という2つのモードでテストができます。

ここでは主に、2つのモードで共通の動作を紹介します。

## 1. NUnitとの違い
NUnitでは、テスト用のクラスに`TestFixture`属性を設定しますが、Unity Test Runnerではその指定は必要ありません。

## 2. 使用できるAttributeについて
基本的に試用できるAttributeはNUnitが用意している属性のものになります。

以下の項目はよく使いそうな項目をピックアップしています。

### 「イニシャライズ」「ファイナライズ」関係
| 属性                | 機能                           | 参考                                                                                  | 
|-------------------|------------------------------|-------------------------------------------------------------------------------------| 
| [OneTimeSetUp]    | クラス内の最初のテストが実行される前に一度だけ実行される | https://docs.nunit.org/articles/nunit/writing-tests/attributes/onetimesetup.html    | 
| [OneTimeTearDown] | クラス内の最後のテストが実行された後に一度だけ実行される | https://docs.nunit.org/articles/nunit/writing-tests/attributes/onetimeteardown.html | 
| [SetUp]           | クラス内の各テスト実行前にそれぞれ実行される       | https://docs.nunit.org/articles/nunit/writing-tests/attributes/setup.html           | 
| [TearDown]        | クラス内の各テスト実行後にそれぞれ実行される       | https://docs.nunit.org/articles/nunit/writing-tests/attributes/teardown.html        | 

### テスト本体関係
| 属性               | 機能                                               | 参考                                                                                 | 
|------------------|--------------------------------------------------|------------------------------------------------------------------------------------| 
| [Test]           | 単純なテスト                                           | https://docs.nunit.org/articles/nunit/writing-tests/attributes/test.html           | 
| [UnityTest]           | コルーチンでテストが実行できる                                           | https://docs.nunit.org/articles/nunit/writing-tests/attributes/test.html           | 
| [TestCase]       | テストメソッドに引数を渡してテストケースを量産                          | https://docs.nunit.org/articles/nunit/writing-tests/attributes/testcase.html       | 
| [TestCaseSource] | 定義しておいたテストケースを使う（引数/戻り値が定数でない場合は[TestCase]が使えない） | https://docs.nunit.org/articles/nunit/writing-tests/attributes/testcasesource.html | 

### 引数や値の生成関係
| 属性       | 機能          | 参考                                                                         | 
|----------|-------------|----------------------------------------------------------------------------| 
| [Range]  | 指定の範囲内の値を生成 | https://docs.nunit.org/articles/nunit/writing-tests/attributes/range.html  | 
| [Values] | 値の組み合わせを生成  | https://docs.nunit.org/articles/nunit/writing-tests/attributes/values.html | 
| [Random] | ランダムな値を生成   | https://docs.nunit.org/articles/nunit/writing-tests/attributes/random.html | 

### その他
| 属性            | 機能                         | 参考                                                                           | 
|---------------|----------------------------|------------------------------------------------------------------------------| 
| [Category]    | 実行したいテストをまとめることができる        | https://docs.nunit.org/articles/nunit/writing-tests/attributes/category.html | 
| [Timeout]     | テストのタイムアウトまでの時間を指定できる（ミリ秒） | https://docs.nunit.org/articles/nunit/writing-tests/attributes/timeout.html  | 
| [Desctiption] | テストに対して説明文を書ける             | https://docs.nunit.org/articles/nunit/writing-tests/attributes/timeout.html  | 
| [Ignore]      | テストが無視され実行されなくなる           | https://docs.nunit.org/articles/nunit/writing-tests/attributes/ignore.html   | 
| [Order]       | まとめて実行する際の実行順を指定できる        | https://docs.nunit.org/articles/nunit/writing-tests/attributes/order.html    | 

## AssertはUnityが用意しているものを使う
Unityが用意しているAssertを使用するほうがUnity Test Runnerに最適化されているます。

using部分に以下のコードを追記しておくと、意識せずに`Unity版Assert`を使用できます。

```C#
using Assert = UnityEngine.Assertions.Assert;
```

### 使用できるStaticメソッド一覧
- https://docs.unity3d.com/ja/current/ScriptReference/Assertions.Assert.html

| メソッド                     | 内容                    | 参考                                                                           | 
|--------------------------|-------------------------------------------|-------------------------------------------------------------------| 
| AreApproximatelyEqual    | 値が等しいことを表明します。                            | https://docs.unity3d.com/ja/current/ScriptReference/Assertions.Assert.AreApproximatelyEqual.html    | 
| AreEqual                 | 値がほぼ等しくないことを表明します。                        | https://docs.unity3d.com/ja/current/ScriptReference/Assertions.Assert.AreEqual.html                 | 
| AreNotApproximatelyEqual | 値が等しくないことを表明します。                          | https://docs.unity3d.com/ja/current/ScriptReference/Assertions.Assert.AreNotApproximatelyEqual.html | 
| AreNotEqual              | 条件がfalseの場合はtrueを返します。| https://docs.unity3d.com/ja/current/ScriptReference/Assertions.Assert.AreNotEqual.html              | 
| IsFalse                  | 値がnullではないことを表明します。                       | https://docs.unity3d.com/ja/current/ScriptReference/Assertions.Assert.IsFalse.html                  | 
| IsNotNull                | 値がnullであることを表明します。                        | https://docs.unity3d.com/ja/current/ScriptReference/Assertions.Assert.IsNotNull.html                | 
| IsNull                   | true となる条件のアサート                           | https://docs.unity3d.com/ja/current/ScriptReference/Assertions.Assert.IsNull.html                   | 
| IsTrue                   | true となる条件のアサート                           | https://docs.unity3d.com/ja/current/ScriptReference/Assertions.Assert.IsTrue.html                   | 

# EditModeとPlayModeの違い
## EditMode
- PlayMode(Unityの再生モード)を経由せずに実行されるので、`テストが速い`です。
- `MonoBehaviour`を継承しているスクリプトのテストは`Start()`,`Update()`が呼ばれないので、基本的にできません。
- 非同期テスト([UnityTest])は動作しません。

## PlayMode
- テストの`実行が遅いです`(通常のUnity再生モードを使用するため)
- 実行すると、テスト用のシーンを自動で生成して、テストを実行します。
- `MonoBehaviour`のテストはこちらを使用する必要があります。
- 非同期テスト([UnityTest])が動作します。
