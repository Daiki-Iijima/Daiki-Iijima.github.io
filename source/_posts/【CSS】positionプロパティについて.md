---
title: 【CSS】positionプロパティについて
date: 2021-03-05 00:50:20
tags:
- CSS
---
# postion属性とは
- 要素の位置を指定するための属性

## 指定する方法の種類
1. relative : 相対位置への配置
	- その要素が本来配置される位置からの相対位置
2. absolute : 絶対位置への配置
	- 画面上の座標
3. fixed : 絶対位置への配置 + スクロールされても位置が固定

## 指定方法
1. まずは位置の指定方法を記述する
```html
position: relative;
```
2. どちらの方向にどれだけ動かすかを指定する
```html
top: 200px;
```

まとめると
```html
.test{
	position: relative;
	top: 200px;
}
```

## relativeとabsoluteの違い
### イメージ
コード
```html
<!DOCTYPE html>
<html>
	<head>
		<title>position</title>
			<style type="text/css">

				.first-section{
					background: lightgreen;
					width: 100px;
					height: 100px;
					position:relative;
					left:200px;
					top:200px;
				}
				.second-section{
					background: pink;
					width: 100px;
					height: 100px;
					position:absolute;
					left:200px;
					top:200px;
				}
				.third-section{
					background: red;
					width: 100px;
					height: 100px;
					position:fixed;
					left:400px;
					top:400px;
				}
		</style>
	</head>
	<body>
		<p>a</p>
		<p>a</p>
		<p>a</p>
		<p>a</p>
		<p>a</p>
		<div class="first-section">
			<p>1</p>
		</div>
		<div class="second-section">
			<p>2</p>
		</div>
		<div class="third-section">
			<p>3</p>
		</div>
	</body>
</html>
```

![参考](/2021/03/05/【CSS】positionプロパティについて/position.png "参考")

# 便利な属性

## 奥行きの指定
`z-index`属性を使って指定する
	- 大きい値を設定したスタイルを適応した要素が上に描画される
```html
.test{
	position: relative;
	top: 200px;
	z-index: 1;
}

.test2{ <!--こっちが上に表示させる-->
	position: relative;
	top: 200px;
	z-index: 2;
}
```

## 透明度の指定
- `opacity`属性を使って`0~1`までの間で指定する
```html
.test{
	position: relative;
	top: 200px;
	opasity: 0.5; <!--透明度を指定-->
}
```
