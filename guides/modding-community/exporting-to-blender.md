---
description: >-
  Step-by-step guide for exporting to Blender for non-mod use (i.e. cosplay, 3d
  print, etc.)
---

# Exporting Characters to Blender

## Summary

**Created by** [Simarilius](https://app.gitbook.com/u/G2MqNkfgTlQ1R3G4B5s6WefLjdy2 "mention") **&** [dragonzkiller](https://app.gitbook.com/u/dpriBUirXwWYeCIhyywmqhKrMMV2 "mention")\
**Published: September 03 2022**\
**Last documented update: December 29 2023**

This guide aims to walk you through finding and exporting a character to blender so that its usable for cosplay or 3d printing or whatever. Guide is using nightly WolvenKit, Cyberpunk add-on for Blender, and Blender 3.6.

#### This guide uses the following versions:

* Cyberpunk 2077 game version 2.1&#x20;
* Blender >= [3.6 (stable)](https://www.blender.org/download/lts/3-6/) or [4.0](https://www.blender.org/download/releases/4-0/)
* Wolvenkit >= 8.11.1 ([stable](https://github.com/WolvenKit/Wolvenkit/releases) | [Nightly](https://github.com/WolvenKit/WolvenKit-nightly-releases))
* [Wolvenkit IO suite for Blender >= 1.5.1](https://github.com/WolvenKit/Cyberpunk-Blender-add-on)

## Prerequisites

* [ ] You have [created a new Wolvenkit project](../../wolvenkit-app/usage/wolvenkit-projects.md#create-a-new-wolvenkit-mod-project)

{% hint style="warning" %}
This guide works just the same for guns — add the .ent to your project, run the script, import, profit. Vehicles are more complex and have their own guide: please see [exporting-vehicles.md](../../modding-community/exporting-vehicles.md "mention") for these.

If you want to add a character's animations, you can check the follow-up guide [exporting-rigs-and-anims.md](exporting-to-blender/exporting-rigs-and-anims.md "mention").
{% endhint %}

## The character's .ent file

This section will tell you how to find and add an NPC's file to your project. If you already have one (because you're exporting an NPV), you can skip it and go straight to [#exporting-to-blender](exporting-to-blender.md#exporting-to-blender "mention").

### Finding the file

Before we can export anything, we need to find the `.ent` file for the character we want to export. This tutorial will use Jackie, but it works just the same for everyone else.

{% hint style="info" %}
You can find a list of the entity files for a lot of the main characters over on the Cyberpunk 2077 Modding wiki [Here](https://wiki.redmodding.org/cyberpunk-2077-modding/for-mod-creators/references-lists-and-overviews/people)
{% endhint %}

With our project open in Wolvenkit, we switch to the [Asset Browser](../../wolvenkit-app/editor/asset-browser.md) and search for the right file:

```
jackie
```

{% hint style="info" %}
You can refine your search, checking only .ent files, by using the following search query:&#x20;

```
jackie > .ent
```
{% endhint %}

This will give us plenty of files — we'll sort them by file extension and scroll to the `ent` section of the list. `jackie_welles.ent` looks promising, so we'll double-check if it's the right file:&#x20;

* Right-click it and select `Open without adding to project`
* Use the `entity preview` tab to confirm that it's him

<figure><img src="../../.gitbook/assets/image (4) (2).png" alt=""><figcaption></figcaption></figure>

Now, [add the file to your project](../../wolvenkit-app/editor/asset-browser.md#adding-files-to-projects).

## Exporting to Blender

With the `.ent` file in your project, you can run the script that will handle the actual export, adding all the necessary files to your project and exporting them in a way that Blender can process.

Open the [script-manager.md](../../wolvenkit-app/tools/script-manager.md "mention") (Tools -> Script Manager as of Wolvenkit 8.15), find `Export_Ent.wscript` and run it.

{% hint style="info" %}
Wscript cant export files from other mods currently, if your exporting an NPV which uses other mods you will need to add any used files/materials to the project manually if you want them in Blender.
{% endhint %}



<details>

<summary>What does the script do/how to do it by hand? (You don't need to know this)</summary>

If you open the Entity file then expand the appearances bit of the entity template, he has 15 appearances which all appear to be defined in jackie\_welles.app. For this next step you need to have the Wolvenkit resources plugin installed (View Options > plugins to install). The app should also be in the search results for jackie, simply right click it, then do find used files. Sort by type again and find the cookedapp files. Theres several which cover the different appearances, for each one you want to include in your export do the following:&#x20;

* Right click, do Find used files&#x20;
* Sort by type, find the mesh files&#x20;
* Select all and right click, add selected to project

You may need to go through the app file afterwards to check all the meshes got found, it sometimes seems to miss some.

The mesh files should now be visible in the project explorer, occasionally I find they arent showing up but closing and reopening the project makes them appear.

Open the Export Tool, and verify your meshes are listed. Double click one then the export options opens, and verify WithMaterials as the export type and LOD Filter is on. Set the texture type to png if it is not. Select Apply to all files of the same extension then confirm.&#x20;

<img src="../../.gitbook/assets/image (7) (1) (1).png" alt="" data-size="original">

Now select Export All (or Export Selected) on the menu bar and a bunch of glb and json files should be exported. After its done a files have been exported notification should pop up to notify you of the success.&#x20;

</details>

{% hint style="success" %}
After the script has successfully run, you will find an `.ent.json` file in your project's [raw folder.](../../wolvenkit-app/editor/project-explorer.md#raw)
{% endhint %}

## Importing into Blender

{% hint style="info" %}
If you right-click the `.ent` file in the project browser and press `Shift` and `Ctrl`, the context menu will let you copy the path to the file!
{% endhint %}

Switch to Blender and use the [Wolvenkit Blender IO Suite](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators-theory/modding-tools/wolvenkit-blender-io-suite "mention")'s [Entity Import](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators-theory/modding-tools/wolvenkit-blender-io-suite/wkit-blender-plugin-import-export#importing-into-blender-2) from the File -> Import menu.&#x20;

{% hint style="warning" %}
Before clicking the import button, please read the next section about [#importing-a-specific-appearance](exporting-to-blender.md#importing-a-specific-appearance "mention").
{% endhint %}

{% hint style="info" %}
Find the full documentation on the yellow wiki under  [Wolvenkit Blender IO Suite](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators-theory/modding-tools/wolvenkit-blender-io-suite "mention") -> [WKit Blender Plugin: Import/Export](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators-theory/modding-tools/wolvenkit-blender-io-suite/wkit-blender-plugin-import-export "mention") ->  [Entities](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators-theory/modding-tools/wolvenkit-blender-io-suite/wkit-blender-plugin-import-export#entities "mention")
{% endhint %}



Point it to the exported `.ent.json` in your project's files.  For Jackie, the relative path is `source\raw\base\characters\entities\main_npc\jackie_welles.ent.json`.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F4gzcGtLrr90pVjAWVdTc%2Fuploads%2FlkiC2IKH8JGip9AqSc9c%2Fblender_plugin_import_entity_2.png?alt=media&#x26;token=e34fa8dc-916e-44c9-a294-94af9771e1e0" alt=""><figcaption></figcaption></figure>

### Importing a specific appearance

Unless you specify otherwise, the `default` appearance will be chosen. If you want another, open the `.ent` file in your project and enter the exact **appearanceName** into the Blender open dialog.&#x20;

You can find the appearance name in your `.ent` file inside the `appearances` list:

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>The same file that you picked in Step 1</p></figcaption></figure>

Now, click the `Import Ent from JSON` button and wait while the Blender plugin does its thing.&#x20;

{% hint style="info" %}
Blender might need a few minutes to load the materials and bake the shaders. If you aren't getting any errors, just assume that it's still at it.&#x20;

To double-check, you can select Window -> Toggle System Console to watch Blender work.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>
