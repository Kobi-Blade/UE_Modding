# Extracting IoStore Cooked Assets
> [!IMPORTANT]
> This only guide applies when there are `.ucas`, `.utoc` & `.pak` files inside `Content/Paks` folder.

> [!CAUTION]
> [FModel](UsingFModel.md) can open `IoStore` containers/paks, and can even let you export them. However, these assets are in a format that only allows them to be read-only. This means that these assets cannot be edited in a valid way for modding (e.g. with [UAssetGUI](../BasicModding/UAssetGUI.md)), nor can they be repackaged.

## ZenTools

ZenTools is a tool that extracts the traditional cooked assets (`.uasset`/`.uexp`) from the `IoStore` container files, which are `.ucas`, `.utoc` & `.pak`. Because some tools out there only support the traditional cooked asset format, such as [UAssetGUI](../BasicModding/UAssetGUI.md), you need to get the right format of assets first.

There are two versions of ZenTools that you need to get depending on your game's UE version; 
- [ZenTools for UE5](https://github.com/LongerWarrior/ZenTools/tree/5.1-5.2) (if your game is UE5)
- [ZenTools for UE4](https://github.com/WistfulHopes/ZenTools-UE4) (obviously if your game is UE4)

### ZenTools for UE5

Go to the [release page](https://github.com/LongerWarrior/ZenTools/releases) and download the latest release. This can just be the `ZenTools.exe` file, but you may also want to download the `.pdb` file alongside it in-case you have errors and want to post the tool output (this is useful for the maintianer).

> [!WARNING]
> Do not run `ZenTools.exe` by clicking on it, it is not meant to be used this way. You would see a window popup then dissapear. This is a tool that is meant to be run from the command line.

Navigate to your modding directory of choice. Then open a command prompt shell. You can do that easily by either right clicking anywhere on the file explorer and clicking "Open in Terminal/command prompt", or by clicking on the file path bar (`folder > folder > folder`), typing `cmd` and hitting enter.

Simply follow the [usage guide](https://github.com/LongerWarrior/ZenTools/tree/5.1-5.2?tab=readme-ov-file#usage) in the project's README on GitHub and enter your command into cmd.

> [!IMPORTANT]
> If your game is UE5.1, make sure to include the `-ZenPackageVersion=Initial` option in your command.
> If your game has an AES key (i.e. is encrypted), you can find it in the [Adding AES](AesKey.md) guide, then use the `-AES=` option in your command.

> [!TIP]
> Make sure to use quotation marks `""` whenever you are specifying file paths if they contain any spaces.

#### Example commands

If your game is UE5.1: 

`ZenTools.exe ExtractPackages "Path to UE5.1 game/Content/Paks" "Output directory" -ZenPackageVersion=Initial`

If your game is UE5.1 and has encryption:

`ZenTools.exe ExtractPackages "Path to UE5.1 game/Content/Paks" "Output directory" -ZenPackageVersion=Initial -AES=0x12345678`

If your game is UE5.2 amd has encryption:

`ZenTools.exe ExtractPackages "Path to UE5.2 game/Content/Paks" "Output directory" -AES=0x12345678`

#### Repacking UE5 IoStore files

Follow this guide

### ZenTools for UE4

Install ZenTools UE4 in the same way as ZenTools UE5 - [download link](https://github.com/WistfulHopes/ZenTools-UE4/releases).

If your game is encrypted, note that there is no `-Aes=` or equivalent option, you must supply a `keys.json` file. This is simply a file that is:
```json
{
    "00000000-0000-0000-0000-000000000000": "DEADBEEFCAFEDEADBEEFCAFEDEADBEEFCAFEDEADBEEFCAFEDEADBEEFCAFEDEAD"
}
```

> [!WARNING]
> The keys.json does not support `0x` at the start of your AES key, so make sure to remove that in the file.

#### Example commands

If game has encryption:

`ZenTools.exe ExtractPackages "Path to UE4 game/Content/Paks" "Output directory" -EncryptionKeys="Path to keys.json"`

If game has no encryption:

`ZenTools.exe ExtractPackages "Path to UE4 game/Content/Paks" "Output directory"`

#### Repacking UE4 IoStore files

Follow this guide