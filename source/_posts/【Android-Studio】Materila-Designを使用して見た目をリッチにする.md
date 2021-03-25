---
title: 【Android Studio】Materila Designを使用して見た目をリッチにする
date: 2021-03-16 22:56:54
tags:
- Android Studio
- Kotlin
---
## 参考資料
- 参考ドキュメント
[https://material.io/design](https://material.io/design)
[https://github.com/material-components/material-components-android](https://github.com/material-components/material-components-android)

- スタートガイド
[https://github.com/material-components/material-components-android/blob/master/docs/getting-started.md](https://github.com/material-components/material-components-android/blob/master/docs/getting-started.md)

## 手順
1. build.gradle(Project:プロジェクト名)に`google()`が含まれているかチェック

    ```jsx
    allprojects {
        repositories {
            google()     <- これが記述してあればOK
        }
    }
    ```

2. build.gradle(Module:app)にライブラリを記述

    `<version>`の部分は以下のURLを参考にする
		- [https://mvnrepository.com/artifact/com.google.android.material/material](https://mvnrepository.com/artifact/com.google.android.material/material)

    ```jsx
    dependencies {
    	...
    	implementation 'com.google.android.material:material:<version>'
    	...
    }
    ```

3. 一度ビルドする
4. styles.xmlを書き換えてみる

    生成したての状態

    ```jsx
    <resources>
        <!-- Base application theme. -->
        <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
            <!-- Customize your theme here. -->
            <item name="colorPrimary">@color/colorPrimary</item>
            <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
            <item name="colorAccent">@color/colorAccent</item>
        </style>

    </resources>
    ```

    これの`<style>`ブロックの`parent`パラメーターを書き換えることで、テーマを変更できる

    ```jsx
    <style name="AppTheme" parent="Theme.MaterialComponents.DayNight.NoActionBar">
    ```

    このテーマを書き換えることで、`<Button>` と `<AutoCompleteTextView>`の XML コンポーネントをそれぞれ `<MaterialButton>` と `<MaterialAutoCompleteTextView>` に置き換えます。

    他のコンポーネントのテーマを変えるには、XMLに直接記述する必要がある
