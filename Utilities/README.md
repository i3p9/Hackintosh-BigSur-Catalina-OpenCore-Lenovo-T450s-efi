# Utilities for T450s

This is where I'll store useful but optional hacks for the laptop

## alc_fix_swift
This folder contains instructions to install the new swift version of alc_fix which doesn't rely on `hda-verb`, `alc-verb` or `CodecCommander` kext. The installation process is in the folder. 

## alc_fix_legacy
This folder contains the old method of alc_fix.


## DW1820A
This folder contains instructions and kexts needed to run DW1820A which enables native WiFi/Bluetooth as well as Airdrop, Instant Hotspot, Hand-off and Continuity. 

## Color Profile

This will download and put the color profile calibrated using Spyder Pro on the TN Panel

```bash
cd /Library/ColorSync/Profiles/Displays/
```

```bash
sudo wget https://github.com/i3p9/Hackintosh-Catalina-OpenCore-Lenovo-T450s-efi/blob/master/Utilities/T450s_Color_Spyder_TNPanel.icm
```

This will ask for admin password beacuse we're modifiying System. Put the password and then change the profile from `System Preferences -> Display -> Color`