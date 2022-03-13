---
description: With great power comes great responsibility
---

# Creating a Mod

## Before we get started

**Congratulations on installing WolvenKit!** We're going to create an example project to help get you up to speed with WolvenKit's features and workflows. We'll walk through creating a basic mod step-by-step, while explaining how to get the best out of WolvenKit. Lastly keep in mind that understanding and modding Cyberpunk 2077 (which is built on CDProjekt’s REDengine 4 game engine can be _very challenging)_. If you're feeling stuck, please consider reaching out to fellow modders and the development team on our [**Discord server.**](../help/community.md) Now without further adieu...

## How WolvenKit fits in to the modding workflow

### Essentials

When modding Cyberpunk 2077, WolvenKit helps with:

* Browsing game files, and helping you bring these into project folders that it helps you set up to organise the content you are modding
* Exporting these [W2RC](../help/glossary.md) RedEngine format game files into formats that can be read and edited by other apps
* Reimporting and converting these edited files back into the RedEngine format
* Packing and installing/copying these files to the correct part of the game folder

### Game entities

When modding, you will need to get your head around fhe following W2RC files:

* .ent files are entity files and equivalent to game objects and are what can be spawned within game. They link in various basic logic and rules that govern that object. They will either link .mesh files in directly for simple objects, or specify a list of appearance variations to call from a dedicated .app file. Note: For characters you should mod the .ent files in the quest subfolder
* .app files hold the different configuration of appearances that can be switched for more complex game entities such as characters or vehicles. These files then directly link in the relevant .mesh geometry, .rig files and .anim animation files for each appearance.&#x20;
* .mesh files are the actual 3d objects that hold the geometry but also hold a list of materials to use for different appearances requested of that mesh in game, which are embedded within compressed buffers within the .mesh file itself.&#x20;

### Materials

Materials are fairly complex in the way they are organised. The key thing is that materials are often embedded within compressed buffers inside the .mesh files. However, they can be and are sometimes referenced as external files with some simpler game objects.

Wkit can't edit these material buffers yet, a feature which is in advanced development for v8.6. In the meantime, you can export the .mesh using the WithMaterials option to get a json file which lists the material assignments. You can edit this file in an external text/script editor, then use the import option to bring the material assignments back into the .mesh file.

* .mt files are material templates that are the lowest level of abstraction and the source for material files.&#x20;
* .mi material instance files instantiate different settings based  on a .mt material template file to describe single-layer materials

One of the .mt files is the multilayered.mt, which is used a lot by characters and vehicles as the core template for multilayered complex materials. Back in the .mesh file, they are referenced within the mesh material buffers as follows:

* .multilayered.mt as the base template
* .mlsetup files to describe the kinds of .mi material assigned to each layer for this instance of the .multilayered.mt
* .mlmask files which combine internally a set of grayscale textures which describes which layer is used by which part of the mesh
* .xbm files hold textures



## Creating a texture replacement mod

### Starting a project

1.  Ensure WolvenKit is properly configured by following the **** [**Setup**](setup.md) procedure


2.  Create a new WolvenKit mod project


3.  (Optional) Configure the Editor to suit your needs using docking


4. Navigate to the Asset Browser window

### Asset Browser

The Asset Browser is the most fundamental WolvenKit tool. It allows us to browse any archive and add individual files to a local mod project. Any files added from the Asset Browser will be added to the **Mod directory** with their folder structure intact. Files added with the Asset Browser can be viewed, studied, modified, and packed as a modded archive.

1.  Use the "breadcrumb" style navigator in the left-hand side of the Asset Browser to quickly navigate folders


2.  Navigate to the following path:

    `Archive/base/characters/common/textures/tattoos`


3.  Use the main file list panel inside the Asset Browser to preview individual files. The XBM file extension always represents a texture file within REDengine. WolvenKit is capable of instantly previewing texture and model files. The Properties window responds automatically to selections within the Asset Browser. Feel free to experiment by selecting a few textures.


4.  For this guide we'll be using `tattoo_casual_d07.xbm`, but feel free to choose another if you're feeling adventurous. To verify this texture mod in game, you will need a game save with Judy available in-person. Beware depending on the texture you choose, you may experience some difficulty when it comes time to verify that the final modded archive works successfully.


5.  Select  `tattoo_casual_d07.xbm` by left-clicking or using the check box. The check boxes are useful for more extensive projects when adding multiple files.


6. Add the texture to your project by double-clicking directly on the file or using the **Add Selected Item(s) to Project** button from the [**Ribbon**](../wolvenkit-app/ribbon/)

### Projects

