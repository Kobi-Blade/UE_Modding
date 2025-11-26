# Translation Mods  
This guide covers the steps of translating the game's default language (`.locres`) into any other language. 

> [!NOTE]  
> This guide assumes you're familiar with FModel (exporting) and UnrealPak/repak (for packaging).


> [!IMPORTANT]  
> If your game is UE5.6 & IoStore - you **must** follow the [UE5.6 Changes](#ue56-version--iostore) after you've made the mod, in order for your translation mod to be recognized by the game.

## Preparation
For this example, I will be translating a game called [Trepang2](https://store.steampowered.com/app/1164940/Trepang2/) from English to Polish using AI.


### Locres Editor

Before we begin, we will be using this `.locres` editor:<br>
[UnrealLocresEditor](https://github.com/Snoozeds/UnrealLocresEditor) by [Snoozeds](https://github.com/Snoozeds).

Download the [release version](https://github.com/Snoozeds/UnrealLocresEditor/releases) and extract the zip file (doesn't matter where).

### Locres File
Using [FModel](https://fmodel.app/), locate the `.locres` file you want to translate and export as raw data as shown below.

![](/Media/locres/locres1.png)

> [!TIP]  
> Localization files are usually located in `/Content/Localization/...` and always inside `.pak` regardless of whether the game is IoStore or not.

## Locres to CSV
- Open `UnrealLocresEditor.Desktop.exe`
- File -> Open locres
- Select the exported `.locres` file and click Load

![](/Media/locres/locres2.png)

If everything is correct, the localization file will be fully loaded into the editor as shown below.

![](/Media/locres/locres3.png)

Next, export it into a `.csv` file by File -> Save As...

Then, open it with Excel.

## Translating
The `.csv` contains 3 columns:
- `key`: the unique identifier (**don't change**).
- `source`: the source text (English).
- `target`: the translated text.

> [!IMPORTANT]  
> If you know the language you're translating to - you can skip this part and translate at your own pace within the Excel sheet.<br>
> Once you're done, continue from [Creating new locres](#creating-new-locres).

For this example, I will be translating a game called [Trepang2](https://store.steampowered.com/app/1164940/Trepang2/) from English to Polish using AI.

> [!NOTE]  
> Alternatively, you can use [DeepL](https://www.deepl.com/) or other methods, but this is just an example! <br>
> You can use AI for bulk translation and then manually double-check.

### Using AI for translating
As an example, you can bulk translate large amounts of localization files using AI, which both **ClaudeAI** and **OpenAI** are _great_ for these tasks.

![](/Media/locres/locres4.png)

Once translated, simply copy the results into the `.csv` and save.

![](/Media/locres/locres5.png)

## Creating new `.locres`
Once translated, we can create an updated `.locres` file using the locres editor.

- Open the LocresEditor
- Load the **default** locres by going to File -> Open locres.
- Open the translated spreadsheet by going to File -> Open Spreadsheet.

If everything was done correctly, you should see the original text and the translated text.

![](/Media/locres/locres6.png)

Next, export the locres:
- File -> Export locres

## Packaging
Create the mod folder to match the game's original folder structure.

For example, the localization used for this example was located in:<br>
`/Content/Localization/UI_Menus/en`

Meaning the mod folder should follow this structure:<br>
`/<MOD_NAME>_P/<GAME>/Content/Localization/UI_Menus/en`

As shown below:

![](/Media/locres/locres7.png)


If you're using unrealpak:
- Drag the mod folder (`<MOD_NAME>_P`) onto the packaging script.
- A new `.pak` file will be created.
- Copy the `.pak` file into the game's Paks folder.

For more information about how to package your mod, view [Cooking Content guide](/IntermediateModding/CookingContent.md).<br>
(don't forget to name your mod with `_P` in its name)

---

## Results
![](/Media/locres/locres8.png)

<br><br><br>

--- 

### UE5.6 version + IoStore
If your game is UE5.6 with IoStore (Paks folder containing `.ucas` and `.utoc`), follow the next steps for the game to recognize your mod:

1. Navigate to Paks folder and duplicate the two `global` files; `global.ucas` and `global.utoc`.
2. Name the newly duplicated files to match your mod file.

![](/Media/locres/UE56_changes.png)