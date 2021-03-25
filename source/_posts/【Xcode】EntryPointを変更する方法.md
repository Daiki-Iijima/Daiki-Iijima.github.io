---
title: 【Xcode】EntryPointを変更する方法
date: 2021-03-01 22:59:11
tags:
- Xcode
- Swift
---
## もくじ
0. 環境
1. Entry Pointとは
2. StoryBordから変更する
3. コードから変更する
4. [おまけ]初回起動時のみ特定の画面を表示させる

## 0. 環境
- MacBook Air M1
- Xcode 12.4

## 1. Entry Pointとは
- プログラムの開始される位置
- この記事では開始される画面の位置も含まれる
### 画面上で見ると以下の画像の矢印部分がEntry Pointを表している
![EntryPointの矢印](/2021/03/01/【Xcode】EntryPointを変更する方法/EntryPointの矢印.png "EntryPointの矢印")

### アシスタントエディタで確認すると以下赤枠部分
![EntryPointのアシスタントエリアでの表示](/2021/03/01/【Xcode】EntryPointを変更する方法/EntryPointのアシスタントエリアでの表示.png "EntryPointのアシスタントエリアでの表示")

## 2. StoryBordから変更する

### ドラックアンドドロップで矢印を移動させる
![EntryPoint変更(マウス).gif](/2021/03/01/【Xcode】EntryPointを変更する方法/EntryPoint変更(マウス).gif "EntryPoint変更(マウス)")

### Utilites areaから移動させる
`Attributes inspector内`の`Is Initial View Controller`にチェクを入れる
![EntryPoint変更(Inspector)](/2021/03/01/【Xcode】EntryPointを変更する方法/EntryPoint変更(Inspector).gif "EntryPoint変更(Inspector)")
 
## 3. コードから変更する
### 1. Main.storybordの遷移させたいViewControllerに`Storyboad ID`を設定する
- `Identity Inspector` 内の`Sotryboard ID`を設定

![Inspector.png](/2021/03/01/【Xcode】EntryPointを変更する方法/Inspector.png "Inspector.png")

- 今回はこのように設定
	- 1画面目 : FirstView
	- 2画面目 : SecondView

### 2. SceneDelegate.swift
1. 何も変更していないデフォルトの状態だとこのようなコードになっていると思います
	```swift
	import UIKit
	
	class SceneDelegate: UIResponder, UIWindowSceneDelegate {
	
	    var window: UIWindow?
	
	
	    func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
	        // Use this method to optionally configure and attach the UIWindow `window` to the provided UIWindowScene `scene`.
	        // If using a storyboard, the `window` property will automatically be initialized and attached to the scene.
	        // This delegate does not imply the connecting scene or session are new (see `application:configurationForConnectingSceneSession` instead).
	        guard let _ = (scene as? UIWindowScene) else { return }
	    }
	
	    func sceneDidDisconnect(_ scene: UIScene) {
	        // Called as the scene is being released by the system.
	        // This occurs shortly after the scene enters the background, or when its session is discarded.
	        // Release any resources associated with this scene that can be re-created the next time the scene connects.
	        // The scene may re-connect later, as its session was not necessarily discarded (see `application:didDiscardSceneSessions` instead).
	    }
	
	    func sceneDidBecomeActive(_ scene: UIScene) {
	        // Called when the scene has moved from an inactive state to an active state.
	        // Use this method to restart any tasks that were paused (or not yet started) when the scene was inactive.
	    }
	
	    func sceneWillResignActive(_ scene: UIScene) {
	        // Called when the scene will move from an active state to an inactive state.
	        // This may occur due to temporary interruptions (ex. an incoming phone call).
	    }
	
	    func sceneWillEnterForeground(_ scene: UIScene) {
	        // Called as the scene transitions from the background to the foreground.
	        // Use this method to undo the changes made on entering the background.
	    }
	
	    func sceneDidEnterBackground(_ scene: UIScene) {
	        // Called as the scene transitions from the foreground to the background.
	        // Use this method to save data, release shared resources, and store enough scene-specific state information
	        // to restore the scene back to its current state.
	    }
	
	
	}
	```
2. `scene`メソッド内に以下のコードのコードを追記します
	- この時、`guard let _ =`の`_`の部分を`window`に変更しています。

	```swift
	func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
		// Use this method to optionally configure and attach the UIWindow `window` to the provided UIWindowScene `scene`.
		// If using a storyboard, the `window` property will automatically be initialized and attached to the scene.
		// This delegate does not imply the connecting scene or session are new (see `application:configurationForConnectingSceneSession` instead).
		guard let windowScene = (scene as? UIWindowScene) else { return }

		window = UIWindow(windowScene: windowScene)
		let storybard = UIStoryboard(name: "Main",bundle: nil)
  	
		//  初めて起動しているか
		if(lanchIsFIrstTme()){
		    window?.rootViewController = storybard.instantiateViewController(identifier: "FirstView")
		    firstLanch()
		}else{
		    window?.rootViewController = storybard.instantiateViewController(identifier: "SecondView")
		}
		
		window?.makeKeyAndVisible()
	}
	```

## 4. [おまけ]初回起動時のみ特定の画面を表示させる
一つ前で実装した切り替え処理とユーザーデフォルト機能を組み合わせて、初回起動かどうかを判定する

- 確認用メソッドと登録用メソッドを作成
	```swift
	private let STORED_KEY = "lanched"
	
	func firstLanch(){
	    return UserDefaults.standard.set(true,forKey: STORED_KEY)
	}
	
	func lanchIsFIrstTme() -> Bool{
	    return !UserDefaults.standard.bool(forKey: STORED_KEY)
	}
	```

- 一つ前で実装したコードを改変
	```swift
	func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
	    // Use this method to optionally configure and attach the UIWindow `window` to the provided UIWindowScene `scene`.
	    // If using a storyboard, the `window` property will automatically be initialized and attached to the scene.
	    // This delegate does not imply the connecting scene or session are new (see `application:configurationForConnectingSceneSession` instead).
	    guard let windowScene = (scene as? UIWindowScene) else { return }
	
	    window = UIWindow(windowScene: windowScene)
	    let storybard = UIStoryboard(name: "Main",bundle: nil)
	    
	    //  初めて起動しているか
	    if(lanchIsFIrstTme()){
	        window?.rootViewController = storybard.instantiateViewController(identifier: "FirstView")
	        firstLanch()
	    }else{
	        window?.rootViewController = storybard.instantiateViewController(identifier: "SecondView")
	    }
	    
	    window?.makeKeyAndVisible()
	}
	```
### こんな感じになればOK
![最終確認](/2021/03/01/【Xcode】EntryPointを変更する方法/最終確認.gif "最終確認")
## 参考
https://stackoverflow.com/questions/10428629/programmatically-set-the-initial-view-controller-using-storyboards/47691073
