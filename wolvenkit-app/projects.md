# Projects

## What is a WolvenKit project?

Mod Projects are the core of WolvenKit functionality. Projects are primarily used to separate and organize source and game files into distinct directories. Each project can be thought of as the source code for any given mod.\
\
The [**Project Explorer**](editor/project-explorer.md) is the central component for each mod project. Project files are separated into two main system directories:\
****\
****The **archive** directory is for [**W2RC**](../help/glossary.md#cr-2-w) files.\
\
The **raw** directory is for [**Raw**](../help/glossary.md#raw) source files.\
\
These are core directories for WolvenKit's file operations. These folders are never exposed to the game inside the [**packed mod.**](../help/glossary.md#packed)

## New Project

#### Creating a new WolvenKit mod project

1.  From the [**Ribbon**](ribbon/) or the [**Home**](home.md) page, click the "New Project" button to create a new project.


2.  Name the mod project


3.  Select a destination for the .modproj


4.  Click **Finish**

    ****
5. WolvenKit will now open the new project and proceed to the [**Editor**](editor/)****

## Open Project

#### Opening an existing WolvenKit mod project

1.  From the [**Ribbon**](ribbon/) or the [**Home**](home.md) page, click the "Open Project" button to create a new project.


2.  Select a .modproj file to open with WolvenKit


3. WolvenKit will now open the project and proceed to the [**Editor**](editor/)****

****

## Pack Project

#### Packing and installing a mod project



From the [**Editor**](editor/) click on the **Pack Project** button within the **Ribbon.** The [**Log**](editor/log.md) will display a result to indicate packing was successful. All files within the **archive directory** of the [**Project Explorer**](editor/project-explorer.md) will now be packed into archive format. The custom archive is _automatically_ installed to the game installation within the [**Settings**](settings.md) page.

{% hint style="warning" %}
WolvenKit expects **unbundled** files with Oodle compressed internal buffers. Files extracted with WolvenKit Console using **uncook** cannot be packed correctly. All files added with the Asset Browser _will be_ the correct format.
{% endhint %}
