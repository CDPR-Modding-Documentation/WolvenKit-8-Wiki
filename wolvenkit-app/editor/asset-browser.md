---
description: Live archive explorer
---

# Asset Browser

{% hint style="info" %}
Starting with 8.5, you will no longer need to open a mod project to load the Asset Browser. You're still required to open a mod project if you want to add anything from it.
{% endhint %}

## What is the Asset Browser?

The Asset Browser is used to navigate, search and filter Cyberpunk 2077 game files so you can transfer these to the [**Project Explorer.**](project-explorer.md) The Asset Browser virtually eliminates the need for uncooking the entire game installation, as individual files can be pulled directly from archive files.

## Using the Asset Browser

### Navigation

![](../../.gitbook/assets/8.4.3\_AssetBrowser\_generic.png)

The left-side breadcrumb navigator can be used to quickly navigate through game directories. Game files are displayed in the right-side panel, in addition to folders. Folders in the file list can also be navigated by double-clicking.

{% hint style="warning" %}
The breadcrumb search bar (bottom-left) is intended for folder searching. However using folder search will typically freeze the Asset Browser. We recommend avoiding this feature for now... Sorry!
{% endhint %}

### Search

The Asset Browser offers powerful search and filter options. The left-side search bar can be used to search for any game file. WolvenKit will search through **all** available game files. For example, `judy kind:xbm` can be used to search for all XBM files containing the word judy. The right-side search bar is for advanced RegEx (regular expressions) style searches.

### Adding files to projects

* **Double-click files** _to add them directly to the_ **Project Explorer**
* **To select multiple files** hold shift and then left click two separate files. These two files and all files between them will be selected. Right-click any of the highlighted files to open the context menu. Then choose **Add Selected Item(s) to Project.**

{% hint style="info" %}
Files added to the Project Explorer with the Asset Browser will not include external buffer files. Buffers are stored within the main file.
{% endhint %}



