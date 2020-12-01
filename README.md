# [SUCCESS] ASRock Z390M-PRO4, i5-9400F, MSI RX570
### Introduction
第９世代デスクトップCPU i5-9400Fを搭載したASRockのZ390マザーボードに、Cloverで動作するCatalinaをインストールしました。CPU, GPU, シャットダウン, スリープ, Ethernet, サウンド全てが動き安定しています。Wi-Fiのカードを持っていないのでCommunityが使えません。Airdrop, AppleWatchでのロック解除が使えないので成功率的には95％でしょうか。


## Spec
- CPU: Intel Core i5-9400F (Base 2,6GHz Turbo 4.1GHz, SMBIOS iMac19,1)
- MB: ASRock Z390M Pro4 (M.2 Key B * 2 + M.2 Key A+E * 1 + PCIe 3.0 x16 * 2)
- Clover Bootloader(r5127)
- Graphics Card: MSI Radeon RX570 ARMOR 4G OC
- Strage: SSD 480GB ADATA SU630
- RAM: 24GB (Patriot Memory  DDR4 2666Mhz PC4-21300 4GBx2, TEAM DDR4 2400MHz PC4-19200 8GBx2)
- Bluetooth: USB Adapter I-O DATA USB-BT40LE (Broadcom BCM20702) 

## Build Guide
Step by Step

### Step.1

BIOS Setting
- BIOS version P4.30
- VT-d --> Disabled
- Onboard WAN Device --> Disabled
- Serial Port --> Disabled
- XHCI Hand-off --> Enabled
- CSM(Compatibility Support Module) --> Disabled  
(i5-9400F doesn't have iGPU. If you use other CPU(which has iGPU), you may turn on "IGPU Multi-Monitor")



My installation is refarence for this EFI, Especcialy USB setting 
導入はSarkさんが[提供していくれているもの](https://github.com/sarkrui/Z390M-Pro4-i7-9700K-Hackintosh)を参考にして行いました。ESPの中身はEFI/Clover/以下のファイルを上のリンクからコピーして、基本的にそのまま使っています。  

driver/UEFI/*.efi
- apfs.efi
- ApfsDriverLoader.efi
- FSInject.efi
- HFSPlus.efi 
- OpenRuntime.efi
- OsxAptioFix3Drv.efi  
です。


