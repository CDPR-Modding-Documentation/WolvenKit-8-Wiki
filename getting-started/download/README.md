---
description: Downloading the WolvenKit application
---

# Download, Install and Setup

## Summary

**Published: October 22 20**\
**Created by @JJTurtle**\
\
**Last documented update: @manavortex, February 25 2023**

This section will walk you through the process of downloading and installing Wolvenkit.&#x20;

{% hint style="info" %}
There is a [Full Install Walkthrough (ELI5)](../eli5-getting-started/), which you can follow if you are not very computer-savy or feel insecure about modding. If you've been sent here by the same guide, ignore this box and start with the [prerequisites](./#prerequisites). :)&#x20;
{% endhint %}

### TL;DR

1. Install REDMod and .NET from the [Prerequisites](./#prerequisites) section below
2. Download Wolvenkit-X.X.X.zip from github ([stable](https://github.com/WolvenKit/Wolvenkit/releases) | [nightly](https://github.com/WolvenKit/WolvenKit-nightly-releases/releases/))
3. Extract it to a folder of your choice
4. Run it and do the [initial configuration](./#first-launch-tl-dr)
5. Optional: Proceed to the guide how to [set up the modding tools](../eli5-getting-started/configure-modding-tools.md)

## Prerequisites

For detailed instructions on installing other software that you might need for mod development, see the section&#x20;

* Windows 10/11 (64-bit) or a Linux build of your choice
* [REDMod](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-users/users-modding-cyberpunk-2077/redmod#installation) (Cyberpunk's modding framework)
* For older WKit versions: [Microsoft .NET 6](https://dotnet.microsoft.com/en-us/download/dotnet/6.0) (versions <= 8.7.1)
* For current WKit: The most recent [Microsoft .NET](https://dotnet.microsoft.com/en-us/download) (confirmed working with [.NET 8](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) and Wolvenkit 8.13)

{% hint style="success" %}
Wolvenkit is mostly developed and used on Windows — if you're on Linux, you should know what we're doing, and this guide isn't for you.

**Unrelated:** The Wolvenkit developer team is looking for a Linux nerd who'd like to keep things compatible!
{% endhint %}

<details>

<summary>Downloading .NET</summary>

Open either of these pages:&#x20;

* [6.0](https://dotnet.microsoft.com/en-us/download)
* [7.0](https://dotnet.microsoft.com/en-us/download/dotnet/7.0)

Download and install the **runtime**. (The SDK is for .NET developers…. unless you are a NET developer, and in which case do whatever you want :smile:)

<img src="../../.gitbook/assets/ELI5_GetStart_Prep_S02.png" alt="" data-size="original">

</details>

## Downloading Wolvenkit

{% hint style="info" %}
If you don't care about the differences, go to the next section: [Which version do I want?](./#which-version-do-i-want)
{% endhint %}

You can download Wolvenkit from any of the following links (click on the cards). If you are uncertain, go to [Nexus](https://www.nexusmods.com/cyberpunk2077/mods/2201).

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td></td><td></td><td></td><td><a href="https://github.com/WolvenKit/Wolvenkit/releases">https://github.com/WolvenKit/Wolvenkit/releases</a></td><td><a href="../../.gitbook/assets/wkit_stable.png">wkit_stable.png</a></td></tr><tr><td></td><td></td><td></td><td><a href="https://www.nexusmods.com/cyberpunk2077/mods/2201">https://www.nexusmods.com/cyberpunk2077/mods/2201</a></td><td><a href="../../.gitbook/assets/wkit_nexus_stable.png">wkit_nexus_stable.png</a></td></tr><tr><td></td><td></td><td></td><td><a href="https://github.com/WolvenKit/WolvenKit-nightly-releases/releases">https://github.com/WolvenKit/WolvenKit-nightly-releases/releases</a></td><td><a href="../../.gitbook/assets/wkit_nightly.png">wkit_nightly.png</a></td></tr></tbody></table>

{% hint style="info" %}
GitHub (the links with the Wolvenkit icon) is the best way to stay up-to-date with WolvenKit, as this is where development happens. You can download the latest [stable release](https://github.com/WolvenKit/Wolvenkit/releases) or Nightly [tester and developer builds](https://github.com/WolvenKit/WolvenKit-nightly-releases/releases/tag/8.9.1-nightly.2023-07-28) fresh from the pipeline.&#x20;

One of the Wolvenkit developers will download the stable version from github to put it on [Nexus](https://www.nexusmods.com/cyberpunk2077/mods/2201), so you can get it from there as well.
{% endhint %}

### What's a "Nightly" and do I want it?

The Nightly is a build of the latest development stand, created automatically every night via pipeline (hence the name). It contains new features that are being worked on, but introduces the risk of bugs.

You will usually want to use the stable version, unless you want to try out new features, help with development and testing, or generally like to live dangerously.

Here are links to the most recent build for each repository:

| Package                                                                               | Latest Release                                                                                                                                                                              | Checks                                                                                                         |
| ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| [WolvenKit](https://github.com/WolvenKit/WolvenKit/releases)                          | [![GitHub release (latest by date)](https://img.shields.io/github/v/release/WolvenKit/WolvenKit)](https://github.com/WolvenKit/WolvenKit/releases/latest)                                   | ![GitHub branch checks state](https://img.shields.io/github/workflow/status/WolvenKit/WolvenKit/check-only)    |
| [WolvenKit Nightly](https://github.com/WolvenKit/WolvenKit-nightly-releases/releases) | [![GitHub release (latest by date)](https://img.shields.io/github/v/release/WolvenKit/WolvenKit-nightly-releases)](https://github.com/WolvenKit/WolvenKit-nightly-releases/releases/latest) | ![GitHub Workflow Status](https://img.shields.io/github/workflow/status/WolvenKit/WolvenKit/WolvenKit-Nightly) |

## Which version do I want?

If you're on Nexus, then you can only download the portable (default) version. In this case, head to the next section.

Github offers you more options:

{% hint style="info" %}
If you don't know which one to use, use the default (portable) one, it's usually the first entry in the list.

You don't need to download Wolvenkti Console, unless a (not-outdated) guide tells you so.
{% endhint %}

| Download option                                              | What is it?                                                                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Wolvenkit-X.X.X.zip<br><strong>You want this</strong></p> | **Default** — the portable version: download and extract this, then start it via Wolvenkit.exe                                                                                                                                                                                                                                                             |
| Wolvenkit.Console-X.X.X.zip                                  | <p>Command Line Interface (CLI): Not the same as regular Wolvenkit. Formerly known as CP2077tools, and becoming increasingly obsolete.</p><p></p><p>Used by other applications to "talk" to Wolvenkit, for example <a href="https://wiki.redmodding.org/cyberpunk-2077-modding/for-mod-creators/modding-tools/mlsetup-builder">MLSetupBuilder</a>.<br></p> |
| Wolvenkit.ConsoleLinux-X.X.X.zip                             | As above, but on Linux. You usually don't need this.                                                                                                                                                                                                                                                                                                       |
| WolvenkitSetup-X.X.X.zip                                     | <p>The Wolvenkit <strong>installer</strong>. This will run a setup and let you pick a folder.<br>Currently (December 2024), the installer has issues.</p>                                                                                                                                                                                                  |
| <p>Source code (zip)<br>Source code (tar.gz)</p>             | A snapshot of the source code that was compiled into this specific release. If you're not a programmer, then you don't want this.                                                                                                                                                                                                                          |



<details>

<summary>Detailed download instructions (with screenshots!)</summary>



Download **either** Stable or Nightly release.

*   [Stable Release](https://github.com/WolvenKit/WolvenKit/releases/latest)

    <figure><img src="../../.gitbook/assets/ELI5_GetStart_Download_S03-01.png" alt=""><figcaption></figcaption></figure>
*   [Nightly Release](https://github.com/WolvenKit/WolvenKit-nightly-releases/releases/latest)

    <figure><img src="../../.gitbook/assets/ELI5_GetStart_Download_S03-02.png" alt=""><figcaption></figcaption></figure>

</details>

## Installing

WolvenKit is not technically installed, you extract the downloaded file into a folder and it runs as a [portable application](https://en.wikipedia.org/wiki/Portable_application). When you update the application, you'll overwrite the existing files with those that you've newly downloaded — you don't need to delete the old files, unless you run into weird problems.&#x20;

Your settings are saved in `C:\Users\yourUserName\AppData\Roaming\REDModding\WolvenKit.`

{% hint style="info" %}
This guide assumes that you install Wolvenkit and Wolvenkit Console to the following folders:

* Wolvenkit: `C:\Cyberpunk2077Mod\Wolvenkit`
* Wolvenkit Console (optional): `C:\Cyberpunk2077Mod\Wolvenkit.CLI`

You can use other paths, the guide just assumes that you don't.
{% endhint %}



<details>

<summary>Making your Cyberpunk2077Mod folder &#x26; Extracting your WolvenKit.zip file</summary>

You can manually make your `Cyberpunk2077Mod` folder in the root of your C: drive by:

1.  Right-clicking your C: drive, Click 'New Folder'\
    \- On Windows 11 you'll have to click 'Show More Options' at the bottom of the list 🙄\


    <figure><img src="../../.gitbook/assets/01.png" alt=""><figcaption></figcaption></figure>

2)  Type or Paste in Cyberpunk2077Mod & press Enter\
    \- You may see the Folder populate within another Directory Folder, this should self-resolve after pressing Enter

    <figure><img src="../../.gitbook/assets/02.png" alt=""><figcaption></figcaption></figure>
3)  From, presumably, your Downloads Folder, drag & drop your wolvenkit.zip file into C:\Cyberpunk2077Mod\


    <figure><img src="../../.gitbook/assets/06 (1).png" alt=""><figcaption></figcaption></figure>


4)  With WolvenKit.zip selected, either right click to Extract All or Click the Extract All Button in File Explorer to begin Extracting\


    <figure><img src="../../.gitbook/assets/05.png" alt=""><figcaption><p>All Done!</p></figcaption></figure>

</details>

### TLDR;

1. Download the new release, extract the files (over your old install if you have one) and run it.&#x20;
2. Optional: Proceed to the [full configuration instructions](../eli5-getting-started/configure-modding-tools.md).
3. Troubleshooting: Delete everything in the install folder, then re-extract the downloaded files again.&#x20;
4. More troubleshooting: Find us on [Discord](https://discord.com/channels/717692382849663036/808086068023918603) in the [#wolvenkit-help-me](https://discord.com/channels/717692382849663036/808086068023918603) channel.

### Optional: Removing old versions

If you don't have any old versions installed, you can proceed to the next section.

1.  Delete all the files in `C:\Cyberpunk2077Mod\WolvenKit` from the previous release so that any cached and orphaned files do not corrupt the updated release.

    <figure><img src="../../.gitbook/assets/ELI5_GetStart_Download_S01.png" alt=""><figcaption></figcaption></figure>
2.  Delete all the files in `C:\Cyberpunk2077Mod\WolvenKit.CLI` from the previous release so that any cached and orphaned files do not corrupt the updated release.

    <figure><img src="../../.gitbook/assets/ELI5_GetStart_Download_S02.png" alt=""><figcaption></figcaption></figure>

### Extracting the downloaded files

#### Regular Wolvenkit

Extract the zip file [Wolvenkit-X.X.X.zip](./#detailed-download-instructions-with-screenshots) to `C:\Cyberpunk2077Mod\WolvenKit.`

<figure><img src="../../.gitbook/assets/ELI5_GetStart_Download_S04.png" alt=""><figcaption></figcaption></figure>

#### Optional: Wolvenkit Console

Unpack the zip file [Wolvenkit.Console-X.X.X.zip ](./#detailed-download-instructions-with-screenshots)to`C:\Cyberpunk2077Mod\WolvenKit.CLI`.

<figure><img src="../../.gitbook/assets/ELI5_GetStart_Download_S05.png" alt=""><figcaption></figcaption></figure>

### Optional: Creating a shortcut

If you want to launch Wolvenkit without browsing to the folder every time, you can create a custom shortcut and pin it to the start menu.

1. Go to `C:\Cyberpunk2077Mod\WolvenKit`
2. Right-click the executable `WolvenKit.exe`
3. Select "Create Shortcut"
4.  You should now see something like this:

    <figure><img src="../../.gitbook/assets/ELI5_GetStart_Download_S06.png" alt=""><figcaption></figcaption></figure>


5. Click "OK"
6. Right-click on your shortcut again and select "Pin to Start Menu"
7. That's it! You can launch now!

## First Launch - TL;DR

{% hint style="info" %}
For full instructions on how to configure Wolvenkit, please see the [detailed guide](../eli5-getting-started/configure-modding-tools.md).

For a more detailed explanation of the options below, please see the [corresponding wiki page](../../wolvenkit-app/settings.md#settings-explained). You can change them at any time by going to [Wolvenkit Home](../../wolvenkit-app/home/) and opening the [settings page](../../wolvenkit-app/settings.md).&#x20;
{% endhint %}

When launching WolvenKit for the first time you will be greeted with a welcome form asking to set your preferences.

We recommend setting the path to your game files immediately.&#x20;

![](<../../.gitbook/assets/8.5.3 FirstSetup generic.png>)

The **Game Executable Path** **(.exe)** is the file path or location of the Cyberpunk2077.exe file. This can be set by manually entering a file path, or using the folder icon to open Windows Explorer.&#x20;

The **Depot Path** is where WolvenKit will keep extracted Cyberpunk assets and files that are required for regular operation.
