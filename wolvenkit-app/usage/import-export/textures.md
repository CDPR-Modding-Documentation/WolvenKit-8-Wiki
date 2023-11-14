---
description: How to import and export textures
---

# Import/Export: Textures

WolvenKit is capable of exporting Cyberpunk XBM files to common formats like png. It will try and automatically determine the correct import settings based on the file name.&#x20;

{% hint style="info" %}
For the UI documentation, check [tools-import-export](../../tools/tools-import-export/ "mention")

For general information such as the file structure and output directory, check [.](./ "mention")

For a step-by-step workflow and troubleshooting, see [Cyberpunk 2077 Modding](http://127.0.0.1:5000/o/-MP5ijqI11FeeX7c8-N8/s/4gzcGtLrr90pVjAWVdTc/ "mention") ->  [Textures: Importing, editing, exporting](http://127.0.0.1:5000/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators/modding-guides/textures-and-luts/images-importing-editing-exporting "mention")
{% endhint %}

## Exporting a texture from Wolvenkit

1. Add the xbm file to your project
2. Open the Export tool (Tools -> Export Tool)
3. Select your texture
4. Click "Export Selected"

<figure><img src="../../../.gitbook/assets/images_export_selected.png" alt=""><figcaption></figcaption></figure>

This will generate a png file in your project's raw folder.

### Export Options

#### XBM Export Type

Choose a common image format for exported textures.

#### Flip Image

Vertically invert textures for convenience

## Importing textures

WolvenKit is capable of importing custom images as Cyberpunk XBM files. The Import/Export Tool can replace an existing XBM or generate new standalone XBM.&#x20;

{% hint style="info" %}
For compatibility reasons, you might want to stick to **png** files.
{% endhint %}

The easiest way to go about it is this:

1. Add an existing xbm file of the same type that you want to import to your Wolvenkit project.&#x20;
2. [Export](textures.md#exporting-a-texture-from-wolvenkit) the xbm file: this adds a png file with the same name to your project's raw folder.
3. Overwrite the png with your edited texture.
4. Open the Import tool, and select your png file. \
   _The correct settings should be applied automatically._&#x20;
5. Click "Import Selected".

<figure><img src="../../../.gitbook/assets/images_import_selected.png" alt=""><figcaption></figcaption></figure>

### Import Options

#### isGamma

Sets isGamma boolean upon import. Color textures (such as diffuse) must be set as true, or they will appear blown-out or too bright in-game.

#### Advanced Options

By default advanced XBM options are hidden. This can be changed by modifying WolvenKit [**Settings**](../../settings.md).

