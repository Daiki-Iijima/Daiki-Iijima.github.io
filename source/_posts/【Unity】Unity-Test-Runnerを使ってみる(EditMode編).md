---
title: 【Unity】Unity Test Runnerを使ってみる(EditMode編)
date: 2021-06-15 22:19:23
tags:
- Unity
- Test Runner
---
# 目次
<!-- toc -->
<!-- more -->

# 手順
## 1. Unity Test RunnerのWindowを表示させる

以下の手順でWindowを表示させます。
```
Window -> General -> Test Runner
```

![手順1](/2021/06/15/【Unity】Unity-Test-Runnerを使ってみる(EditMode%E7%B7%A8)/手順1.png "手順1")

## 2. Test用のファイルを生成する
Test Runner Windowから自動でテストに必要なファイルを生成します。

下の画像のように、一番上のタブの`EditMode`を選択(白くなります)して、中段にある`Create EditMode Test Assembly Folder`を押下してファイルを生成します。

![手順2](/2021/06/15/【Unity】Unity-Test-Runnerを使ってみる(EditMode%E7%B7%A8)/手順2.png "手順2")

Assetsフォルダに`フォルダ`が生成されます。このときにつける名前はデフォルトで、`Tests`ですが、名前は変更しても構いません。

`Tests`でフォルダを生成すると、`Tests.asmdef`というファイルが生成されます。(フォルダ名.asmdef)

### .asmdefファイルとはなにか

## 3. テスト用スクリプトファイルの作成
Editorフォルダを作成し、その中で`C# Test Script`を作成します。

```
右クリック -> Create -> Testing -> C# Test Script
```

## 4. コードを記述する準備
EditModeでは、`UnityTest属性(コルーチン)`は使用できないので、テストは`Test属性`を使用してテストを記述します。

生成すると以下のようなコードになっていると思います。
```C#
using System.Collections;
using System.Collections.Generic;
using NUnit.Framework;
using UnityEngine;
using UnityEngine.TestTools;

namespace Tests
{
    public class test
    {
        // A Test behaves as an ordinary method
        [Test]
        public void testSimplePasses()
        {
            // Use the Assert class to test conditions
        }

        // A UnityTest behaves like a coroutine in Play Mode. In Edit Mode you can use
        // `yield return null;` to skip a frame.
        [UnityTest]
        public IEnumerator testWithEnumeratorPasses()
        {
            // Use the Assert class to test conditions.
            // Use yield to skip a frame.
            yield return null;
        }
    }
}
```

初期手順として、以下のようなことをしておくと、スムーズにテストを記述できるようになると思います。
- EditModeでは使えない`UnityTest属性`を使用している`testWithEnumeratorPasses()`を消去します。
- `UnityAssert`を使用できるように、`using`を追加します。
- 不要なコメントを消す

```C#
using System.Collections;
using System.Collections.Generic;
using NUnit.Framework;
using UnityEngine;
using UnityEngine.TestTools;
using Assert = UnityEngine.Assertions.Assert;

namespace Tests
{
    public class test
    {
        [Test]
        public void testSimplePasses()
        {
        }

    }
}
```

## 5. テストを記述して実行する
今回は、テストのために、1+1が2になるかという簡単なテストを書いてみます。

以下のテストは、成功するテストです。
```C#
using System.Collections;
using System.Collections.Generic;
using NUnit.Framework;
using UnityEngine;
using UnityEngine.TestTools;
using Assert = UnityEngine.Assertions.Assert;

namespace Tests
{
    public class test
    {
        [Test]
        public void AddTest()
        {
          Assert.AreEqual(2,1+1);
        }
    }
}
```

Unityの画面に戻り、`Test Runnerウィンドウ`中断の`RunAll`を押下するとテストが実行されます。

![手順5_1](/2021/06/15/【Unity】Unity-Test-Runnerを使ってみる(EditMode%E7%B7%A8)/手順5_1.png "手順5_1")

矢印のトグルボタンを押して深く潜っていくと定義した`AddTestクラス`があると思います。この部分をクリックすると詳細が表示されます。詳細情報はテストが失敗したときに役に立ちます。

以下の画像が先程のテストコードを失敗するように変更してテストした結果です。

```C#
using System.Collections;
using System.Collections.Generic;
using NUnit.Framework;
using UnityEngine;
using UnityEngine.TestTools;
using Assert = UnityEngine.Assertions.Assert;

namespace Tests
{
    public class test
    {
        [Test]
        public void AddTest()
        {
          Assert.AreEqual(0,1+1);
        }
    }
}
```

`Expected 2 == 0`となっています。この右側が成功した場合の値です。左側が計算した結果です。

![手順5_2](/2021/06/15/【Unity】Unity-Test-Runnerを使ってみる(EditMode%E7%B7%A8)/手順5_2.png "手順5_2")
