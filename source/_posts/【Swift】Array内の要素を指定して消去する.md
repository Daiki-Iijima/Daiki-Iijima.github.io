---
title: 【Swift】Array内の要素を指定して消去する
date: 2021-03-01 23:16:50
tags:
- Swift
---
## もくじ
1. removeAllを使用する
	- 短くかける
2. for文を使用する
	- ちょっと冗長
3. その他の参考

## 注意
この方法の場合、比較する要素に一致するデータは`全て配列から消去`されます

## 1.removeAllを使用する
`removeAll(where:)メソッド`を使用し、要素を比較して一致している値全てを消去する

```swift
//	配列定義
var testArray :Array<String> = Array<String>()

//	要素追加
testArray.append("test")
testArray.append("kemono")

//	testと一致する要素を全て消去
testArray.removeAll(where: {$0 == "test"})
```

## 2.for文を使用する
`for文`を使用して配列内の要素を列挙して、要素を比較した結果一致している配列内要素を全て消去する

```swift
//	配列定義
var testArray :Array<String> = Array<String>()

//	要素追加
testArray.append("test")
testArray.append("test")
testArray.append("kemono")

//	要素を操作するのでコピーを作成して、それをfor文で列挙する
let copyArray = testArray

//	一致する要素を消去
for i in 0...copyArray.count - 1{
    if(copyArray[i] == "test"){
        testArray.remove(at: i)
    }
}
```

## 3.その他の参考
- https://qiita.com/fuziki/items/e8b1bb5b2dc8c8f43041
