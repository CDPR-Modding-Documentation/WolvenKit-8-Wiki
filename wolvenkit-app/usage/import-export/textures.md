---
description: How to import and export textures
---

# Import/Export: Textures

WolvenKit is capable of exporting Cyberpunk XBM files to common formats like png. It will try and automatically determine the correct import settings based on the file name.&#x20;

{% hint style="info" %}
For the UI documentation, check [tools-import-export.md](../../tools/tools-import-export.md "mention")

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

Choose a common image format for exported textures. Possible options (as of 8.9.1):

* png
* dds
* tga
* bmp
* jpg
* png

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

<figure><img src="../../../.gitbook/assets/wolvenkit_import_png.png" alt=""><figcaption></figcaption></figure>

####

#### Advanced Options

By default advanced XBM options are hidden. This can be changed by modifying WolvenKit [**Settings**](../../settings.md). (Is this still the case? Double-check)

#### Texture Group

Select a preset for import. **This will preselect the options below**, so pick  the right one for your use case!

{% hint style="info" %}
Wolvenkit will try to guess the right preset from your file name, so you'll want to stick to the game's naming conventions.
{% endhint %}

Possible values are:

* TexG\_Generic\_Color
* TexG\_Generic\_Grayscale
* TexG\_Generic\_Normal
* TexG\_Generic\_Data
* TexG\_Generic\_UI
* TexG\_Generic\_Font
* TexG\_Generic\_LUT
* TexG\_Generic\_MorphBlend
* TexG\_Multilayer\_Color
* TexG\_Multilayer\_Normal
* TexG\_Multilayer\_Grayscale
* TexG\_Multilayer\_Microblend

#### isGamma

Sets isGamma boolean upon import. Color textures (such as diffuse) must be set as true, or they will appear blown-out or too bright in-game.

#### VFlip (Default: True)

Should the image be v-flipped?

{% hint style="warning" %}
The game saves images as upside-down. Wolvenkit will fix that for you, so unless your texture is already flipped, you'll want to leave this alone.
{% endhint %}

#### RawFormat

_as of 8.9.1_

Raw format for export. Possible values are:

* TRF\_Invalid
* TRF\_TrueColor
* TRF\_DeepColor
* TRF\_Grayscale
* TRF\_HDRFloat
* TRF\_HDRHalf
* TRF\_HDRFloatGrayscale
* TRF\_Grayscale\_Font
* TRF\_R8G8
* TRF\_R32UI
* TRF\_Max

#### Generate MipMaps

Should [MipMap](https://en.wikipedia.org/wiki/Mipmap)s be created?

{% hint style="warning" %}
The \
This requires the texture width and height to be potencies of 2!
{% endhint %}

#### IsStreamable

???

#### PremultiplyAlpha

???

