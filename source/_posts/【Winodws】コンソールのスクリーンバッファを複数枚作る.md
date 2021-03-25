---
title: 【Winodws】コンソールのスクリーンバッファを複数枚作る
date: 2021-03-17 04:33:29
tags:
- Windows
- Windows API
---
## スクリーンバッファとは?
- 実際の文字が書き込まれるバッファのことで、実際にコンソールに描画されるのはこのスクリーンバッファの内容
- コンソールが作成された時点で既定で1つ作成されている(描画されから当たり前)
- 独自のスクリーンバッファを作成して出力を行うことも可能

## CreateConsoleScreenBuffer
```
HANDLE WINAPI CreateConsoleScreenBuffer(
    DWORD dwDesiredAccess,
    DWORD dwShareMode,
    const SECURITY_ATTRIBUTES *lpSecurityAttributes,
    DWORD dwFlags,
    LPVOID lpScreenBufferData
);
```

|引数型|解説|例|
|---|---|---|
|dwDesiredAccess|スクリーンバッファへのアクセス権を指定|GENERIC_READ \| GENERIC_WRITE|
|dwShareMode|スクリーンバッファを共有するための定数を指定(共有しない場合は0)|0|
|*lpSecurityAttributes|SECURITY_ATTRIBUTES構造体のアドレスを指定するが普通はNULLを指定|NULL|
|dwFlags|CONSOLE_TEXTMODE_BUFFERを指定|CONSOLE_TEXTMODE_BUFFER|
|lpScreenBufferData|NULLを指定|NULL|
|戻り値|戻り値のスクリーンバッファハンドルはCloseHandleで閉じる||

## SetConsoleActiveScreenBuffer
- スクリーンバッファをアクティブにしてコンソールに描画

```
BOOL WINAPI SetConsoleActiveScreenBuffer(
    HANDLE hConsoleOutput
);
```

|引数型|解説|例|
|---|---|---|
|hConsoleOutput|スクリーンバッファのハンドル(CreateConsoleScreenBufferの戻り値)を指定||

