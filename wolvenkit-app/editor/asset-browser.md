---
description: Live archive explorer
---

# Asset Browser

## What is the Asset Browser?

The Asset Browser is used to navigate, search and filter Cyberpunk 2077 game files so you can transfer these to the [**Project Explorer.**](project-explorer.md) The Asset Browser eliminates the need for uncooking the entire game installation, as individual files can be pulled directly from archive files.

## Where is it?

In the default view (as of 8.11), you will find it pinned to the right side of the viewport.

If it isn't there, check the **View** menu and make sure that it's enabled.

## Using the Asset Browser

{% hint style="info" %}
Wolvenkit Search has its own sub-page: [wolvenkit-search-finding-files.md](../usage/wolvenkit-search-finding-files.md "mention")
{% endhint %}

### Navigation

![](<../../.gitbook/assets/8.5 Asset Browser.png>)

The left-side breadcrumb navigator can be used to quickly navigate through game directories. Game files are displayed in the right-side panel, in addition to folders. Folders in the file list can also be navigated by double-clicking.

### Mod Browser

You can switch the Asset Browser to Mod Browsing mode via button. The [search](asset-browser.md#search) will no longer consider base game files and search in your loaded .archives instead.

Wolvenkit will search any installed mods and anything under the [#additional-mod-directory](../settings.md#additional-mod-directory "mention"). There is no way to browse an `.archive` file in a different folder — if you insist on doing that, check [Legacy: Analysing other mods with Wolvenkit Console](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/modding-guides/analysing-other-mods/legacy-analysing-other-mods-with-wolvenkit-console "mention").

<figure><img src="../../.gitbook/assets/asset_browser_mod_browser (1).png" alt=""><figcaption></figcaption></figure>

### Adding files to projects

* **Double-click files** _to add them directly to the_ **Project Explorer**
* **To select multiple files** hold shift and then left click two separate files. These two files and all files between them will be selected. Right-click any of the highlighted files to open the context menu. Then choose **Add Selected Item(s) to Project.**

{% hint style="info" %}
Files added to the Project Explorer with the Asset Browser will not include external buffer files. Buffers are stored within the main file.
{% endhint %}

### Context Menu

As of 8.11.1, the context menu has the following entries:

#### Add selected items to project

See [#adding-files-to-projects](asset-browser.md#adding-files-to-projects "mention") above

#### Open without adding to project

What it says — you can browse a file in the [file-editor](file-editor/ "mention") without adding it to your project. Saving (Hotkey: `Ctrl+S`) lets you save it to disk, though.

#### Find used files

{% hint style="info" %}
Requires the [#wolvenkit-resources](../home/home-plugins.md#wolvenkit-resources "mention") plugin to be installed.
{% endhint %}

Will make the Asset Browser display a list of everything your current file is linking to.

#### Find files using this

{% hint style="info" %}
Requires the [#wolvenkit-resources](../home/home-plugins.md#wolvenkit-resources "mention") plugin to be installed.
{% endhint %}

Like [#find-used-files](asset-browser.md#find-used-files "mention"), but the opposite: will make the Asset Browser display a list of everything that links to your current file.

#### Browse to asset folder

Will navigate the asset browser to the current selection's path in the game files (if it is a game file).

#### Copy Relative Path

Copies the selection's relative path to clipboard.&#x20;
