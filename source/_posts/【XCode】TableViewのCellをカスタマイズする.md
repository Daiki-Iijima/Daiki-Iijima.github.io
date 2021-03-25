---
title: 【XCode】TableViewのCellをカスタマイズする
date: 2021-03-14 23:28:07
tags:
- XCode
- Swift
---
## 環境
- MacBook Air M1
- OS : 11.2(20D64)
- XCode : 12.4
- Swift : 5.3.2 

## 参考
- https://rara-world.com/ios-swift-tableview-custom-cell/

## 

### 1. 新規ファイル追加でCocoa Touch Classを選択 
![新規作成](/2021/03/14/【XCode】TableViewのCellをカスタマイズする/新規作成.png "新規作成")

### 2. 作成時の設定
- Class : 好きな名前(今回は`CustomTableViewCell`)
- Subclass of : UITableViewCell
- Also create XIB file : ON
- Language : Swift

![作成時オプション](/2021/03/14/【XCode】TableViewのCellをカスタマイズする/作成時オプション.png "作成時オプション")

２つの新規ファイルが生成されればOK
![作成済みチェック](/2021/03/14/【XCode】TableViewのCellをカスタマイズする/作成済みチェック.png "作成済みチェック")

### 3. CustomTableViewCell.xibを編集
#### Cellにラベルを追加
![ラベル追加](/2021/03/14/【XCode】TableViewのCellをカスタマイズする/ラベル追加.png "ラベル追加")

#### Rostoration IDの設定
任意の文字列でいい(セル生成時に使用する)
![Identifier](/2021/03/14/【XCode】TableViewのCellをカスタマイズする/Identifier.png "Identifier")

### 4. CustomTableViewCell.swiftでラベルの参照を設定
![ラベル参照](/2021/03/14/【XCode】TableViewのCellをカスタマイズする/ラベル参照.gif "ラベル参照")

### 5. Main.storyboardを編集
Table Viewを追加
![TableVIew](/2021/03/14/【XCode】TableViewのCellをカスタマイズする/TableVIew.png "TableVIew")

### 6. ViewController.swiftを編集
#### Main.storyboardで指定した、Table Viewの参照を設定
- 参照時の変数名を今回は`TableView`とする

![TableView参照](/2021/03/14/【XCode】TableViewのCellをカスタマイズする/TableView参照.gif "TableView参照")

#### viewDidLoad()に追記
- UITableViewに対して、delegateと使用する`Cell`の情報を設定
	- TableView.register : 使用するカスタムセルの情報を登録 
		- nibName = 作ったCellのクラス名
		- forCellReuseIdentifier = xibで指定したidentifier名
	- TableView.delegate : 
	- TableView.dataSorce :

```Swift
override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.

        //	ここから
        TableView.register(UINib(nibName: "CustomTableViewCell", bundle: nil), forCellReuseIdentifier: "CustomCell")
        TableView.delegate = self
        TableView.dataSource = self
        //	ここまで
    }
```

#### UITableViewDelegate,UITableViewDataSourceを継承
- どちらのメソッドも、`optional`なので、最低限のメソッドの定義をすれば、他のメソッドは定義しなくてもいい
- UITableViewDelegate : TableView内のデータが選択や生成、編集されたときに呼び出されるメソッドが定義されたプロトコル群
- UITableViewDataSource : テーブルに表示させたいデータを設定するためのプロトコル群

```Swift
class ViewController: UIViewController,UITableViewDelegate,UITableViewDataSource {
	...
}
```

継承すると、エラーが出るはずなので、Fixをクリックしてメソッドを2つ自動生成してもらうと、以下のようなメソッドが自動生成されるはず
```
//	UITableViewDelegateの継承によって生成された
//	TableViewに生成するセル数を設定する(Int型を返す)
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
	Code
}

//	UITableViewDataSourceの継承によって生成された
//	TableViewに表示するセルのデータを設定する(UITableViewCellを返す)
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
	Code
}
```

今回は、生成するセルを`10個`、表示するデータを各セルを`上から数えたときの番号`にする
```
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return 10
}

func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "CustomCell",for: indexPath) as! CustomTableViewCell
    
    cell.Label.text = String(indexPath.row)
    
    return cell
}
```

## 実行した結果
![完成](/2021/03/14/【XCode】TableViewのCellをカスタマイズする/完成.png "完成")

## ViewController.swiftの完成形
```swift
import UIKit

class ViewController: UIViewController,UITableViewDelegate,UITableViewDataSource {
    
    
    @IBOutlet weak var TableView: UITableView!
    
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 10
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "CustomCell",for: indexPath) as! CustomTableViewCell
        
        cell.Label.text = String(1)
        
        return cell
    }
    

    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
        TableView.register(UINib(nibName: "CustomTableViewCell", bundle: nil), forCellReuseIdentifier: "CustomCell")
        TableView.delegate = self
        TableView.dataSource = self
    }


}
```
