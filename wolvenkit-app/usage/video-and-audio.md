---
description: How to view video and audio files in WolvenKit.
---

# Video and Audio

{% hint style="info" %}
This page is about the WolvenKit app. To bulk-export or -import video and audio files, check [video-and-audio-files-cli.md](../../wolvenkit-cli/usage/video-and-audio-files-cli.md "mention")
{% endhint %}

## Audio

### Voice-overs & music

Voice-overs and most music are stored as `.wem` files – you can use the [search](wolvenkit-search-finding-files.md) to filter by extension.&#x20;

When you select an audio file in your Project Explorer or the Asset Browser, the File Information widget will turn into an audio player:

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
You can convert .wem files to playable formats using [the Export tool](import-export/). if you'd rather use the command line interface, check [#audio-files](../../wolvenkit-cli/usage/video-and-audio-files-cli.md#audio-files "mention").
{% endhint %}

### Sound effects

{% hint style="warning" %}
Sound effects are stored differently and cannot be previewed in WolvenKit. If you want to search and preview SFX, use the [SoundDB web tool](https://sounddb.redmodding.org/sfx).
{% endhint %}

You can import and export sound effects stored in .opuspak files using the Import and Export tools respectively. See this page for a walk-through:

{% content-ref url="import-export/import-export-sound-effects.md" %}
[import-export-sound-effects.md](import-export/import-export-sound-effects.md)
{% endcontent-ref %}

## Video

{% hint style="warning" %}
Wolvenkit can't preview video files. Add them to your Wolvenkit project or export them via CLI ([#video-files](../../wolvenkit-cli/usage/video-and-audio-files-cli.md#video-files "mention")) and watch them via [RADTools](http://www.radgametools.com/bnkdown.htm) as bink.
{% endhint %}

In the past, Wolvenkit used to be able to view videos. However, due to license issues, we had since to remove the plugin.

However, it was only a wrapper around RADTools, which you can also install as external tool.
