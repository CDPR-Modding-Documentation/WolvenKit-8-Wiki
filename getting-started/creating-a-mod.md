---
description: With great power comes great responsibility
---

# Creating a Mod

## Before we get started

**Congratulations on installing WolvenKit!** We're going to create an example project to help get you up to speed with WolvenKit's features and workflows. We'll walk through creating a basic mod step-by-step, while explaining how to get the best out of WolvenKit. Lastly keep in mind that understanding and modding Cyberpunk 2077 can be _very challenging_. If you're feeling stuck, please consider reaching out to fellow modders and the development team on our [**Discord server.**](../help/community.md) Now without further adieu...

{% hint style="info" %}
What can WolvenKit do? Check out the [**Overview**](../features/overview.md) page to learn more about WolvenKit's features. Have some more questions before getting started? Try the [**FAQ!**](../help/faq.md)****
{% endhint %}

## Creating a texture replacement mod

### Summary

WolvenKit is a tool for mod developers to interact with REDengine file formats. Generally speaking most mods created with WolvenKit share a similar workflow:

1. Browse and extract game files\

2. Convert game files to common formats that can be modified\

3. Modify the file, often with an external application\

4. Convert the common format file back to game format\

5. Build a mod package including the newly modified files\


In the guide below we'll cover these steps in detail to replace an image in Cyberpunk.

## Getting Started with WolvenKit

### Starting a project

1.  Ensure WolvenKit is properly configured by following the **** [**Setup**](setup.md) procedure


2.  Create a new WolvenKit mod project