Mod Projects are the core of WolvenKit functionality. Projects are primarily used to separate and organize source and game files into distinct self-contained mods. Each project can be thought of as the source code for any given mod.\
\
The [**Project Explorer**](../wolvenkit-app/editor/project-explorer.md) is the central component for each mod project. Project files are separated into two main system directories:\
****\
****The **Mod** directory is for [**W2RC**](../help/glossary.md#cr-2-w) files.\
\
The **Raw** directory is for [**Raw**](../help/glossary.md#raw) source files.\
\
These are core directories for WolvenKit's file operations. These folders are never exposed to the game inside the [**packed mod**](../help/glossary.md#packed).

1.  (Optional) Navigate to the [**Project Explorer**](../wolvenkit-app/editor/project-explorer.md) window to examine the new file added to the Mod directory. The preview functionality of the Properties window also works for local project files. Many REDengine assets and common image files (png, tga, etc.) can be automatically previewed by selecting them within the Project Explorer.


2. (Optional) Files within the Project Explorer can be managed by right-clicking them directly. Additionally, with a file (or folder) selected, the same options become available from the [**Actions**](../wolvenkit-app/ribbon/actions.md#project-explorer-actions) section of the Ribbon.

### Exporting REDengine Files

WolvenKit features a bespoke tool for conversions between [**W2RC**](../help/glossary.md#cr-2-w) and [**Raw**](../help/glossary.md#raw) formats, _creatively_ named [**Import/Export**](../wolvenkit-app/editor/import-export/). The tool can be accessed through the [**View**](../wolvenkit-app/ribbon/view.md#editors) tab of the Ribbon. The Import/Export tool is extremely robust, featuring advanced options and batch functionality.

The **Mod** and **Raw** directories within the **Project Explorer** behave as a mirror to one another; REDengine files are always stored in the Mod directory, and the analogous "generic" format file will be stored in the Raw directory with the same folder structure. Import and export destinations _never_ need to be specified enabling ultra-fast file I/O, with the added benefit of automatically-organized Raw files.

1.  Navigate to the [**Import/Export**](../wolvenkit-app/editor/import-export/) window, then ensure the **Export** toggle is selected


2.  Double-click the `tattoo_casual_d07.xbm` file within the Export grid to view advanced options. Any asset within the Import/Export grid can be doubled clicked to adjust advanced I/O options for each file format.


3.  Inspect the **XBM Export Type** drop down menu, in this case we want to export the texture as a **TGA**


4.  Press the **Confirm** button to proceed. For batch exports, using the checkbox for **Apply to all files of the same extension** will ensure that any XBM _currently_ within the Import/Export grid will inherit the same advanced options.


5. Press **Process Selected** to complete the export operation. A new TGA image will now be available within the **Project Explorer Raw directory**.

{% hint style="info" %}
Cyberpunk textures appear to be upside-down. This is **not a bug** or issue with WolvenKit, nearly all textures are inverted. The Import/Export tool is capable of inverting processed textures during Import and Export.
{% endhint %}

### Editing Textures

While this guide is step-by-step, it's counter-productive for the WolvenKit team to guide users on using other software. We can recommend free tools such as [Krita](https://krita.org), [Paint.net](https://getpaint.net), or [Gimp](https://gimp.org) for editing TGA format textures. If you're not familiar with image editing software, we recommend learning how to use creative software from experts in those fields. YouTube is an excellent resource for learning the basics of most applications.

1.  Import the `tattoo_casual_d07.tga` texture file to an image editing software of your choice


2.  Make a _distinct and recognizable_ change to the image


3. Export the `tattoo_casual_d07.tga` texture file as a **TGA**, overwriting the original TGA file

### Importing REDengine Files

1.  Return to the WolvenKit Editor


2.  Navigate to the [**Import/Export**](../wolvenkit-app/editor/import-export/) window, then ensure the **Import** toggle is selected


3. Select the `tattoo_casual_d07.tga` file within the Import grid. Double-click the TGA file within the Import grid to access advanced options.\

4.  Within the advanced options, uncheck **Use existing file**. This ensures a successful import while using TGA with WolvenKit 8.4.3. Press **Confirm** to proceed.


5.  Press **Process Selected** to complete the Import operation


6. Verify the updated texture by selecting the XBM within the Project Explorer. The new texture should be viewable with the Properties window.&#x20;

{% hint style="warning" %}
Custom TGA files may appear upside down within the file previewer! There is a known visual issue with WolvenKit 8.4.3. The imported XBM file preview will be correct.
{% endhint %}

### File Editing

The core feature of WolvenKit is the [**File Editor**](../wolvenkit-app/editor/file-editor.md#what-is-the-file-editor). Any REDengine file can be modified and saved with the built in REDengine document viewer.

1. Double-click the `tattoo_casual_d07.xbm` file within the **Project Explorer**.\

2. Within the document view, select **CBitmapTexture.** Then use the panel on the righthand side to expand the **Setup** category.\

3. Within the Setup category press the empty checkbox for the **isGamma** property. The box should now display an X for true. This step is necessary for all **color textures** to display as sRGB. Without **isGamma** checked color textures will appear bright and washed out.

### Building

WolvenKit features a one-click mod building solution. The build process packs any **Mod directory** files into archive format and installs to the game automatically.

WolvenKit only supports **unbundled** files. Files that have been decompressed with Oodle Kraken _will not_ be packed correctly. Buffers must be compressed within the main W2RC file. Files added with the built-in Asset Browser will **always** be the correct format.

1.  From within the General section of the Ribbon, select the [**Pack Project**](../wolvenkit-app/ribbon/general.md#pack-project) button


2.  Verify the mod project has been packed and installed by viewing the [**Log**](../wolvenkit-app/editor/log.md) window


3. Congratulations! Launch Cyberpunk and check out your first mod with WolvenKit!

## Final Thoughts

While not all encompassing, this guide teaches the core philosophy behind our modding pipeline. If you've followed along so far, you're ready to start getting the most out of WolvenKit. We recommend familiarizing yourself with the Wiki to understand how our Editors and Tools work. Please keep in mind that everything in our community from software such as WolvenKit or this Wiki is developed, written, and created by passionate volunteers. If you encounter issues with software or documentation, consider getting involved with us on Discord!



Enjoy your RED Modding journey!

