### Audio

ALCPlugFIx is required to fix static noise on headphones, however Black-Dragon74 released a Swift version that doesn't require `hda-verb`, `alc-verb` or `CodecCommander` kext. 

**Installation**:

- Open terminal and type following commands one by one on the listed order:
- `sudo spctl --master-disable`
- `sudo mkdir /usr/local/bin/`
- `cd to the ALCPlugFix dictionary`
- `sudo cp -R ALC3232.plist /usr/local/bin/`
- `./install.sh`
- Now the installer will ask you to drop the `ALC3232.plist` into the terminal window.
- Open a new finder window and press `Shift + Cmd(Alt) + G` to open a new `go to folder:` window
- Now type: `/usr/local/bin/`
- Drag the `ALC3232.plist` from the `/usr/local/bin` folder into the terminal window and press enter.
- Done

