---
description: >-
  Step-by-step guide for exporting to Blender for non-mod use (i.e. cosplay, 3d
  print, etc.)
---

# Exporting to Blender

## Summary

**Created by** [Simarilius](http://localhost:5000/u/G2MqNkfgTlQ1R3G4B5s6WefLjdy2 "mention") **&** [dragonzkiller](http://localhost:5000/u/dpriBUirXwWYeCIhyywmqhKrMMV2 "mention")****\
**Published September 03 2022 (updated January 13 2023)**

This guide aims to walk you through finding and exporting a character to blender so that its usable for cosplay or 3d printing or whatever. Guide is using nightly WolvenKit, Cyberpunk add-on for Blender, and Blender 3.2.

#### This guide uses the following versions:

* Cyberpunk 2077 game version 1.61
* Blender 3.2 stable
* Cyberpunk add-on for Blender 1.1.0

### Requirements

* [**WolvenKit nightly release version 8.8.1**](https://github.com/WolvenKit/WolvenKit)
* [**Blender 3.1**](https://www.blender.org/) **or newer**
* ****[**Cyberpunk add-on for Blender 1.1.0**](https://github.com/WolvenKit/Cyberpunk-Blender-add-on/releases/tag/1.1.0)****

## Exporting to Blender

First step is to locate the ent file for the character you want, I'm gonna use Jackie for the example. To start I've created a new project for him,&#x20;

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

A search for jackie in the asset browser returns plenty of files, if you sort by type and find the ent files in the list jackie\_welles.ent looks like a pretty good starting place. Right click then Open without adding to project and you can preview to confirm its him.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Expanding the appearances bit of the entity template, he has 15 appearances which all appear to be defined in jackie\_welles.app. For this next step you need to have the Wolvenkit resources plugin installed (View Options > plugins to install). The app should also be in the search results for jackie, simply right click it, then do find used files. Sort by type again and find the cookedapp files. Theres several which cover the different appearances, for each one you want to include in your export do the following:&#x20;

* Right click, do Find used files&#x20;
* Sort by type, find the mesh files&#x20;
* Select all and right click, add selected to project

You may need to go through the app file afterwards to check all the meshes got found, it sometimes seems to miss some.



![](<../../.gitbook/assets/image (1) (1) (1).png>)

The mesh files should now be visible in the project explorer, occasionally I find they arent showing up but closing and reopening the project makes them appear.

Open the Export Tool, and verify your meshes are listed. Double click one then the export options opens, and verify WithMaterials as the export type and LOD Filter is on. Set the texture type to png if it is not. Select Apply to all files of the same extension then confirm.&#x20;

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

Now select Export All (or Export Selected) on the menu bar and a bunch of glb and json files should be exported. After its done a files have been exported notification should pop up to notify you of the success. Now you should be able to fire up Blender and get importing.

Open blender, delete the default cube and go to a scripting tab, and run the following, with the path set to your project directory.

```python
import json
import glob
import os
import bpy
path = '<<YOUR PROJECT DIRECTORY>>\\source\\raw\\base'

meshes =  glob.glob(path+"\**\*.glb", recursive = True)

for mesh in meshes:
    try:
       bpy.ops.io_scene_gltf.cp77(filepath=mesh)
    except:
        print("Failed on ",mesh)
```

You should get something like the image below. If you see massive bone handles, drag select the bones and press h to hide them, and your character model should appear. Note at this point if you've exported several appearances all the meshes will be visible together, you'll need to do some organization into collections to get the outfits separated.

If it doesn't import, you can go through the folders inside your project and individually import the glb files with the Cyberpunk GLB plugin. They should import with materials wherever they are a type supported by the plugin, which unfortunately isn't all yet. You may need to change the alpha blend settings on things like tattoos, as they may show up as big chunks of black.&#x20;



<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

After a bit of organization and a switch to the Cycles renderer you should get something like this.

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

If you get lots of bits that are a bright magenta type color then the shaders are too complex for Eevee to render, and you need to switch to Cycles. Example of Eevee vs Cycles below. Please note her dress was from an older version of the shader and this issue has been mostly resolved.

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

Process is basically the same for guns and vehicles etc, track down the mesh files, add to project, export with materials.
