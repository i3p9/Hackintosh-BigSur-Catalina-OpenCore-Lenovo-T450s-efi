# Utilities for T450s

This is where I'll store useful but optional hacks for the laptop

## alc_fix
This is a fix for Headphone jack not working after sleep. To install this, cd into the repository, then:

- `sudo spctl --master-disable`
- `cd alc_fix`
- `./install.sh`

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