# Extracting IoStore Cooked Assets
> [!IMPORTANT]
> This guide only applies when there are `.ucas`, `.utoc` & `.pak` files inside `Content/Paks` folder.

> [!CAUTION]
> [FModel](UsingFModel.md) can open `IoStore` containers/paks, and can even let you export them. However, these assets are incompatible with [UAssetGUI](../BasicModding/UAssetGUI.md), but can be edited by manual [hex editing](../BasicModding/HexEditing.md). 

Because some tools out there only support the traditional cooked asset format, such as [UAssetGUI](../BasicModding/UAssetGUI.md), you need to get the right format of assets first.

The following tools, retoc and Zentools, can be used to extract the traditional cooked assets (`.uasset`/`.uexp`) from the `IoStore` container files, which are `.ucas`, `.utoc` & `.pak`.

> [!TIP]
> It is recommended to try using retoc first as it is generally faster and more reliable. If you encounter any issues, you can try using ZenTools as a backup.

## retoc

[retoc](https://github.com/trumank/retoc) is not only able to pack and unpack `IoStore` containers, but also convert between Zen assets and Legacy assets (found in `.pak` containers).

To use retoc, you need to download the latest release from the [releases page](https://github.com/trumank/retoc/releases). Download the file you need based on your system or use the powershell script provided at the top if you are on Windows.

Navigate to the directory where you downloaded `retoc.exe` and open the terminal. 

Run `retoc.exe --help` to see the available commands and options. 

`to-legacy` is used to convert from the `IoStore` format to the cooked asset format you can edit with UAssetGUI.

> [!TIP]
> It is recommended to use `--filter` to specify which assets you want to convert, especially if you are working with large games.
> <br>For example: `--filter "/Content/MainFolder/saving-loading/customization/progress"` will only convert assets inside the `progress` folder.

Use `--aes-key` to specify the AES key if your game is encrypted. You can find the AES key in the [Adding AES](AesKey.md) guide.

Here is an awesome video guide on using retoc as a command line tool:

[![UE modding (5.4 w/ IoStore): retoc + UAssetGUI](https://img.youtube.com/vi/2nkhdAREFXI/0.jpg)](https://www.youtube.com/embed/2nkhdAREFXI "UE modding (5.4 w/ IoStore): retoc + UAssetGUI")

## ZenTools

There are two versions of ZenTools that you need to get depending on your game's UE version; 
- [ZenTools for UE5](https://github.com/Buckminsterfullerene02/UE-Modding-Tools/tree/main/Loose%20Files/ZenTools) (if your game is UE5.1 - UE5.4)
- [ZenTools for UE4](https://github.com/WistfulHopes/ZenTools-UE4) (if your game is UE4)

### ZenTools for UE5

Go to the [release page](https://github.com/LongerWarrior/ZenTools/releases) and download the latest release. This can just be the `ZenTools.exe` file, but you may also want to download the `.pdb` file alongside it in-case you have errors and want to post the tool output (this is useful for the maintianer).

> [!WARNING]
> Do not run `ZenTools.exe` by clicking on it, it is not meant to be used this way. You would see a window popup then dissapear. This is a tool that is meant to be run from the command line.

Navigate to your modding directory of choice. Then open a command prompt shell. You can do that easily by either right clicking anywhere on the file explorer and clicking "Open in Terminal/command prompt", or by clicking on the file path bar (`folder > folder > folder`), typing `cmd` and hitting enter.

Simply follow the [usage guide](https://github.com/LongerWarrior/ZenTools/tree/5.1-5.2?tab=readme-ov-file#usage) in the project's README on GitHub and enter your command into cmd.

> [!IMPORTANT]
> If your game is UE5.1, make sure to include the `-ZenPackageVersion=Initial` option in your command.
> If your game has an AES key (i.e. is encrypted), you can find it in the [Adding AES](AesKey.md) guide, then use the `-AES=` option in your command.

> [!CAUTION]
> Make sure to use quotation marks `""` whenever you are specifying file paths if they contain any spaces.

> [!TIP]
> If it is taking a long time to extract, try using package filters to filter certain folders, for example `/Game/Content/Blueprints`. You can find project folders by opening the pak in FModel

#### Example commands

If your game is UE5.1: 

`ZenTools.exe ExtractPackages "Path to UE5.1 game/Content/Paks" "Output directory" -ZenPackageVersion=Initial`

If your game is UE5.1 and has encryption:

`ZenTools.exe ExtractPackages "Path to UE5.1 game/Content/Paks" "Output directory" -ZenPackageVersion=Initial -AES=0x12345678`

If your game is UE5.2 and has encryption:

`ZenTools.exe ExtractPackages "Path to UE5.2 game/Content/Paks" "Output directory" -AES=0x12345678`

If your game is very large (e.g. 100GB+) and you want to only extract certain asset paths, say, weapon blueprints folder:

`ZenTools.exe ExtractPackages "Path to game/Content/Paks" "Output directory" -PackageFilter=/Game/Content/Blueprints/Weapons`

#### Repacking UE5 IoStore files

Follow [this guide](../BasicModding/IoStorePacking.md#scenario-1-packing-cooked-assets).

### ZenTools for UE4

Install ZenTools UE4 in the same way as ZenTools UE5 - [download link](https://github.com/WistfulHopes/ZenTools-UE4/releases).

If your game is encrypted, note that there is no `-Aes=` or equivalent option, you must supply a `keys.json` file. This is simply a file that is:
```json
{
    "00000000-0000-0000-0000-000000000000": "DEADBEEFCAFEDEADBEEFCAFEDEADBEEFCAFEDEADBEEFCAFEDEADBEEFCAFEDEAD"
}
```

> [!CAUTION]
> The keys.json does not support `0x` at the start of your AES key, so make sure to remove that in the file.

> [!CAUTION]
> Make sure to use quotation marks `""` whenever you are specifying file paths if they contain any spaces.

> [!TIP]
> If it is taking a long time to extract, try using package filters to filter certain folders, for example `/Game/Content/Blueprints`. You can find project folders by opening the pak in FModel

#### Example commands

If game has encryption:

`ZenTools.exe ExtractPackages "Path to UE4 game/Content/Paks" "Output directory" -EncryptionKeys="Path to keys.json"`

If game has no encryption:

`ZenTools.exe ExtractPackages "Path to UE4 game/Content/Paks" "Output directory"`

If your game is very large (e.g. 100GB+) and you want to only extract certain asset paths, say, enemy blueprints folder:

`ZenTools.exe ExtractPackages "Path to game/Content/Paks" "Output directory" -PackageFilter=/Game/Content/Blueprints/Enemies`

#### Repacking UE4 IoStore files

Follow [this guide](../BasicModding/IoStorePacking.md#scenario-1-packing-cooked-assets).
