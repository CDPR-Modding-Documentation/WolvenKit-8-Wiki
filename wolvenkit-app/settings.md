# Settings

![](<../.gitbook/assets/8.5.3 Settings generic.png>)

## Cyberpunk 2077

### Show File Preview

Enables interactive Quick Previews within the Properties panel. Toggle off for improved performance when navigating the Asset Browser and Project Explorer.

### **Game Executable (.exe) Path**

The **Game Executable (.exe) Path** is the location of the Cyberpunk2077.exe file. The .exe can be located by finding the Cyberpunk installation and navigating to the `Cyberpunk 2077\bin\x64\` folder. The path can be set by manually entering a file path, or using the folder icon to browse system files for the preferred Cyberpunk directory. As a reminder, if Cyberpunk is installed within Program Files we recommend running WolvenKit as administrator.

### Depot Path

The **Depot Path** is a WolvenKit system folder for caching game assets. WolvenKit can optionally unbundle all Cyberpunk archives to this directory. Additionally this folder is used as a cache for mesh exports with materials. WolvenKit builds a repository of visual assets within the Depot for usage with external applications such as Blender. Learn more about the [**Material exports here**](editor/import-export/blender-integration.md)**.**\
\
The Depot Path is set by default to `.../User/AppData/Roaming/REDModding/WolvenKit/MaterialDepot`, however any custom folder can be substituted. The Depot can be in excess of 30 gigabytes with materials, so we recommend a destination with ample free disk space.&#x20;

## File Editor

### Group Large Collections

Toggles limited collections for improved performance within the File Editor when working when navigating large files.

### Group Size

Adjusts the amount of elements of in a limited collection within the File Editor.

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
