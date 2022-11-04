---
description: Configuring WolvenKit for modding
---

# Setup

## First Launch

When launching WolvenKit for the first time you will be greeted with a welcome form asking to set your preferences. We recommend setting the path to your game files immediately. If you should close this form, you can access the same [**Settings**](../wolvenkit-app/settings.md) at any time through the Home page.

![](<../.gitbook/assets/8.5.3 FirstSetup generic.png>)

The **Game Executable Path** **(.exe)** is the file path or location of the Cyberpunk2077.exe file. This can be set by manually entering a file path, or using the folder icon to browse system files for the preferred Cyberpunk installation. As a reminder, if Cyberpunk is installed within Program Files we recommend running WolvenKit as administrator.

{% hint style="info" %}
Can't find Cyberpunk2077.exe? Try the default locations listed below:\
\
**STEAM**\
`C:\Program Files (x86)\Steam\steamapps\common\Cyberpunk 2077\bin\x64`\
``\
``**`GOG`**\
`C:\Program Files (x86)\GOG Galaxy\Games\Cyberpunk 2077\bin\x64`
{% endhint %}

The **Depot Path** is a WolvenKit system folder for creating a cache of textures and other Cyberpunk assets. The Depot Path is set by default to `.../AppData/Roaming/REDModding/WolvenKit/MaterialDepot`, however any custom folder can be substituted. A Depot with materials can be in excess of 30 gigabytes, so we recommend a destination with ample free disk space.

{% hint style="danger" %}
Be sure to set the Game Executable Path! Functionality is extremely diminished if WolvenKit cannot properly locate your game installation.
{% endhint %}

## Using WolvenKit

Creating a new mod project is necessary to begin using most WolvenKit features. A new project can be created from the [**Home**](../wolvenkit-app/home.md#welcome) page or the [**Toolbar**](broken-reference). If you're new to WolvenKit, we strongly recommend reading the next wiki section, [**Creating a Mod**](creating-a-mod.md).
