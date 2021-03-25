---
title: 【Ubuntu】キーボードの初期設定
date: 2021-03-11 18:55:00
tags:
- Linux
- Ubuntu
---
## Ubuntu Serverで使用するキーボードレイアウトを日本語配列に変更する
1. `sudo dpkg-reconfigure keyboard-configuration`を入力
	```shell-session
	$ sudo dpkg-reconfigure keyboard-configuration
	```

- dpkg-reconfigure : 指定した`Debian`パッケージが`debconf`を採用している場合に、パッケージの再設定をすることができるコマンド
	- `debconf`に対応しているリストは`ls /var/lib/dpkg/info/*.config`でみることができる
- keyboard-configuration : キーボードのレイアウト設定ファイル


### ここからは矢印キーとEnterキーで操作する(GUI風になる)
2. Generic 105-key (Intl)PCを選択
![2](/2021/03/11/【Ubuntu】キーボードの初期設定/2.png "2")

3. Japaneseを選択
![3](/2021/03/11/【Ubuntu】キーボードの初期設定/2.png "3")

4. Japaneseを選択
![4](/2021/03/11/【Ubuntu】キーボードの初期設定/2.png "4")

5. `/etc/default/keyboard`の設定を書き換えている場合表示される
- キーボードオプションを維持する場合は`Yes`を選択、初期化していい場合は`No`を選択
![5](/2021/03/11/【Ubuntu】キーボードの初期設定/5.png "5")

6. 「The default for the keyboard layout」を選択
![6](/2021/03/11/【Ubuntu】キーボードの初期設定/6.png "6")

7. 「No compose key」を選択するとコンソール画面に戻る
![7](/2021/03/11/【Ubuntu】キーボードの初期設定/7.png "7")

8. コンソール画面が表示され必要んな情報を生成してくれるので少し待つ(ネットワークが必要?)
	```shell-session
	Your console font configuration will be updated the next time your system
	boots. If you want to update it now, run 'setupcon' from a virtual console.
	update-initramfs: deferring update (trigger activated)
	Processing triggers for initramfs-tools (0.137ubuntu12) ...
	update-initramfs: Generating /boot/initrd.img-5.8.0-1006-raspi
	....
	
	```
9. 入力待機画面に戻れば成功

## 「Caps Lock」を「Ctrl」に変更する
`/etc/default/keyboard`の`XKBOPTIONS`に以下を書き加える
- デフォルト
```shell-session
XKBOPTIONS=""
```

- 書き換え後
```shell-session
XKBOPTIONS="ctrl:nocaps"
```
