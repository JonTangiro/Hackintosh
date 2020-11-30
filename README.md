# Hackintosh
[HELP] ASRock Z390M-PRO4, i5-9400F, MSI RX570

こんにちは、初心者です。シャットダウン とスリープ復帰の問題で困っています。 ASRock Z390M-PRO4とi5-9400FでCatalina 10.15.7を入れています。

インストール成功してBluetoothやEthernet、iMassage等が機能する程度まで成功しているのですが、シャットダウン、スリープがうまくいきません。

## シャットダウンについて  
シャットダウンをしてPCが一度眠ったかな（CPUファンの音が一瞬消える）と思ったら再度起動します。10回に１回くらいの割合でうまくいくことはあります。  

## スリープについて  
スリープという処理はおそらくされているのだと思いますが、すぐ復帰されてしまいます。マザーボードのマーク→ Clover→スリープ復帰という形で立ち上がります。（再起動されているわけではないと思います。）  

一応自分でできる原因特定作業として  
 - シャットダウン時にUSBを全て抜く
 - Bluetoothをオフにする（USBドングルを抜く）
 - Ethernetを抜く  
などしてみたのですが、変化ありませんでした。  

bootmacosの[パワーマネジメント入門](https://bootmacos.com/archives/5107)の記事を参考にして pmset -g assertions を叩いてみました。

```
hoge@hoges-iMac ~ % pmset -g assertions
2020-11-29 18:03:44 +0900 
Assertion status system-wide:
   BackgroundTask                 0
   ApplePushServiceTask           0
   UserIsActive                   1
   PreventUserIdleDisplaySleep    0
   PreventSystemSleep             0
   ExternalMedia                  1
   PreventUserIdleSystemSleep     0
   NetworkClientActive            0
Listed by owning process:
   pid 105(powerd): [0x0000000800088000] 02:06:21 ExternalMedia named: "com.apple.powermanagement.externalmediamounted"  
   pid 148(hidd): [0x0000001f000981b3] 00:00:00 UserIsActive named: "com.apple.iohideventsystem.queue.tickle serviceID:1000004f8 name:AppleUserHIDEventSe product:66EC-S eventType:3"  
	Timeout will fire in 600 secs Action=TimeoutActionRelease
Kernel Assertions: 0x104=USB,MAGICWAKE
   id=500  level=255 0x4=USB mod=1970/01/01 9:00 description=com.apple.usb.externaldevice.14400000 owner=USB2.0 Hub
   id=502  level=255 0x4=USB mod=1970/01/01 9:00 description=com.apple.usb.externaldevice.14100000 owner=66EC-S
   id=503  level=255 0x4=USB mod=1970/01/01 9:00 description=com.apple.usb.externaldevice.14500000 owner=4-Port USB 2.0 Hub
   id=505  level=255 0x4=USB mod=1970/01/01 9:00 description=com.apple.usb.externaldevice.14c00000 owner=HV620
   id=506  level=255 0x4=USB mod=1970/01/01 9:00 description=com.apple.usb.externaldevice.14a00000 owner=4-Port USB 3.0 Hub
   id=508  level=255 0x4=USB mod=1970/01/01 9:00 description=com.apple.usb.externaldevice.14410000 owner=ScanSnap S1500
   id=509  level=255 0x4=USB mod=1970/01/01 9:00 description=com.apple.usb.externaldevice.14420000 owner=USB Charger
   id=510  level=255 0x4=USB mod=1970/01/01 9:00 description=com.apple.usb.externaldevice.14440000 owner=US-1x2
   id=511  level=255 0x4=USB mod=1970/01/01 9:00 description=com.apple.usb.externaldevice.14510000 owner=USB Receiver
   id=512  level=255 0x4=USB mod=1970/01/01 9:00 description=com.apple.usb.externaldevice.14530000 owner=BCM20702A0
   id=513  level=255 0x100=MAGICWAKE mod=1970/01/01 9:00 description=en0 owner=en0
Idle sleep preventers: IODisplayWrangler
```

IO USB周りが問題っぽい気もするのですが、どのように対処すればいいのかも分からなく困っています。  

アドバイスお願いいたします。  

## 構成

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

MacのバージョンとCloverのバージョン  
- macOS Catalina 10.15.7  
- Clover r5127  


### EFIについて

導入はSarkさんが[提供していくれているもの](https://github.com/sarkrui/Z390M-Pro4-i7-9700K-Hackintosh)を参考にして行いました。ESPの中身はEFI/Clover/以下のファイルを上のリンクからコピーして、基本的にそのまま使っています。  

使用しているdriver/UEFI/*.efiは
- apfs.efi
- ApfsDriverLoader.efi
- FSInject.efi
- HFSPlus.efi 
- OpenRuntime.efi
- OsxAptioFix3Drv.efi  
です。

手を加えた内容は以下の通りです。

- WhatEverGreen.kext  
  	起動時に画面が乱れることがあったので追加しました。
- USBPorts.kext  
  	Hackintoolsで作成し直しました。
- SSDT.aml  
  	CPUのパワーマネジメント用にssdtPRGen.shを使って作成しました。
- config.plist  
  	最初のUSBから起動する際に使用したconfig.plistを、Sarkさんのconfig.plistに近づけるように編集して行っています。

