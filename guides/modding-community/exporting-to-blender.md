---
description: >-
  Step-by-step guide for exporting to Blender for non-mod use (i.e. cosplay, 3d
  print, etc.)
---

# Exporting Characters to Blender

## Summary

**Created by** [Simarilius](http://127.0.0.1:5000/u/G2MqNkfgTlQ1R3G4B5s6WefLjdy2 "mention") **&** [dragonzkiller](http://127.0.0.1:5000/u/dpriBUirXwWYeCIhyywmqhKrMMV2 "mention")\
**Published September 03 2022 (last updated Oct 2023)**

This guide aims to walk you through finding and exporting a character to blender so that its usable for cosplay or 3d printing or whatever. Guide is using nightly WolvenKit, Cyberpunk add-on for Blender, and Blender 3.6.

#### This guide uses the following versions:

* Cyberpunk 2077 game version 2.01&#x20;
* Blender 3.6 stable
* Cyberpunk add-on for Blender 1.4.0

### Requirements

* [**WolvenKit latest nightly release version**](https://github.com/WolvenKit/WolvenKit-nightly-releases)
* [**Blender 3.6**](https://www.blender.org/) **or newer**
* [**Cyberpunk add-on for Blender 1.4.0**](https://github.com/WolvenKit/Cyberpunk-Blender-add-on/releases) **or newer**

## Exporting to Blender

First step is to locate the ent file for the character you want, I'm gonna use Jackie for the example. To start I've created a new project for him,&#x20;

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

A search for jackie in the asset browser returns plenty of files, if you sort by type and find the ent files in the list jackie\_welles.ent looks like a pretty good starting place. Right click then Open without adding to project and you can preview to confirm its him.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
You can find a list of the entity files for a lot of the main characters over on the Cyberpunk 2077 Modding wiki [Here](https://wiki.redmodding.org/cyberpunk-2077-modding/for-mod-creators/references-lists-and-overviews/people)
{% endhint %}

Add the ent file to the project, then do Tools>Scripts and Run the Export\_Ent script. That will add all the files used by the entity to the project, export the meshes to glb and json the ent and app files.

<details>

<summary>If you want to know what the script is doing, the manual way of doing it is shown here, but you shouldnt need to know this.</summary>

If you open the Entity file then expand the appearances bit of the entity template, he has 15 appearances which all appear to be defined in jackie\_welles.app. For this next step you need to have the Wolvenkit resources plugin installed (View Options > plugins to install). The app should also be in the search results for jackie, simply right click it, then do find used files. Sort by type again and find the cookedapp files. Theres several which cover the different appearances, for each one you want to include in your export do the following:&#x20;

* Right click, do Find used files&#x20;
* Sort by type, find the mesh files&#x20;
* Select all and right click, add selected to project

You may need to go through the app file afterwards to check all the meshes got found, it sometimes seems to miss some.

The mesh files should now be visible in the project explorer, occasionally I find they arent showing up but closing and reopening the project makes them appear.

Open the Export Tool, and verify your meshes are listed. Double click one then the export options opens, and verify WithMaterials as the export type and LOD Filter is on. Set the texture type to png if it is not. Select Apply to all files of the same extension then confirm.&#x20;

<img src="../../.gitbook/assets/image (7) (1).png" alt="" data-size="original">

Now select Export All (or Export Selected) on the menu bar and a bunch of glb and json files should be exported. After its done a files have been exported notification should pop up to notify you of the success.&#x20;

</details>

### Get a specific appearance

If you're fine with the default appearance, you can go to the next section and import your project into Blender.

Otherwise, you need to enter the exact **appearanceName** into the Blender open dialog. You can find the appearance name in your `.ent` file inside the `appearances` list:

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>The same file that you picked in Step 1</p></figcaption></figure>

### Importing to Blender

Open blender, go file>import then select Cyberpunk Entity (.json)

Navigate to the json of the character that the script created, will be in the source\raw folders inside your project, for Jackie its source\raw\base\characters\entities\main\_npc\jackie\_welles.ent.json

{% hint style="info" %}
Phantom Liberty files are in ep1 not base, and some of the main npcs have files in both, be careful not to get confused!
{% endhint %}

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

If you get any stuff thats Solid black in cycles is probably getting SVM errors, which you can solve by cutting off some of the normals in the multilayer. (we're working on a proper fix) Eevee works fairly well these days, shaders just take a while to compile.

Process is basically the same for guns etc, track down the ent files, add to project, run the script and import. For vehicles its a bit more involved, theres a guide for that [here](https://wiki.redmodding.org/wolvenkit/modding-community/exporting-to-blender/exporting-vehicles).
