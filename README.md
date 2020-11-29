# Hackintosh
[HELP] ASRock Z390M-PRO4, i5-9400F, MSI RX570

こんにちは、初心者です。シャットダウン とスリープ復帰の問題で困っています。 ASRock Z390M-PRO4とi5-9400FでCatalina 10.15.7を入れています。

インストール成功してBluetoothやEthernet、iMassage等が機能する程度まで成功しているのですが、シャットダウン、スリープがうまくいきません。

###　シャットダウンについて
シャットダウンをしてPCが一度眠ったかな（CPUファンの音が一瞬消える）と思ったら再度起動します。10回に１回くらいの割合でうまくいくことはあります。  

###　スリープについて

スリープ自体はするのですが、スリープを復帰させた後勝手に再起動がかかります。  

一応自分でできる原因特定作業として
 - シャットダウン時にUSBを全て抜く
 - Bluetoothをオフにする（USBドングルを抜く）
 - Ethernetを抜く

などしてみたのですが、変化ありませんでした。



アドバイスお願いいたします。  

構成

- ASRock Z390M Pro4

- Core i5-9400F

- MSI RX570

  ​	SMBIOS iMac 19,1



BIOS設定

- BIOS version P4.30
- VT-d --> Disabled
- Onboard WAN Device --> Disabled
- Serial Port --> Disabled
- XHCI Hand-off --> Enabled
- CSM(Compatibility Support Module) --> Disabled

macOS Catalina 10.15.7

導入はSarkさんが提供していくれているもの（https://github.com/sarkrui/Z390M-Pro4-i7-9700K-Hackintosh）を参考にして行いました。ESPの中身はEFI/Clover/以下のファイルを上のリンクからコピーして、基本的にそのまま使っています。

手を加えた内容は以下の通りです。

- WhatEverGreen.kext
  	起動時に画面が乱れることがあったので追加しました。
- USBPorts.kext
  	Hackintoolsで作成し直しました。
- SSDT.aml
  	CPUのパワーマネジメント用にssdtPRGen.shを使って作成しました。
- config.plist
  	最初のUSBから起動する際に使用したconfig.plistを、Sarkさんのconfig.plistに近づけるように編集して行っています。

