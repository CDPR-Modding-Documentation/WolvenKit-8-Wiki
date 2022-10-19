# Project Explorer

## What is the Project Explorer?

The Project Explorer is primarily a tool for organizing and navigating mod project files. The Project Explorer gives a constant tree view of all mod project files which streamlines the modding workflow significantly. There are four main **WolvenKit directories** inside the Project Explorer.&#x20;

* The _**archive** directory_ contains REDengine [**CR2W**](../../help/glossary.md#cr-2-w) files. Files added to the mod project with the [**Asset Browser**](asset-browser.md) will automatically be organized here. Files within the archive directory are packed into the archive when building a mod project.
* The _**raw** directory_ contains source assets such as models and textures. These files will not be included in the packed mod project, however they are extremely valuable to have nearby with the WolvenKit content pipeline.
* The _**scripts** directory_ can be used to organize and pack redscript files.
* The _**tweaks** directory_ can be used to organize and pack tweakdb files.

![](<../../.gitbook/assets/8.5.3 ProjectExplorer generic.png>)

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
