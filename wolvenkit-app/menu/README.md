# Menu

## What is the Menu?

The Menu is the main navigation bar at the top of the WolvenKit application. The Menu contains key functionality such as saving, opening files, and building mods. Read below for details about each Menu button. The Menu also displays the current mod project name and file opened with WolvenKit.

### Toolbar

The [#toolbar](./#toolbar "mention") is available directly below the Menu from the Editor. The buttons add convenience shortcuts to certain menu functions.

Additionally, the Toolbar contains the **Launch Profiles** button.

<figure><img src="../../.gitbook/assets/WK 8.7 Menu and Toolbar Generic.png" alt=""><figcaption></figcaption></figure>

## HOME

Shows the WolvenKit [**Home**](../home/) view

## File

### New File

Opens the dialogue to create a new file.&#x20;

### Save

Save the currently selected document from the File Viewer

### Save As&#x20;

Save the currently selected document from the File Viewer as a new file

### Save All

Save all currently open documents from the File Viewer

## Project

### New Project

Create a new WolvenKit mod project

### Open Project

Open an existing WolvenKit mod project

### Project Configuration

Configure various project settings

### Scan project for broken references

This will go through every file in your project, checking if **referenced resources** are **in your project** or **part of the base game**.&#x20;

If you are using a texture library, you will obviously get false positives here.

### Scan for unused files

The opposite of "Scan project for broken references" — this will check every file in your project and check if it's used by something.&#x20;

Will give you a list that you can copy to clipboard, or options to move/delete the files.

{% hint style="danger" %}
This feature is experimental, so handle with care!
{% endhint %}

### Delete empty folders

Will yeet folders without files in them. Works recursively (will also delete empty folder trees).

### Run File Validation on entire project

Will run the [Wolvenkit File Validation](../file-validation.md) on every file in your project, and open the log file afterwards. \
This will generate a lot of duplicate text, but is the best way to find mistakes.

## Build

### Pack Project

Generates the install-ready structure in your project's `packed` folder, then creates a zip file.&#x20;

{% hint style="info" %}
The generated zip file is ready for Nexus upload!
{% endhint %}

### Pack as REDmod

Generates the install-ready structure (REDmod format) in your project's `packed` folder, then creates a zip file.&#x20;

{% hint style="info" %}
This option is hidden by default and can be turned on in the [#settings](./#settings "mention"). Read [here](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-users/users-modding-cyberpunk-2077/redmod/usage#why-would-i-want-this) why.&#x20;
{% endhint %}

### Install

Runs [#pack-project](./#pack-project "mention"), then copies the contents of `packed` to your game directory.\
You can learn about [Archive files Load Order](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-users/users-modding-cyberpunk-2077/load-order "mention") on the yellow wiki.

### Install as REDmod

Runs [#pack-as-redmod](./#pack-as-redmod "mention"), then copies the contents of `packed` to your game directory.

{% hint style="info" %}
This option is hidden by default and can be turned on in the [#settings](./#settings "mention"). Read [here](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-users/users-modding-cyberpunk-2077/redmod/usage#why-would-i-want-this) why.&#x20;
{% endhint %}

### Install & Launch Game

Runs [#install](./#install "mention"), then launches the game for you

### Install as REDmod & Launch Game

Runs [#install-as-redmod](./#install-as-redmod "mention"), then launches the game for you

{% hint style="info" %}
This option is hidden by default and can be turned on in the [#settings](./#settings "mention"). Read [here](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-users/users-modding-cyberpunk-2077/redmod/usage#why-would-i-want-this) why.&#x20;
{% endhint %}

### Clean All

Deletes the contents of your Wolvenkit project's `packed` directory.

### Hot Reload

Pack archives and instantly install to game directory while Cyberpunk 2077 is running for testing (Requires [RedHotTools](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators-theory/modding-tools/redhottools "mention")).

### Launch Profiles

Create and modify one-click pack & launch operations

## View

### Project Explorer

Toggles the [#project-explorer](./#project-explorer "mention") on or off

### Asset Browser

Toggles the [#asset-browser](./#asset-browser "mention") on or off

### Properties

Toggles the [properties.md](../editor/properties.md "mention") panel for your currently selected file  or off

### Log

Toggles the [log.md](../editor/log.md "mention") panel on or off.

### Tweak Browser

Toggles the **Tweak Browser** on or off. This panel will let you browse the TweakDB.

### LocKey browser

Toggles the LocKey browser on or off. This panel will let you browse translation strings.

### Show File Preview

Same as [**Settings**](../settings.md#show-file-preview) option - enables/disables interactive Quick Previews within the Properties panel.&#x20;

{% hint style="info" %}
This feature impacts performance. Navigating the Asset Browser or Project Explorer will be **faster** if the preview is **toggled off** or **inactive**.
{% endhint %}

### Layout

#### Save Layout to Project

Saves the [**Editor**](../editor/) UI layout to the current WolvenKit project, making it persistent across sessions.

If you do this without an open Wolvenkit project, the view will be saved to the default file `%USERPROFILE%\AppData\Roaming\REDModding\WolvenKit\DockStates.xml`

#### Reset Layout

Resets the UI layout to the default from one of the following files (by priority):

1. `%USERPROFILE%\AppData\Roaming\REDModding\WolvenKit\DockStates.xml`
2. `Path\To\Wolvenkit\DockStatesDefault.xml`

This can be especially helpful if the layout is bugged or an editor window is unrecoverable.

## Tools

### Depot Generator

Tool for building a `depot`, a collection of extracted game assets to use them in other tools.\
[**Read more**](../tools/#depot-generator)

### Sound Modding Tool

Tool for modding sound files\
[**Read more**](../tools/#sound-modding-tool)

### **Script Manager**

Toggles the [#script-manager](./#script-manager "mention")

### Import Tool

Toggles the [#import-tool](../tools/tools-import-export.md#import-tool "mention")

### Export Tool

Toggles the [#export-tool](../tools/tools-import-export.md#export-tool "mention")

### Settings

Open the WolvenKit [**Settings**](../settings.md) page

## Game

### Launch Game

Launches Cyberpunk 2077

### Launch Game with Steam

Launches Cyberpunk 2077 using Steam

### Open Game Folder

Opens the Cyberpunk 2077 game directory in Windows Explorer

## Extensions

### Plugin Manager

Opens the WolvenKit Plugin Manager

#### Mod Manager

Opens the WolvenKit Plugin Manager

#### Cyberpunk Blender Add-on

Opens external-link to the Cyberpunk Blender Add-on GitHub page\
[https://github.com/WolvenKit/Cyberpunk-Blender-add-on](https://github.com/WolvenKit/Cyberpunk-Blender-add-on)

## Help

### Setting Up WolvenKit

Opens an external-link to the [**Setup**](broken-reference) page

### Creating a Mod

Opens an external-link to the [**Creating a Mod**](../../getting-started/creating-a-mod.md) page

#### Discord Invitation

### Opens an external-link to a [Discord](https://discord.gg/Epkq79kd96) invitation

### About WolvenKit

Opens an external-link to the [**About**](../../about.md) page

### Open Log Folder

Opens the folder with the Wolvenkit Logs
