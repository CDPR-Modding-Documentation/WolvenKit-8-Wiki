# Project Explorer

## What is the Project Explorer?

The Project Explorer is primarily a tool for organizing and navigating mod project files. The Project Explorer gives a constant tree view of all mod project files which streamlines the modding workflow significantly. There are four main **WolvenKit directories** inside the Project Explorer.&#x20;

### Project Explorer Tabs

You can switch between different tabs at the top of the project explorer (see the red arrow on the screenshot below). Their function (and content) will be explained in the next sections.

<figure><img src="../../.gitbook/assets/wkit_project_explorer.png" alt=""><figcaption><p>As of 8.11</p></figcaption></figure>

###

### Archive

**Location:** `your_wolvenkit_project/source/archive`

This directory contains game files in the REDengine [**CR2W**](../../help/glossary.md#cr-2-w) format, which you can add via [**Asset Browser**](asset-browser.md)**.**&#x20;

Everything in this folder will be packed into your mod's .archive file.

### Raw

**Location:** `your_wolvenkit_project/source/raw`

This is your working directory. Keep any files here that you don't want to end up on Nexus.

When you [export files](../usage/import-export/) via Wolvenkit, the exports will be placed in a [mirrored folder structure](../usage/import-export/#file-structure-the-raw-folder).

### Resources

**Location:** `your_wolvenkit_project/source/resources`

This folder contains other files for your mod. Any of its contents will be [packed](../menu/toolbar.md#pack-mod) so that they extract directly into the Cyberpunk directory. For that reason, you (or Wolvenkit) should create the following subdirectories:



|                                                                                                                                     |                                                        |
| ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| script (.reds, [RedScript](http://127.0.0.1:5000/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators/references-lists-and-overviews/scripting)) | r6/scripts                                             |
| tweaks (.yaml, [TweakXL](http://127.0.0.1:5000/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators/core-mods-explained/archivexl))              | r6/tweaks                                              |
| CET (.lua, [Cyber Engine Tweaks](https://wiki.redmodding.org/cyber-engine-tweaks/))                                                 | `bin/x64/plugins/cyber_engine/tweaks/mod/your_mod_dir` |

### Source

**Location:** `your_wolvenkit_project/source`

Will show you everything. No context sorting.

## Using the Project Explorer

WolvenKit features a bespoke [**File Editor**](file-editor.md) which is capable of opening and modifying any REDengine file. Double-click any file within the archive directory of the Project Explorer to open the document viewer.\
\
Non-REDengine files which are typically stored in the _raw directory_ can be accessed with the Project Explorer as well. Files such as blend, psd, png, and many more can be opened with the preferred system application. For example, double-clicking a .tga file will open the file with the users system preferred image application.

Any file within the Project Explorer can be moved by dragging and dropping. Additionally files can be copied by holding _Control_ while dragging and dropping.

### Context Menu

Right-click any file within the Project Explorer to explore the Context Menu.

![](<../../.gitbook/assets/8.5.3 ProjectExplorer ContextMenu.png>)

#### Open in MLSetupBuilder

Requires MLSetupBuilder plugin for WolvenKit. Install by navigating to the [**View Options**](broken-reference) Toolbar panel.

#### Export to JSON/Import to JSON

Writes any REDengine file within the _archive directory_ to human readable JSON format, as a mirrored file within the _raw directory_. JSON files can then be modified and converted back to REDengine format from the context menu by right-clicking the JSON file.

#### Delete

Moves any project file to the OS/system Recycle Bin.

#### Rename

Opens a dialogue box which allows any project file to be renamed.

#### Copy

Select any project file to be copied.

#### Paste

Pastes copied project file.

#### Copy relative path

Copies the selected file path to OS/system clipboard, trimming off all folders outside the game directory. Extremely useful for modifying paths while using the File Editor.&#x20;

#### Replace with original

Replaces the selected file with the original unmodified version from the game archives. (archive directory only)

#### Open in File Explorer

Find the selected file with the OS/system file explorer.

### Filtering

The Project Explorer can be filtered by directory.

**SOURCE** |  All project directories (default)\
&#x20;   **archive**  |  Archive directory\
&#x20;   **raw** |  Raw directory\
&#x20;  **scripts** |  Script directory\
&#x20;   **tweaks**  |  Tweaks directory\
**PACKED**  |  Internal WolvenKit folder for mod deployment. Can be used to install extra files.\
\
Additionally the rightmost hamburger-style button can be used to toggle a flat file list without folders.
