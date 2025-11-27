# Editing IoStore Assets using `retoc`
This guide goes through all the steps needed to create your first asset edit mod for a game that uses IoStore.

For this example, I will be modding [The Last Caretaker](https://store.steampowered.com/app/1783560/The_Last_Caretaker/) which runs on a native UE5.6 with IoStore enabled, and will be editing a simple value within one of the DataTable (DA) assets.

> [!TIP]
> IoStore? If you have `.utoc` and `.ucas` file extensions in your game's Pak folder, then it uses IoStore.

### The tools we need:
- [FModel](https://fmodel.app/): For browsing and locating the asset you want to modify.
- [Retoc](https://github.com/trumank/retoc) by [trumank](https://github.com/trumank): For extracting and repackaging the assets.
- [UAssetGUI](https://github.com/atenfyr/UAssetGUI) by [atenfyr](https://github.com/atenfyr/): For editing the extracted assets.

> [!CAUTION]
> Assumes you already have the game's mapping file, know the game's UE version, and AES key (if any).

## Searching for the file with FModel
Open the game files using FModel and find an asset that you're interested in editing its value(s).

> [!NOTE]
> If you don't know how to setup FModel, make sure to read the [FModel Guide](./TheBasics/ExportingFModel.md) on how to configure it.

![](/Media/EditingWithRetoc/retocEdit1.png)

For this example, I'm interested in editing the `InventoryWeightCapacityIncrease` default variable value within the `DA_Enhancer_Character_HaulMastery` file.

## Extracting with retoc
The tool `retoc` is used exclusively through CMD, so start by opening the cmd.

> [!NOTE]
> On Windows, you can open it by pressing "Windows + R" on your keyboard, type "cmd" and press Enter.

1. First, set the current path to the folder where retoc is located using `cd`.<br> 
For example, I've placed the `retoc.exe` in `C:\UE Modding\Tools\retoc` so I would execute `cd "C:\UE Modding\Tools\retoc"`.
2. The full command for extracting a specific asset is:<br>
`retoc to-legacy --no-shaders <Paks_Folder> --filter <Asset_Path> --version <version> <output_folder>`.

### Explanation

- `<Paks_Folder>`: The full path to the game's Paks folder, for example:<br>
`E:\SteamLibrary\steamapps\common\TheLastCaretakerDemo\Voyage\Content\Paks`.
- `<Asset_Path>`: The full path to the asset that we want to edit, for example:<br>
`Voyage/Content/Data/Assets/Enhancements/DA_Enhancer_Character_HaulMastery.uasset`.
- `<version>`: The UE version of the game, for example: `UE5_6`.
- `<output_folder>`: The folder that retoc will extract the files into.

### Examples
Extracting a single asset: <br>
![](/Media/EditingWithRetoc/retocEdit2.png)

Extracting **all** assets: <br>
![](/Media/EditingWithRetoc/retocEdit3.png)

> [!WARNING]  
> Extracting **all** assets may use a lot of disk space and is unnecessary if you only need to edit a single asset.

## Editing with UAssetGUI
Once you're done extracting, navigate to extracted/target `.uasset` file and open it with UAssetGUI.

1. Make sure you have the correct UE version specified, and provide usmapping file for the game (Utils -> Import mappings).

![](/Media/EditingWithRetoc/retocEdit5.png)

2. If UAssetGUI complains when opening the file, about failing to open a dependency asset as shown below, simply repeat the retoc process with a `--filter` tag followed by the given asset(s), and reopen the file.

![](/Media/EditingWithRetoc/retocEdit4.png)

3. This part will be different with each asset, so you will have to find the variable you need, for this example it's located here which I will change its value.

![](/Media/EditingWithRetoc/retocEdit6.png)

Once done, simply save your changes and close UAssetGUI.

## Preparing for packaging
Before packaging, make sure you remove:
1. Any files created by UAssetGUI that end with `.bak` extension.
2. Any dependency assets that you may have extracted previously.<br>Meaning **only** the files you've modified should stay, with `.uasset` and `.uexp` for each one.

![](/Media/EditingWithRetoc/retocEdit7.png)

## Repackaging with retoc
The last step is to repackage the mod folder using retoc into `.pak`, `.utoc`, and `.ucas`.

The command: `retoc to-zen <Folder_name> <Folder_name>.utoc --version <version>`

For example: <br>
![](/Media/EditingWithRetoc/retocEdit8.png)


And you're done! Now copy the 3 newly created files into game's Paks folder and test your new mod.

---

The mod that this guide is based on, is available here: <br>
[https://www.nexusmods.com/thelastcaretaker/mods/6](https://www.nexusmods.com/thelastcaretaker/mods/6) 

