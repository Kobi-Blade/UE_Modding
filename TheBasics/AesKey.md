# Finding AES Key
Some games will have their `.pak` files encrypted with an AES key. </br>
Luckily, it's an easy task to find the AES key.

There are two methods:
- Method 1: using [AESDumpster](https://github.com/GHFear/AESDumpster) by [GHFear](https://github.com/GHFear/)
- Method 2: using the Java version Aes_Finder (backup if first doesn't work).

## Getting the AES - Method 1
1. Navigate to [AESDumpster](https://github.com/GHFear/AESDumpster).
2. Download executable from releases.
3. Drop your game's largest executable (usually called "Gamename"-Shipping.exe) on top of AESDumpster-Win64.exe
4. Within a few seconds, it will output the found AES key on the screen.

## Getting the AES - Method 2
1. Download the [AES_Finder.exe](https://github.com/Dmgvol/UE_Modding/raw/main/Tools/AES_finder.exe).<br>
_(the tool is using Java, and requires Java Runtime to be installed)_
2. Place the `.exe` in the same folder as the game binary executable.<br>
_(the one with "Win64-Shipping.exe" in its name)_<br>
(For example: `...\Ghostrunner 2\Ghostrunner2\Binaries\Win64\`)
3. Launch the game and then launch the AES finder.
4. Wait a few seconds, and a new text file named `key.txt` will appear in that folder, which will contain the AES key.

That's it!
