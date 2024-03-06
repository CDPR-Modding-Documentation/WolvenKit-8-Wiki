---
description: The depot is a collection of image and binary files used for modding the game
---

# The Wolvenkit Depot

## Section Brief

Formerly part of the ELI5 guide, this has been moved to the general section.

The depot is where wolvenkit stores accessible copies of basegame assets that are needed for editing/viewing project assets. With the current version of wolvenkit, you DO NOT need to do anything other than specify a folder for it. Everything else happens seamlessly in the background as and when needed. The only reason to generate a depot now is for using MLSB. If your not doing that, just skip this.



There are three methods of creating and maintaining a depot:

{% hint style="danger" %}
I recommend that you skip this section for now and do the Validate Functionality steps first. Based on what you learn there, make the decision which kind of Depot you want.
{% endhint %}

1. [**Adhoc Depot**](./#steps-adhoc-depot) is the manual process of creating the asset files as you need them. The general idea is that almost all the files you need are already accessible to WolvenKit. The biggest benefit is the minimal disk space usage.&#x20;
2. [**Partial Depot**](./#steps-partial-depot) is mostly uncooked and unbundled, and it's only missing the GLB files. Unless you are needing that specific file type, this depot has everything you will need.  The biggest detractor is that it requires 120GiB of disk space. It will let you access the microblends and masks in MLSB, but wont have meshes available.
3. [**Full Depot**](./#steps-full-depot) (outdated as of 2023!) is every asset available to us. The biggest benefit is that everything is ready to use and MLSB can work with the assets. The biggest detractor is that it requires 160GiB of disk space.

## Steps: Adhoc Depot

{% hint style="info" %}
If you understand how the asset files relate to each other, then an Adhoc Depot works perfectly fine. Be aware that experience and knowledge are required if this is the type of depot you want to maintain.

* An in-game item is used to find the ENT file,
* The ENT file is used to find the APP file,
* The APP file is used to find the MESH file,&#x20;
* The MESH file is used to find the MLMASK, MLSETUP, and XBM files, and it can be exported to create the GLB file,
* The MLSETUP file is used to find the material layers and the MLTEMPLATE file,
* MLMASK file can be exported to create the DDS files,
* DDS file can be imported to create the XBM file, but the XBM file can also be accessed directly from the MESH.
{% endhint %}

1.  Add the asset to your project which also adds the asset to the Import/Export Tool.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Depot_Adhoc_S01.png" alt=""><figcaption></figcaption></figure>
2.  Open the Import/Export Tool, right click on asset, and click on Show Settings. Most of the time the default settings will provide you the output you're needing, but for DDS files from MLMASK and if you need the rig files, then you'll need to get into the settings to make those alterations.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Depot_Adhoc_S02.png" alt=""><figcaption></figcaption></figure>
3.  Once you have the settings to what you need, either select the files you want to export and click the Process Selected button, or click the Process All for everything on the list.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Depot_Adhoc_S03.png" alt=""><figcaption></figcaption></figure>

## Steps: Partial Depot

{% hint style="info" %}
Some of the unbundle files are already accessible in the WolvenKit Asset Browser. You may want to search for the files you want in Asset Browser before unbundling the game. For the ones that aren't, the source files can be accessed through the mesh file and the Import/Export tool will generate them.
{% endhint %}

1.  Launch WolvenKit application and click on Tools then Depot Generator.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Depot_Partial_S01.png" alt=""><figcaption></figcaption></figure>
2.  Click into the field next to Depot Path and select the folder C:\Cyberpunk2077Mod\Depot

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Depot_Partial_S02.png" alt=""><figcaption></figcaption></figure>
3. Select PNG and then click the Generate Materials button. While the program is running, the button will deactivate and once the program is complete File Explorer will automatically open at the location of your Depot.

<figure><img src="../../../.gitbook/assets/ELI5_GetStart_Depot_Partial_S04.png" alt=""><figcaption></figcaption></figure>

6. You do not need to unbundle anything else, since the Wolvenkit exports will do that for you. If you want, you can stop reading now.
7. To unbundle the following list of extensions click on the **Unbundle Game** button: `gradient`, `w2mi`, `matlib`, `emt`, `sp`, `hp`, `fp`, `mi`, `mt`, `mlsetup`, `mltemplate`, and `texarray`.&#x20;

<figure><img src="../../../.gitbook/assets/ELI5_GetStart_Depot_Partial_S05.png" alt=""><figcaption></figcaption></figure>

## Steps: Full Depot

{% hint style="danger" %}
As of October 2023 and Wolvenkit 8.11, you do not need a full depot. The process is still documented under [legacy-full-depot.md](legacy-full-depot.md "mention"). However, it is advised that you stick to a [partial depot.](./#steps-partial-depot)
{% endhint %}
