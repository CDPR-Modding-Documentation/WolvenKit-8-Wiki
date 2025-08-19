---
description: How to import and export audio from opusinfo/opuspaks.
---

# Import/Export: Sound effects

Unlike music and voice-overs, sound effects in Cyberpunk 2077 are stored inside .opuspak files, which are described by a single `sfx_container.opusinfo` file.

{% hint style="info" %}
For the UI documentation, check [Tools: Import/Export UI](https://wiki.redmodding.org/wolvenkit/wolvenkit-app/tools/tools-import-export)

For general information such as the file structure and output directory, check [Import/Export](https://wiki.redmodding.org/wolvenkit/wolvenkit-app/usage/import-export)
{% endhint %}

## Exporting sound effects

In order to export sound effects, you need to have the `sfx_container.opusinfo` file in your project. Find it in the [Asset Browser](../../editor/asset-browser.md) and [add it to your project](../../editor/asset-browser.md#adding-files-to-projects).

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption><p>You should now see the file in the project explorer.</p></figcaption></figure>

With the opusinfo selected in the Export tool (if you don't see the file, press Refresh), you should now see the export options on the right.&#x20;

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption><p>The Export Tool looks something like this.</p></figcaption></figure>

The important field for us here is "Selected for Export". Click the three dots on the right to open a selection window where you can choose which hashes to export. Click the hash you want and press the arrow button pointing right to add it to selection.

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption><p>Hash selection window</p></figcaption></figure>

{% hint style="info" %}
_Hash_ is basically an ID of a sound. To find the hashes you need, you can use the [SoundDB web tool](https://sounddb.redmodding.org/sfx).
{% endhint %}

Once you've selected what you want, press Finish to confirm the selection and back in the Export tool press "Export Selected". The sounds you've chosen should now be in the raw folder of your project. You will find two files for each of the sounds, one is origin `.opus` and the other is `.wav`. You can usually ignore the .opus file.

## Importing sound effects

{% hint style="danger" %}
Note that importing sounds this way is **incompatible** with any other mod modifying the sounds this way. You should prefer using [the REDmod method](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators-theory/modding-tools/redmod/audio-modding)!
{% endhint %}

To import back a sound effect, all you need is the sound file in `.wav` format with the exact same filename it had when you exported it. It should also be in the same folder (raw).

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption><p>The import tool with a sound effect selected.</p></figcaption></figure>

You can usually leave the default settings as they are. After pressing "Import selected", your project's archive folder should now contain a new modified `sfx_container.opusinfo` and one or more `sfx_container_XXX.opuspak` (XXX being a number). The opuspak contains your new sound (and other sounds too).

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption><p>Example of imported sound effect result.</p></figcaption></figure>
