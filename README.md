# MinecraftAppleSiliconShim
Run the ARM64 version of Minecraft through the stock launcher

## Quick Install
Make sure you have an ARM64 version of Java installed first! You can download the Azul Zulu JDK [here](https://www.azul.com/downloads/?os=macos&architecture=arm-64-bit&package=jdk) (DMG is easiest!).

Run `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/lotuspar/MinecraftAppleSiliconShim/main/quick.sh)"` in the Terminal. Alternatively, download quick.sh yourself, make it executable and run it.\
\
If you don't want to use the quick installer (or it doesn't work) follow the steps starting from Requirements.\
\
After the quick installer is done, [change the Java executable](https://github.com/lotuspar/MinecraftAppleSiliconShim/raw/main/images/what's%20a%20java%20executable%3F%3F%3F.png) for a launcher profile to the shim (probably stored in your user folder)

## Requirements
To use this you need an [ARM64 / AArch64 version of Java](https://www.azul.com/downloads/?package=jdk#download-openjdk) and the ARM64 LWJGL natives & fat binary. You can get this from [m1-multimc-hack](https://github.com/yusefnapora/m1-multimc-hack).\
These need to be in a folder called "shim" in the Minecraft data directory (~/Library/Application Support/minecraft)\
\
The end result should be 2 paths existing like this:\
`~/Library/Application Support/minecraft/shim/lwjglnatives/` (filled with .dylib files)\
`~/Library/Application Support/minecraft/shim/lwjglfat.jar` (one file)\
\
After the files are there, remove the quarantine flag from the dylibs by executing `xattr -r -d com.apple.quarantine ~/Library/Application Support/minecraft/shim/lwjglnatives/*.dylib` in the Terminal.

## Usage
After getting the requirements just set the Java executable in your Minecraft profile to the shim!

## Quirks and fixes
### Troubleshooting
Bugs in the shim won't be visible in the Minecraft launcher. To see them look at "m1shimlog.txt" in the Minecraft data directory.

### Minecraft errors
If you get the error `Could not initialize class ca.weblite.objc.RuntimeUtils` turn off Fullscreen in the game options. If you can't get to the options, go to the game directory and change `fullscreen: true` to `fullscreen: false` in "options.txt"

### Java version changing
By default the shim will use the first Java found in the path (the one used when running `java` in the Terminal)\
To change the Java version running the game, pass `-javahome (path to java home directory)` to the game arguments. You can do this right below where you set the profile Java executable.\
To find Java home directories on your system, run `/usr/libexec/java_home -V` in the Terminal.

## Credits
This is definitely not a full list, but thanks to:\
[yusefnapora](https://github.com/yusefnapora) for making [m1-multimc-hack](https://github.com/yusefnapora/m1-multimc-hack)! This was the main starting point for MinecraftAppleSiliconShim!\
[tanmayb123](https://github.com/tanmayb123) for some of the biggest work getting Minecraft running natively on M1 machines with [AppleSiliconMinecraft.md](https://gist.github.com/tanmayb123/d55b16c493326945385e815453de411a)!
