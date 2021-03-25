---
title: 自作ソート【Swift】
date: 2021-02-24 18:44:14
tags:
- Swift
---
## 目的
- ソートアルゴリズムの基本を身につける
- Swiftになれる

## 要件
- 数字をソートアルゴリズムを使ってソートする(Swiftのソート関数は使わない)
- 日本語ひらがな、アルファベット小文字の1文字をソートする
- インプットは数字の場合と、文字の場合がある (ただし、文字と数字の組み合わせはない、どちらか1種類のみの羅列が入力される)
- 最後に昇順 or 降順の指定がある
- ユーザーは決まった手順を守るとは限らないので、その場合の例外の対応方法の組み込み (無理矢理処理しても、エラーを返してもいい)k

## コード
```swift
import UIKit

let testValue1:String = "24,6723,23,111,43,1,昇順"
let testValue2:String = "え,い,う,か,と,昇順"
let testValue3:String = "-2,-22347999,あ,2,い,3,-1,ああ,昇順"

enum OrderType:String{
    case none = "例外"
    case ascending = "昇順"
    case descending = "降順"
}

enum ValueType:String{
    case Iregular = "例外"
    case Number = "数字"
    case Charactor = "ローマ字"
    case Japanese = "日本語"
}

//  ============= メイン処理 ==============
//  入力された文字列を分割
var inputValueList = testValue3.split(separator: ",")

//  ソートタイプのチェック
var orderType:OrderType = OrderType(rawValue: String(inputValueList.last ?? "")) ?? OrderType.none

if(orderType == OrderType.none){
    print("ソート方法を指定してください")
    print("指定がないため、昇順ソートを行います")
    
    orderType = OrderType.ascending
}else{
    //  ソート指定は邪魔なので取り除く
    inputValueList.removeLast()
}

//  入力文字列のタイプを判定
let valueType = CheckValueType(targetValueList: inputValueList)

//  ソート処理
var sortedNumberList:Array<Substring> = Array<Substring>()
sortedNumberList = Sort(targetNumberList:inputValueList)

//  何をソートしたか表示
switch valueType {
case .Number:
    print(ValueType.Number.rawValue + "ソート完了")
case .Charactor:
    print(ValueType.Charactor.rawValue + "ソート完了")
case .Japanese:
    print(ValueType.Japanese.rawValue + "ソート完了")
case .Iregular:
    print(ValueType.Iregular.rawValue + "ソート完了")
}

//  ソートタイプによって出力を切り替え
switch orderType {
case .ascending:
    print(sortedNumberList)
case .descending:
    print(Array(sortedNumberList.reversed()))
case .none:
    print("ソート失敗")
}

//  =====================================

//  ============== メソッド ===============
//  値のタイプを判定
func CheckValueType(targetValueList:Array<Substring>)-> ValueType{
    var retVal : ValueType = ValueType.Iregular
    let targetValueCount = targetValueList.count
    
    var numberCount = 0
    var charCount = 0
    var japaneseCount = 0
    
    //  数字の並びかチェック
    for i in 0...inputValueList.count - 1{
        let str:Int = Int(inputValueList[i].cString(using: .shiftJIS)!.first!)
        if(str >= 48 && str <= 57){         //  数字
            numberCount += 1
        }else if(str >= 97 && str <= 122){  //  小文字
            charCount += 1
        }else if(str >= 65 && str <= 90){   //  大文字
            charCount += 1
        }else if(str == -125){              //  ひらがな
            japaneseCount += 1
        }else if(str == -126){              //  カタカナ
            japaneseCount += 1
        }
    }
    
    
    if(numberCount == targetValueCount){
        retVal = ValueType.Number
    }else if(charCount == targetValueCount){
        retVal = ValueType.Charactor
    }else if(japaneseCount == targetValueCount){
        retVal = ValueType.Japanese
    }else{
        retVal = ValueType.Iregular
    }
    
    return retVal
}

//  ソート処理
func Sort(targetNumberList:Array<Substring>)->Array<Substring>{
    
    var sortList = targetNumberList
    var isChange = false
    
    for index in 0...sortList.count - 1{
        
        if(index + 1 == sortList.count)
        {
            break
        }
        
        let firstList = sortList[index].cString(using: .shiftJIS)!
        var firstSign = 1
        var firstJapaneseSign = 0
        
        let firstCheckValue = firstList.first!
        if(firstCheckValue == 45 )   //  マイナス符号
        {
            firstSign = -1
        }
        
        if(firstCheckValue == -125 ||  //  ひらがな
            firstCheckValue == -126)    //  カタカナ
        {
            firstJapaneseSign = Int(firstCheckValue) * -1
        }
        
        
        var first:Int = 0
        
        for fc in firstList{
            first += Int(fc) * firstSign
        }
        
        if(firstJapaneseSign != 0){
            first  *= firstJapaneseSign
        }
        
        
        let secondList = sortList[index+1].cString(using: .shiftJIS)!
        
        var secondSign = 1
        var secondJapaneseCheckSign = 0
        
        let secondCheckValue = secondList.first!
        if(secondCheckValue == 45)   //  マイナス符号
        {
            secondSign = -1
        }
        
        if(secondCheckValue == -125 ||  //  ひらがな
            secondCheckValue == -126)    //  カタカナ
        {
            secondJapaneseCheckSign = Int(secondCheckValue) * -1
        }
        var second:Int = 0
        
        for sc in secondList{
            second += Int(sc) * secondSign
        }
        
        if(secondJapaneseCheckSign != 0){
            second *= secondJapaneseCheckSign
        }

        
        let firstValue = sortList[index]
        let secondValue = sortList[index+1]
        
        if(first > second)
        {
            isChange = true

            sortList[index] = secondValue
            sortList[index + 1] = firstValue
        }
    }
    
    if(isChange){
        sortList = Sort(targetNumberList: sortList)
    }
    
    return sortList
}
//  =======================================
```

## 備考（感想）
- 文字コード変換する時に全てShiftJISのコードで変換されてしまった(未解決)
- 今回使ったソートアルゴリズムは「バブルソート」
-	小数に対応していない
