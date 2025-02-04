# Rooftops&Alleys - Color Picker
Quick guide on getting custom clothing mods to work with the game's customization color picker.

The goal is to have the same first few materials, referencing the original materials, and having the material slots matching the original names.

> [!IMPORTANT]  
> Different clothing items will have different set of materials and material slot names - make sure you double check with the item you're replacing.

## Material Order
The order of the material list is important, and has to match up with the original one (at least for the first few ones).

When modeling the mesh in Blender, ensure the first few materials match up with the material "purpose" of each one.

Meaning if the first material is used for the primary color - ensure you assign that material to sections of your mesh that would change colors in-game.

If the skeletal mesh has a "skin" material, make sure it's assigned to the relevant parts of the mesh.

The rest of the material stack doesn't matter, can be your custom ones...

### Example - Tshirt SK
The default tshirt SK has 2 materials: `MI-cloth-Upper` and `MI-skin-colour`.

Only the mesh sections that are assigned to material id 0 (MI-cloth-Upper), will be able to change colors in-game.

### Example - StrappedPants SK
Different models will have different stack of materials, and the "StrappedPants" has 3, `MI-lower-primary`, `MI-lower-secondary`, and `MI-skin-colour`.

## The Setup
Once you have the SK imported, look at the SK/SM in FModel and how the materials are structured.

1. Ensure the first few materials match up with the original materials visible in FModel (any additional materials don't matter)
2. Place the materials in the same folder structure as shown in FModel _(highlighted)_. 
3. Each material has its own material slot, name it the same as shown in Fmodel _(highlighted)_.
4. If you don't have those materials dummied/replicated - the next section will explain it.

![](/GameSpecific/RNA/media/colorpicker/1.png)

<hr>

## Material Dummying
Asset dummying is the process of creating an empty object of the same type, placing it in the same folder structure as in game files and the same file name.

> [!TIP]
> If you don't have the base customization materials in your UE project, I would highly suggest creating them so when you make more mods - they will be auto-assigned on import.

The customization related materials are located in:<br>
`MainFolder/Content/Materials/customization/materials/`

1. Create the same folder structure in your project.
2. Create any nested folders that your mod needs. <br>
_The image below shows all of the folders for all types of clothing types._

If it's a tshirt, then you only need `UpperBody` and `Skin`.

![](/GameSpecific/RNA/media/colorpicker/3.png)

3. Create materials with the same names as shown in FModel.
4. They can stay empty, we don't care about the content, only the fact that they will be referenced in the Skeletal/Static Mesh.

![](/GameSpecific/RNA/media/colorpicker/2.png)



## Packaging
Before you package, double check all:
- The materials are named exactly as in FModel.
- The materials are placed in the same folder structure as in FModel.
- The material slots are named exactly to match the SK/SM.
- The dummy materials are not being included in the pak chunk of the mod.

![](/GameSpecific/RNA/media/colorpicker/1.png)
