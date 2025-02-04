# Rooftops&Alleys - Cel shaded Material Instance
In the latest update (February 2025), the developer has added a custom material for modders to use in their custom clothing items, that accepts a custom base color texture as one of its parameters while keeping the original cel-shaded style of the game.

### Why should I use it?
If you want to have your clothing mods to look better and fit with the overall RNA style with the cel-shading effect, then you should use this approach. <br>
But if you prefer a plain plastic look like most mods do - then you can skip this one.

![](/GameSpecific/RNA/media/celshading/comparison.png)

## Dummying the Material Instance (MI)
In order to use any material or material instance and the global parameters, we have to create it in the original folder in the editor.

> [!IMPORTANT]  
> Some folders, asset names, and parameters may have been changed throughout the updates, so make sure you double-check with FModel while following the guide, as the guide is for your reference and not for following it blindly.

1. Create the following folder structure in your UE project: <br>
`/MainFolder/Content/Materials/customization/Materials/modding/`

![](/GameSpecific/RNA/media/celshading/1.png)

2. Create a new material called `M-modded-shader`.

![](/GameSpecific/RNA/media/celshading/2.png)

3. Add a new `TextureSampleParameter2D`, call it `Modded Texture`, and connect it to Base Color.

![](/GameSpecific/RNA/media/celshading/3.png)

> [!NOTE]  
> The single texture param is enough to get it working, but I'm showing the proper way to fully dummy it and utilize all of its parameters, like wind intensity, tint, brightness.

4. Looking at the material structure in FModel, we can see there are a handful of useful parameters.<br>
Create a new global parameter and name it as the first one.

The default value of each is located under ` "ScalarValues": [` section in Fmodel, in a corresponding order.<br>
So for the first one, the default value is `0.55`.

![](/GameSpecific/RNA/media/celshading/4.png)

5. Repeat the process until you have all of them.

> [!IMPORTANT]  
> You can pick just the parameters you like/need, I've chosen to have all of them for more control, but you don't have to have all of them.

If you're lazy to create each one, here's a 
[copy-paste material nodes](https://blueprintue.com/blueprint/l-t3xq3o/) to directly paste it into the material graph.

![](/GameSpecific/RNA/media/celshading/5.png)

6. The next step is to connect all of them, and an easy way to do it is by connecting all with a Multiply node.

> [!NOTE]  
> It doesn't matter how you connect the nodes, as long as all parameters make their way to the material shader, it will work.

![](/GameSpecific/RNA/media/celshading/6.png)

6. Change the following settings in the material settings:
- Shading Model to `Unlit`.
- Two Sided to `True`.
- Used with Skeletal Mesh to `True`.

![](/GameSpecific/RNA/media/celshading/7.png)

The final version should look like this:

![](/GameSpecific/RNA/media/celshading/8.png)


## Using the new MI

1. Create a Material Instance (MI) from that material we just created.

![](/GameSpecific/RNA/media/celshading/9.png)

2. Name it `MI-modded-shader`.

3. Create a new MI from `MI-modded-shader`, and drag that MI into your mod folder (or where you will be using it).

4. Open it and adjust any parameters to suit your mod needs.

For example, for a custom tshirt I've modified the used texture and the overall brightness.

![](/GameSpecific/RNA/media/celshading/10.png)

Here's another example, for lowerbody where I've specified `0` for all wind parameters, as by default it will have subtle wind effects which are suitable for cloths and shirts.

![](/GameSpecific/RNA/media/celshading/11.png)

Additional fine tuning for the cel-shading can be done by adjust the different "Bands" and "Tints".
