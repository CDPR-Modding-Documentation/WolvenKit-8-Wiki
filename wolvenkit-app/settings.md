---
description: Wolvenkit's settings and what they mean
---

# Settings

## TL;DR

You **must** make sure that your Game Executable Path is set. Wolvenkit will not work otherwise.

<table><thead><tr><th width="281">Setting</th><th>value</th></tr></thead><tbody><tr><td>Game Executable Path (.exe)</td><td><p>Path to the game's executable file on your hard drive, e.g. </p><p><code>C:\Games\Cyberpunk 2077\bin\x64\Cyberpunk2077.exe</code></p></td></tr><tr><td>Depot Path</td><td><p>Defaults to <code>C:\Users\yourusername\AppData\Roaming\REDModding\WolvenKit\Depot</code></p><p><br>A folder where Wolvenkit can store all its clutter. <br><strong>NOT</strong> your game directory.</p></td></tr></tbody></table>

## Settings: Overview

For a textual explanation of the seettings, see [the next section](settings.md#settings-explained)

<figure><img src="../.gitbook/assets/8.9.0 settings generic.png" alt=""><figcaption><p>Example settings window for 8.9.0</p></figcaption></figure>

<figure><img src="../.gitbook/assets/8.9.1 settings generic.png" alt=""><figcaption><p>Example settings window for 8.9.1</p></figcaption></figure>

## Settings explained

### Show File Preview

Enables interactive Quick Previews within the Properties panel. Toggle off for improved performance when navigating the Asset Browser and Project Explorer.

### **Game Executable (.exe) Path**

The **Game Executable (.exe) Path** is the location of the `Cyberpunk2077.exe` , which can be found in your `Cyberpunk 2077\bin\x64\` folder. You can paste the absolute path to the file, or use the folder icon to browse inside  [The Cyberpunk 2077 Game Directory](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-users/users-modding-cyberpunk-2077/the-cyberpunk-2077-game-directory "mention").

{% hint style="info" %}
If Cyberpunk is installed within Program Files, we recommend running WolvenKit as administrator.
{% endhint %}

### Depot Path

The **Depot Path** is a WolvenKit system folder for caching game assets.  It serves as a cache for mesh exports with materials. WolvenKit builds a repository of visual assets within the Depot for usage with external applications such as MLSetupBuilder or Blender.&#x20;

By default, it is set to `C:\Users\yourusername\AppData\Roaming\REDModding\WolvenKit\Depot`, but you can pick any location. It does not need to be on an SSD, although Wolvenkit might load faster if it is.

{% hint style="warning" %}
Depending on how many game assets you extract, the Depot can grow to more than 30 gigabytes.
{% endhint %}

Learn more about the [**Material exports here**](usage/blender-integration.md)**.**

### Analyze Mods

Uncheck the box to disable validation of installed `.archive` files. This will improve performance when switching to the [Mod Browser](editor/asset-browser.md#mod-browser), but you won't receive warnings about corrupt archives anymore.

### Additional Mod Directory

A directory for .archive mods outside of your game directory, for example for resources that you want to load for multiple projects. Mods inside this folder will show up in the [Mod Browser](editor/asset-browser.md#mod-browser) **after** your installed mods.

## File Editor

### Group Large Collections

Toggles limited collections for improved performance within the File Editor when working when navigating large files.

### Group Size

Adjusts the amount of elements of in a limited collection within the File Editor.

### Default to Simple Mode

Starting with 1.14, Wolvenkit offers multiple editor modes. You can find details under [#switching-editor-modes](editor/file-editor/#switching-editor-modes "mention").

## General

### **Show Guided Tour**

UNKNOWN FUNCTIONALITY\
This toggle may not work in the latest WolvenKit build.

### **Update Channel**

The update channel determines which type WolvenKit updates are received.

* **Stable**    WolvenKit will only show prompts when new releases are published (recommended)
* **Nightly**    WolvenKit will show the latest development builds which may be unstable

### **Theme Accent**

Changes the accent color of UI elements throughout WolvenKit.
