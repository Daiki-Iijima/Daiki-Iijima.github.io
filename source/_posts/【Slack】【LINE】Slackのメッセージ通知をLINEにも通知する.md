---
title: 【Slack】【LINE】Slackのメッセージ通知をLINEにも通知する
date: 2021-06-18 22:59:50
tags:
- Slack
- LINE
- GAS
---
# 目次
<!-- toc -->
<!-- more -->

# 環境
- Slacki
  - アプリ : Outgoing Webhook
- LINE
  - サービス : LINE Notify
- GAS(Google Apps Script)

# 手順
## 1. Google Action Scriptを作成する
Googleドライブから作成できます。

```
Googleドライブ -> 左上のプラスボタン(新規ボタン) -> その他 -> Google Apps Script
```

![Googleドライブ](/2021/06/18/%E3%80%90Slack%E3%80%91%E3%80%90LINE%E3%80%91Slack%E3%81%AE%E3%83%A1%E3%83%83%E3%82%BB%E3%83%BC%E3%82%B8%E9%80%9A%E7%9F%A5%E3%82%92LINE%E3%81%AB%E3%82%82%E9%80%9A%E7%9F%A5%E3%81%99%E3%82%8B/Google%E3%83%89%E3%83%A9%E3%82%A4%E3%83%96.png "Googleドライブ")

## 2. コードを記述する
この時点では、コード内の`「」`で囲まれている以下に列挙している部分のトークンは取得していないので、空白で大丈夫です
- 「SlackのOutgoing Webhookのトークン」
- 「LINEのトークン」

```javascript
function doPost(e) {

  //投稿のトークン取得
  var t = e.parameter.token;

  //トークンが一致しているか
  if( t != "「SlackのOutgoing Webhookのトークン」")
  {return;}

   //各種情報を取得
   var chName = e.parameter.channel_name;
   var userName = e.parameter.user_name;
   var text = e.parameter.text;
   //@lineの部分はいらないから削除しとく
   text =text.substring(5);
  var msg = "\n【発言のあったチャンネル】: "+chName+
    "\n【発言者】 : "+userName+ "\n【内容】\n"+text;
  //送信
  send(msg);
}

function send(message)
{
  //lineトークン
  var token = "「LINEのトークン」";

  var op =
      {
        "method" : "post",
        "payload": "message=" + message,
        "headers":{"Authorization" : "Bearer " + token}
      };
UrlFetchApp.fetch("https://notify-api.line.me/api/notify",op);
}
```

## 3. LINEのLINE Notifyの登録
使用しているLINEアカウントでログイン後、以下の手順でNotifyアプリの登録を行います。

```
右上の名前クリック -> マイページ -> アクセストークンの発行 -> トークン名、ルームの選択
```

![LINE設定_1](/2021/06/18/【Slack】【LINE】Slackのメッセージ通知をLINEにも通知する/LINE設定_1.png "LINE設定_1")
![LINE設定_2](/2021/06/18/【Slack】【LINE】Slackのメッセージ通知をLINEにも通知する/LINE設定_2.png "LINE設定_2")
![LINE設定_3](/2021/06/18/【Slack】【LINE】Slackのメッセージ通知をLINEにも通知する/LINE設定_3.png "LINE設定_3")

この手順で`発行されるトークンをメモしておきます。`

## 4. SlackのOutgoing Webhookの設定
1. 以下のURLから、Slack Appの管理ページに飛びます。
- https://ワークスペース名-workspace.slack.com/services

2. 画面上部にある、`App ディレクトリの検索`で`Outgoing Webhook`を検索します。

3. Outgoing WebhookをSlackに追加します。
![Slack設定_1](/2021/06/18/【Slack】【LINE】Slackのメッセージ通知をLINEにも通知する/Slack設定_1.png "Slack設定_1")

4. そのまま設定を開き、画像の赤枠の欄の`トークン`をメモしておきます。

![Slack設定_2](/2021/06/18/【Slack】【LINE】Slackのメッセージ通知をLINEにも通知する/Slack設定_2.png "Slack設定_2")

5. 画面を開いたままでGoogle Apps Scriptに移動します。

## 5. Google Apps Scriptのトークン部分を埋めてデプロイ
1. メモしたトークンを追記する
  - 「SlackのOutgoing Webhookのトークン」
  - 「LINEのトークン」

```javascript
function doPost(e) {

  //投稿のトークン取得
  var t = e.parameter.token;

  //トークンが一致しているか
  if( t != "「SlackのOutgoing Webhookのトークン」")
  {return;}

   //各種情報を取得
   var chName = e.parameter.channel_name;
   var userName = e.parameter.user_name;
   var text = e.parameter.text;
   //@lineの部分はいらないから削除しとく
   text =text.substring(5);
  var msg = "\n【発言のあったチャンネル】: "+chName+
    "\n【発言者】 : "+userName+ "\n【内容】\n"+text;
  //送信
  send(msg);
}

function send(message)
{
  //lineトークン
  var token = "「LINEのトークン」";

  var op =
      {
        "method" : "post",
        "payload": "message=" + message,
        "headers":{"Authorization" : "Bearer " + token}
      };
UrlFetchApp.fetch("https://notify-api.line.me/api/notify",op);
}
```

2. 新規デプロイのための設定をする
画面上部のデプロイから新しいデプロイを選択

![GAS設定_1](/2021/06/18/【Slack】【LINE】Slackのメッセージ通知をLINEにも通知する/GAS設定_1.png "GAS設定_1")

種類の選択から、`ウェブアプリ`を選択

![GAS設定_2](/2021/06/18/【Slack】【LINE】Slackのメッセージ通知をLINEにも通知する/GAS設定_2.png "GAS設定_2")

アクセスできるユーザーを`全員`に設定

![GAS設定_3](/2021/06/18/【Slack】【LINE】Slackのメッセージ通知をLINEにも通知する/GAS設定_3.png "GAS設定_3")

3. URLをメモする
デプロイが成功すると、アプリのURLが生成されるのでコピーします。

![GAS設定_4](/2021/06/18/【Slack】【LINE】Slackのメッセージ通知をLINEにも通知する/GAS設定_4.png "GAS設定_4")

## 6. Outgoing WebhookにGASアプリの紐付け
赤枠で囲まれている欄にGASアプリのURLを貼り付けて、設定を保存します。

![Slack紐付け](/2021/06/18/【Slack】【LINE】Slackのメッセージ通知をLINEにも通知する/Slack紐付け.png "Slack紐付け")

## 7. 試してみる
今回のキーワード設定だと、`@line`を先頭につけて投稿したメッセージがLINEにも投稿されることになります。


# 参考
- https://qiita.com/AzuQiita/items/35f43b8a5609f037bbef
