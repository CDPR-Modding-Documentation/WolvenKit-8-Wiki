---
description: A list of Wolvenkit error codes, and what they mean
---

# Error Codes

## Summary

**Published**: May 1 2024 by [manavortex](https://app.gitbook.com/u/NfZBoxGegfUqB33J9HXuCs6PVaC3 "mention")\
**Last documented update**: May 1 2024 by [manavortex](https://app.gitbook.com/u/NfZBoxGegfUqB33J9HXuCs6PVaC3 "mention")

This page contains an overview about Wolvenkit's internal error codes and what they mean.

{% hint style="warning" %}
For **developers**:&#x20;

When editing this page (especially section headers), please update the internal mapping:\
`WolvenKit/Helpers/LogCodeHelper.cs`
{% endhint %}

## What to do with an error

If you ended up on this page, you ran into a problem that needs to be fixed inside WolvenKit. You now have the following options:

### Install the Nightly

If you are on the stable release, you should try [the-wolvenkit-nightly.md](../getting-started/download/the-wolvenkit-nightly.md "mention"). There's a good chance that your problem is already solved.

### Update all tools involved

Make sure that you are on the most recent version of whatever tool's you're using. This includes, but is not limited to, the [Wolvenkit Blender IO Suite](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators-theory/modding-tools/wolvenkit-blender-io-suite "mention") and [MLSETUP Builder](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators-theory/modding-tools/mlsetup-builder "mention").

### Find support on Discord

Find our [discord server](http://discord.gg/redmodding) and hit up the **`#wolvenkit-support`** channel. (Don't bother if you aren't on the Nightly yet, it's the first thing anyone there will tell you.)

### Create a ticket

If your error still happens in the Nightly, you need to **tell us about it**. It's easy: bugs that don't get reported don't get fixed.&#x20;

Head to Wolvenkit's github page and [create a ticket](https://github.com/WolvenKit/Wolvenkit/issues) (you need a github or Google account, but they won't send you spam).&#x20;

To fix the bug, we need to **watch it in action**. Please include everything we need to make it happen!

## Error code list

### 0x2000: Type not supported (8192)

WolvenKit ran into a problem during internal conversion. Here's what you can do:

1. Install [the-wolvenkit-nightly.md](../getting-started/download/the-wolvenkit-nightly.md "mention")
2. Re-create whatever file you were trying to work on at that time:
   1. A game file from an earlier patch: Add it to your project again
   2. A depot file: Delete the file from the depot and/or [re-create the depot](usage/create-depot/#steps-partial-depot)
   3. A raw file: re-create the file with the latest version of whatever tool you used (Wolvenkit, the [Wolvenkit Blender IO Suite](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators-theory/modding-tools/wolvenkit-blender-io-suite "mention")...)

If that doesn't work, please get in touch via [Discord](https://discord.com/invite/redmodding) or browse the troubleshooting section.

### 0x5000: Invalid settings

You have an unspecified issue with your settings. Double-check them and make sure that everything is configured correctly.&#x20;

If that doesn't help, remove or re-name your settings file and restart WolvenKit:

```
C:\Users\<yourusername>\AppData\Roaming\RedModding\Wolvenkit\config.json
```

### 0x5001: Invalid Game File Executable

Check your [settings.md](settings.md "mention") ->[#game-executable-.exe-path](settings.md#game-executable-.exe-path "mention") and make sure that it points at your `Cyberpunk2077.exe`. For more information, check the wiki link.

### 0x5002: Failed to launch game executable

Check [#id-0x5001-invalid-game-file-executable](error-codes.md#id-0x5001-invalid-game-file-executable "mention") and make sure that all your settings are valid. If that doesn't fix your problem, you may have to reset your settings, see [#id-0x5000-invalid-settings](error-codes.md#id-0x5000-invalid-settings "mention") for detes.

