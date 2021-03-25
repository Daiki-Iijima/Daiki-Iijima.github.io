---
title: 【Kotlin】View内のコンポーネントの取得方法
date: 2021-03-12 02:07:04
tags:
- Android
- Android Studio
- Kotlin
---
## Javaっぽく取得する

データバインディングというらしい？

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
				
				// コンポーネントに設定したID(textView)からTextViewを取得する
				val textView = findViewById(R.id.textView) as TextView
}
```

## Kotlinっぽく取得する（Kotlin Android Extensions使用）

### Kotlin Android Extensions

Kotlinが公式で提供している、Androidアプリ開発をサポートしてくれる拡張機能
[https://archive-blog.yagi2.dev/2017/10/18/good-bye-findviewbyid.html](https://archive-blog.yagi2.dev/2017/10/18/good-bye-findviewbyid.html)

```kotlin
// Inportする必要がある
// <layout>には取得したいLayoutXMLの名前を指定
import kotlinx.android.synthetic.main.<layout>.*

override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

				// 後はViewないで指定した、コンポーネントのIDから呼び出せる
				textView.text = "テストだよ"
}
```
