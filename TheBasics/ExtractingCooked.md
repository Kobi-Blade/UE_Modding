# Extracting Cooked Assets
> [!IMPORTANT]
> This only guide applies when there are NOT `.ucas` or `.utoc` files inside `Content/Paks` folder. There may be `.pak`, `.sig` or other files or folders.   

## Repak

For this guide, we will be using [repak](https://github.com/trumank/repak). This tool is widely used as it:
1. Is very easy to download and use
2. Has very good support of all UE4 and UE5 versions
3. Is actively maintained
4. Is faster than alternatives
5. Is cross-platform
6. Has some useful utilities built-in (but we will be using its most basic functionalities)
7. Guards against malicious pak files that attempt to write to parent directories

### Installation

To install repak, simply head to the [releases page](https://github.com/trumank/repak/releases) and download the latest release. For windows users, you can download the `repak_cli-x86_64-pc-windows-msvc.msi` to have it installed into your PATH automatically, which allows you to call the `repak` utility from anywhere in your system.

If you choose the installer (`.msi`) and double click it to install repak, Windows will likely:
1. Ask if you want to run it. Click yes
2. Show a defender popup saying you shouldn't run this file. Click "More" then "Run anyway". This popup shows because the repak installer is not signed, which costs over $100/year

If you don't feel comfortable running the installer on your computer, you can simply download the `.zip` version of repak and then in the below usage commands, you can reference to wherever you have the repak.exe (with absolute/relative paths or by adding it to your `PATH` manually).

### Usage

> [!WARNING]
> Do not run `repak.exe` by clicking on it, it is not meant to be used this way. You would see a window popup then dissapear. This is a tool that is meant to be run from the command line.

Navigate to the directory of the game's pak files. This will be located at `game install path/game name/game project name/Content/Paks/`. Then open a command prompt shell. You can do that easily by either right clicking anywhere on the file explorer and clicking "Open in Terminal/command prompt", or by clicking on the file path bar (where it says `game > Content > Paks`), typing `cmd` and hitting enter.

In your cmd window, type `repak -h`. This should list the help menu for repak. 

> [!CAUTION]
> If you get an error like "command repak not found", you did not install repak correctly. If you opened the cmd before installing repak, you must close and re-open cmd.

To view the unpack command options, simply run `repak unpack -h`.

Unpacking is simple, just follow the help menu.

> [!WARNING]
> If your game has an AES key (i.e. is encrypted), you can find it in the [Adding AES](AesKey.md) guide, then use the `--aes-key` option in your unpack command.

#### Example unpack commands:

`repak unpack MyGameName-WindowsNoEditor.pak`

`repak unpack MyGameName-WindowsNoEditor.pak --output "F:/Modding/Game/Unpacked"`

`repak --aes-key 0x12345678 unpack MyEncryptedGame.pak`

#### Pakchunks

If your game uses pakchunks (many smaller `.pak` files instead of one big one), you have to do a tiny bit more work. Repak can only process one pak at a time, so you can't just have some wildcard to unpak all pak files in a directory.

To unpack them all at once, do the following:
1. Open powershell (by similar way as above, such as typing `pwsh` into file path box)
2. Use your normal command, but instead of specifying your specific `.pak` file, you can type `repak unpack (gci *.pak)`

> [!TIP]
> If you want to output all files into the same folder, specify your output folder with `--output`. Alternately, if you want each pak file to have its own unpacked folder, do not specify the `--output` option.

E.g.

`repak --aes-key 0x12345678 unpack (gci *.pak) --output "F:/Modding/Game/Unpacked"`