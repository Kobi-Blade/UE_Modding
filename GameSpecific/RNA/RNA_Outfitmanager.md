# Rooftops&Alleys - OutfitManager

Quick guide on converting traditional modded SK clothing items to work with the OutfitManager mod.

> [!IMPORTANT]  
> This guide assumes you've already have a skeletal mesh that works with the default method of overwriting existing items.


## Folder Structure
1. Create the following folder structure in your UE5.4 editor.
2. Create a folder named `CustomOutfits`.
3. Inside that folder, create the following folders: `Backpack`, `Head`, `Headphones`, `Lowerbody`, `Shoes`,`Upperbody`.

![](/GameSpecific/RNA/media/outfitmanager/1.png)

## Mod Folder
1. Create a folder with the name of your mod in the correct clothing item type. <br>

For this example, I will be adding a tshirt with a custom red pattern, named `Red` (mod name should stay consistent).

![](/GameSpecific/RNA/media/outfitmanager/2.png)

2. Once the mod folder is created, drag your  mesh into the mod folder.

![](/GameSpecific/RNA/media/outfitmanager/3.png)

3. Import a 2D texture to be used as an icon for your mod.

4. Name the icon texture as `T_<ModName>_Icon`, in my case it's `T_Red_Icon` as the mod name is `Red`.

5. Name the mesh accordingly.<br>
If it's a skeletal mesh -> name it `SK_<ModName>`, for example `SK_Red`.<br>
If it's a static mesh -> name it `SM_<ModName>` for example `SM_Red`.

> [!IMPORTANT]  
> Skeletal meshes are: Shoes, Lowerbody, Upperbody, and Head.<br>
> Static meshes are: Headphones and Backpacks.

6. It doesn't matter how you name the textures and materials, just make sure you package the needed assets.

![](/GameSpecific/RNA/media/outfitmanager/4.png)

## Packaging
There are two types of packaging; the manual chunk assigning and via a primary asset label (which is shown below).

1. Create a Primary Asset Label by right-clicking in the folder -> Miscellaneous -> Data Asset -> Primary Asset Label.

2. Name it `PAL_<Modname>`, in this case it will be `PAL_Red`.

3. Open the Label and adjust the following settings:

- Adjust the priority to `1`.
- Give a random Chunk ID number (between 300 and 9999).
- Change the Cook Rule to `Always Cook`.
- Click `+` on the `Explicit Asset` and add all the items you need to be packaged.

![](/GameSpecific/RNA/media/outfitmanager/5.png)

> [!IMPORTANT]  
> If the Label is located inside the folder where all the items are needed to be packaged - you can simply tick the `Label Assets  in My Directory` instead of manually adding them.

4. Package the mod, move the files to Paks folder, name it accoringly and launch the game.

## In-Game
1. Ensure you have Outfitmanager enabled by clicking DML in main menu, Blueprint Mods, and typing `outfitmanager`.<br>
And then reload main menu (enter any level and go back to menu).

2. When you click on DML, a third option will be available, named "Outfit Manager".

3. Enter the mod name, the clothing type, and click `Add`.

![](/GameSpecific/RNA/media/outfitmanager/6.png)

If everything was done correctly, it should show a success message and your clothing item should appear as a new item in the customization panel under the correct clothing type.

![](/GameSpecific/RNA/media/outfitmanager/7.png)

<br>

<hr>

## Examples

> [!NOTE]  
> Pay attention to the type of the clothing type and if it's a SkeletalMesh (SK) or a StaticMesh (SM), and how you name the assets.

### SK Example
Example of another SK mod (Lowerbody type): 

![](/GameSpecific/RNA/media/outfitmanager/example1.png)

The mod name is `CamoWoodland` and the important assets are the skeletal mesh named `SK_CamoWoodland` and the 2D texture used for the icon preview, named `T_CamoWoodland_Icon`.


### SM Example
An example of a static mesh mod (Backpack):

![](/GameSpecific/RNA/media/outfitmanager/example2.png)

The Modname is `Jetpack` of type Backpack which is a static mesh, so the mesh is named `SM_Jetpack` and the icon preview is named `T_Jetpack_Icon`.