3.  Configure the Editor using [**docking**](../wolvenkit-app/editor/#docking). Within the [**Toolbar**](../wolvenkit-app/editor/toolbar.md), use the [**View Options**](../wolvenkit-app/editor/toolbar.md#view-options) panel to ensure that the Asset Browser, Project Explorer, Import/Export, Properties, and Log windows are visible.


4. Navigate to the Asset Browser window

### Asset Browser

The Asset Browser is the most fundamental WolvenKit tool. It allows us to browse any archive and add individual files to a local mod project. Any files added from the Asset Browser will be added to the **archive directory** with their folder structure intact. Files added with the Asset Browser can be viewed, studied, modified, and packed as a modded archive.

1.  Use the "breadcrumb" style navigator in the left-hand side of the Asset Browser to quickly navigate folders


2.  Navigate to the following path:

    `base/characters/common/textures/tattoos`


3.  Use the main file list panel inside the Asset Browser to preview individual files. The XBM file extension always represents a texture file within REDengine. WolvenKit is capable of instantly previewing texture and model files. The Properties window responds automatically to selections within the Asset Browser. Feel free to experiment by selecting a few textures.


4.  For this guide we'll be using `tattoo_casual_d07.xbm`, but feel free to choose another if you're feeling adventurous. To verify this texture mod in game, you will need a game save with Judy available in-person. Beware depending on the texture you choose, you may experience some difficulty when it comes time to verify that the final modded archive works successfully.


5.  Select  `tattoo_casual_d07.xbm` by left-clicking or using the check box. The check boxes are useful for more extensive projects when adding multiple files.


6. Add the texture to your project by double-clicking directly on the file

### Projects

Mod Projects are the core of WolvenKit functionality. Projects are primarily used to separate and organize source and game files into distinct self-contained mods. Each project can be thought of as the source code for any given mod.\
\
The [**Project Explorer**](../wolvenkit-app/editor/project-explorer.md) is the central component for each mod project. Project files are separated into two main system directories:\
****\
****The **archive** directory is for REDengine/Cyberpunk format files.\
\
The **raw** directory is for non-REDengine/generic format source files.\
\
These are core directories for WolvenKit's file operations. These folders are never exposed to the game inside the [**packed mod**](../help/glossary.md#packed).

1.  (Optional) Navigate to the [**Project Explorer**](../wolvenkit-app/editor/project-explorer.md) window to examine the new file added to the archive directory. The preview functionality of the Properties window also works for local project files. Many REDengine assets and common image files (png, tga, etc.) can be automatically previewed by selecting them within the Project Explorer.


2. (Optional) Files within the Project Explorer have additional options when right-clicked. Directly right-click any file to open the [**Context Menu**](../wolvenkit-app/editor/project-explorer.md#context-menu).

### Exporting REDengine Files

WolvenKit features a bespoke tool for conversions between REDengine and non-REDengine formats, _creatively_ named [**Import/Export**](../wolvenkit-app/editor/import-export/). The Import/Export tool is extremely robust, featuring advanced options and batch functionality.

The **archive** and **raw** directories within the **Project Explorer** behave as a mirror to one another; REDengine files are always stored in the _archive directory_, and the analogous "generic" format file will be stored in the _raw directory_ with the same folder structure. Import and export destinations _never_ need to be specified enabling ultra-fast file I/O, with the added benefit of automatically-organized Raw files.

1.  Navigate to the [**Import/Export**](../wolvenkit-app/editor/import-export/) window, then ensure the **Export** toggle is selected


2.  Double-click the `tattoo_casual_d07.xbm` file within the Export grid to view advanced options. Any asset within the Import/Export grid can be doubled clicked to adjust advanced I/O options for each file format.


3.  Inspect the **XBM Export Type** drop down menu, in this case we want to export the texture as a **TGA**


4.  Press the **Confirm** button to proceed. For batch exports, using the checkbox for **Apply to all files of the same extension** will ensure that any XBM _currently_ within the Import/Export grid will inherit the same advanced options.


5. Press **Process Selected** to complete the export operation. A new TGA image will now be available within the **Project Explorer Raw directory**.

{% hint style="info" %}
Cyberpunk textures appear to be upside-down. This is **not a bug** or issue with WolvenKit, nearly all textures are inverted. The Import/Export tool is capable of inverting processed textures during Import and Export.
{% endhint %}

### Editing Textures

While this guide is step-by-step, it's counter-productive for the WolvenKit team to guide users on using other software. We can recommend free tools such as [Krita](https://krita.org), [Paint.net](https://getpaint.net/), or [Gimp](https://gimp.org/) for editing TGA format textures. If you're not familiar with image editing software, we recommend learning how to use creative software from experts in those fields. YouTube is an excellent resource for learning the basics of most applications.

1.  Import the `tattoo_casual_d07.tga` texture file to an image editing software of your choice


2.  Make a _distinct and recognizable_ change to the image


3. Export the `tattoo_casual_d07.tga` texture file as a **TGA**, overwriting the original TGA file

### Importing REDengine Files

1.  Return to the WolvenKit Editor


2.  Navigate to the [**Import/Export**](../wolvenkit-app/editor/import-export/) window, then ensure the **Import** toggle is selected


3. Select the `tattoo_casual_d07.tga` file within the Import grid. Double-click the TGA file within the Import grid to access advanced options.\

4.  Within the advanced options, check the **isGamma** box. This step is necessary for all _color textures_ (such as d/diffuse) to display as sRGB. Without **isGamma** checked color textures will appear bright and washed out. Press **Confirm** to proceed.


5.  Press **Process Selected** to complete the Import operation


6. Verify the updated texture by selecting the XBM within the Project Explorer. The new texture should be viewable with the Properties window.&#x20;

{% hint style="warning" %}
Custom TGA files may appear upside down within the file previewer! There is a known visual issue with WolvenKit. The imported XBM file preview will be correct.
{% endhint %}

### Building

WolvenKit features a one-click mod building solution. The build process packs any **archive directory** files into archive format and installs to the game automatically.

WolvenKit only supports **unbundled** files. Files that have been decompressed using WolvenKit CLI _will not_ be packed correctly. Buffers must be compressed within the main REDengine file. Files added with the built-in Asset Browser will **always** be the correct format.

1.  From within the [**Toolbar**](../wolvenkit-app/editor/toolbar.md), select the [**Pack & Install**](../wolvenkit-app/editor/toolbar.md#pack-and-install) button


2.  Verify the mod project has been packed and installed by viewing the [**Log**](../wolvenkit-app/editor/log.md) window


3. Congratulations! Launch Cyberpunk and check out your first mod with WolvenKit!

## Final Thoughts

While not all encompassing, this guide teaches the core philosophy behind our modding pipeline. If you've followed along so far, you're ready to start getting the most out of WolvenKit. We recommend familiarizing yourself with the Wiki to understand how our Editors work. Please keep in mind that everything in our community from software such as WolvenKit or this Wiki is developed, written, and created by passionate volunteers. If you encounter issues with software or documentation, consider getting involved with us on the [Discord server!](https://discord.com/invite/Epkq79kd96)



Enjoy your RED Modding journey!

