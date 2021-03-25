---
title: div属性について
date: 2021-02-23 21:33:43
tags: HTML
---
# dev(devision)要素について
- `dev`要素は、複数のブロックに対して、レイアウトを適応させることができる
- `\<dev\>\</dev\>`で囲んだブロック全体にレイアウトが適応させる
- 基本的な概念は内部CSSの`class`や`id`と同じ

```html
<html>
 <head>
  <style>
   .A{
    background:pink;
    }
   #B{
    background:yellow;
    }
  </style>	
 </head>
 <body>
  <!--classを使用-->
  <div class="A">
    <h1>これは見出しです</p>
    <p>これは見出しに対する本文です</p>
  </div>

  <!--idを使用-->
  <div id="B">
    <h1>これは見出し2です</p>
    <p>これは見出し2に対する本文です</p>
  </div>

 </body>
</html>
```
