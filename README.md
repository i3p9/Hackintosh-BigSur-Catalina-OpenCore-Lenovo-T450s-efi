## Notice: Updated to OC 0.6.4 and kexts. EFI currently works in Big Sur and Catalina

![img](https://img.shields.io/github/last-commit/i3p9/Hackintosh-Catalina-Opencore-Lenovo-T450s-efi.svg?color=green&label=last-commit) ![img](https://img.shields.io/badge/macOS%20support-catalina--bigsur-blue) ![img](https://img.shields.io/badge/Opencore%20version-0.6.4-red)

Issues (with OC 0.6.4):
* Opencore 0.6.4 has introduced an issue with BootStrap. Please follow the steps linked [here](https://github.com/acidanthera/bugtracker/issues/1222#issuecomment-739241310). In the config I have set `BootProtect` to `None`, and `RequestBootVarRouting` is already enabled. So all you have to do it boot using `BootProtect` to `None` once, reset nvram and then set `BootProtect` to `Bootstrap`. (This step is unnecessary if you don't want Bootstrap, it is only needed if you run mutiple OS in your computer)

Changes I made:
* Using VoodooRMI instead of VoodooPS2Trackpad for Touchpad/Trackpoint. I've found this to be leagues better in terms of smoothness and gestures
* Disabled `SSDT-SMBU` and `SSDT-Thinkpad_Clickpad` patch for VoodooRMI compatibility. Also the clickpad patch didn't work for newer OC versions
* Switched to  Vanilla OC instead of the modified one
* Added OpenCanopy support and Mac-like boot GUI
* Switched to MacBooPro12,1 SMBIOS and tweaked Power Management for better battery life. By switching we lose Wired Sidecar but it was very laggy and often unuseable, but we gained much better power management, thus, better battery life. If you want Sidecar, you can switch back to Macbook9,1
* Updated alc_fix for Big Sur
* Added `YogaSMC` kext to enable Fan reading. Control is currently not working, will update once it works. 

Since this is a fairly vanilla EFI, if you want to add kexts/patches to it, go ahead, here's some suggestions:  
* If you have Intel WiFi/BT Card, use [OpenIntelWireless](https://github.com/OpenIntelWireless) for WiFi/Bluetooth support. Works well with the 7265AC that comes with T450s, although it has a perticular issue with Bluetooth audio (AAC/aptX). Check this [Issue](https://github.com/OpenIntelWireless/itlwm/issues/85) for more information.
* For better battery life and thermal, use VoltageShift. I have a small guide [here.](#utilities)
* I highly recommend HiDPI, use [one-key-hidpi](https://github.com/mlch911/one-key-hidpi) to enable HiDPI.

# What's working
Everything works except for VGA (macOS doesn't support it), Sidecar (Processor doesn't support it) and SD Card Reader (unreliable kext).

Stuff that works: Proper touchpad with gestures, Function keys, Brightness, Power management, Sleep/wake, Wifi/Bluetooth, Airdrop, Instant Hotspot, Continuity, Import from iphone/ipad, MiniDP etc.

# Utilities
Here I'll have utlities that are necessary or good-to-have for this computer. 

 For alc_fix, DW1820A Config and other, go to the folder [Utilities](https://github.com/i3p9/Hackintosh-BigSur-Catalina-OpenCore-Lenovo-T450s-efi/tree/master/Utilities) to find detailed information on them. 

## VoltageShift
[VoltageShift](https://github.com/sicreative/VoltageShift) is one of the best tool to have lower temp and better battery life. *Note that this is a fairly advance tool and it **can** damage your computer if used without proper research. *
Considering you understand the risk, let's go ahead and set it up:
- The kext needed is already in the EFI, disabled. first we need to enable it. Go to `config.plist` and change `Kernel -> Add -> Item 23 -> Enabled` boolean from `NO` to `YES` (Item 23 is not static, you just have to find the entry where you have VoltageShift.kext)
- Reboot. Then download and copy VoltageShift to `/usr/local/bin`
```bash
wget https://raw.githubusercontent.com/i3p9/Hackintosh-BigSur-Catalina-OpenCore-Lenovo-T450s-efi/master/Utilities/VoltageShift/voltageshift
sudo cp voltageshift /usr/local/bin
```
- Restart terminal and then check if voltageshift is working by `voltageshift info`
- If working, then you can undervolt your CPU by running `voltageshift offset -90` (I don't recommend undervolting below -100mV, just do -90mV first, stress test to see if stable and then test -100mV)
- The undervolt will stick until the next reboot. So I suggest Automator/AppleScript to run it on boot. You can also use AppleScript to undervol/overvolt/switch turbo boost mode depending on what apps you're running/battery percentage etc.  
This was just the basic undervolt guide for CPU only. I highly suggest reading the Readme on the [VoltageShift](https://github.com/sicreative/VoltageShift) repo to learn mode about Undervolting and switching Intel Turbo Boost to on/off.

Big Sur Screenshot (Currently running Stable 11.0.1:
![About Mac Big Sur](https://i.imgur.com/7PHmsEm.png)

<details><summary>Original Readme from Echo</summary>
<p>

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
</p>
</details>