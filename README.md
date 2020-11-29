## Notice: Updated to OC 0.6.3 and kexts. Big Sur Update is currently working out of the box. Tested it myself. 
## This is an update for Echo's repo. OC has been updated to 0.6.3 and all the kexts are updated to the lastet version to date. I did make some QOL changes for it. I'll try to keep the repo updated following major OC releases. 
![img](https://img.shields.io/github/last-commit/i3p9/Hackintosh-Catalina-Opencore-Lenovo-T450s-efi.svg?color=green&label=last-commit) ![img](https://img.shields.io/badge/macOS%20support-catalina--bigsur-blue) ![img](https://img.shields.io/badge/Opencore%20version-0.6.3-red) [![Gitter](https://badges.gitter.im/ThinkPad-Hackintosh/t450s.svg)](https://gitter.im/ThinkPad-Hackintosh/t450s?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

Issues (with OC 0.6.3):
* When an external monitor is connected via MiniDP, external mouse gets very laggy to the point it's almost unuseable, investigating the issue now. Please let me know if anyone faces this issue. (Only happens in Big Sur)

Changes I made:
* Using VoodooRMI instead of VoodooPS2Trackpad for Touchpad/Trackpoint. I've found this to be leagues better in terms of smoothness and gestures
* Disabled `SSDT-SMBU` and `SSDT-Thinkpad_Clickpad` patch for VoodooRMI compatibility. Also the clickpad patch didn't work for newer OC versions
* Switched to  Vanilla OC instead of the modified one
* Added OpenCanopy support and Mac-like boot GUI
* Switched to MacBooPro12,1 SMBIOS and tweaked Power Management for better battery life. By switching we lose Wired Sidecar but it was very laggy and often unuseable, but we gained much better power management, thus, better battery life. If you want Sidecar, you can switch back to Macbook9,1
* Updated alc_fix for Big Sur

Note: This is a fairly vanilla EFI. If you have Intel WiFi/BT Card, use [OpenIntelWireless](https://github.com/OpenIntelWireless) for WiFi/Bluetooth

Big Sur Screenshot (Currently running Stable 11.0.1:
![About Mac Big Sur](https://i.imgur.com/7PHmsEm.png)

Original Readme from Echo: 
# Thinkpad T450s Catalina

## Notice: If you need to edit config.plist, don't use OpenCore configurator, use PlistEdit pro or Xcode instead.

## Introduction

efi for Thinkpad T450s (20BXCT01WW) Hackintosh Catalina/Big Sur

- CPU: i5-5200U
- Integrated Graphics: HD Graphics 5500
- Sound Card: ALC292
- Wireless Card: **DW1820A 00JT494** 

## Bios

- `Security -> Security Chip`: **Disabled**;
- `Memory Protection -> Execution Prevention`: **Enabled**;
- `Virtualization -> Intel Virtualization Technology`: **Enabled**;
- `Internal Device Access -> Bottom Cover Tamper Detection`: must be **Disabled**;
- `Anti-Theft -> Current Setting`: **Disabled**;
- `Anti-Theft -> Computrace -> Current Setting`: **Disabled**;
- `Secure Boot -> Secure Boot`: **Disabled**;
- `UEFI/Legacy Boot`: **UEFI Only**;
- `CSM Support`: **Yes**.

## What works

- Sleep / Wake
- Wifi and Bluetooth (DW1820A)
- Handoff, Continuity, AirDrop
- iMessage, FaceTime, App Store, iTunes Store (Change Config.plist -> PlatformInfo -> Generic -> MLB and SystemSerialNumber)
- Ethernet
- Onboard audio (Use alc_fix to fix unworking jack after replug )
- USB 2.0 / USB 3.0
- Battery
- Touchpad
- Redpoint
- miniDP
- Use [one-key-hidpi](https://github.com/daliansky/XiaoMi-Pro-Hackintosh/blob/master/one-key-hidpi) to enable HiDPI
- If you are using a usb mouse with side buttons, you can spoof apple usb mouse by change the pid and vid in AnyAppleUSBMouse.kext/Info.plist and enable it in config.plist.

## What doesn't work

- VGA
- Sidecar (Wired Sidecar works but only in Macbook9,1 SMBIOS, which has bad battery life, you can choose what you want)
- SD Card Reader (RTS5227) (kext is not reliable)
