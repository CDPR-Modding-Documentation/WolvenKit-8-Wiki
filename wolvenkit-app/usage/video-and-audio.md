---
description: How to view video and audio files in Wolvenkit
---

# Video and Audio

{% hint style="info" %}
This page is about the Wolvenkit app. To bulk-export or -import video and audio files, check [video-and-audio-files-cli.md](../../wolvenkit-cli/usage/video-and-audio-files-cli.md "mention")
{% endhint %}

## Audio

Audio files within Wolvenkit are saved as `.wem` files – you can use the [search](wolvenkit-search-finding-files.md) to filter by extension.

When you select an audio file in your Project Explorer or the Asset Browser, the File Information widget will turn into an audio player:

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
You can convert .wem files to .ogg via as [Revorb](https://cloudflare-ipfs.com/ipfs/QmVgjfU7qgPEtANatrfh7VQJby9t1ojrTbN7X8Ei4djF4e/revorb.exe). if you'd rather use the command line interface, check [#audio-files](../../wolvenkit-cli/usage/video-and-audio-files-cli.md#audio-files "mention").
{% endhint %}

## Video

{% hint style="warning" %}
Wolvenkit can't preview video files. Add them to your Wolvenkit project or export them via CLI ([#video-files](../../wolvenkit-cli/usage/video-and-audio-files-cli.md#video-files "mention")) and watch them via [RADTools](http://www.radgametools.com/bnkdown.htm) as bink.
{% endhint %}

In the past, Wolvenkit used to be able to view videos. However, due to license issues, we had since to remove the plugin.

However, it was only a wrapper around RADTools, which you can also install as external tool.
