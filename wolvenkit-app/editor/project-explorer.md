# Project Explorer

## What is the Project Explorer?

The Project Explorer is similar to any file explorer, however it is fixed to the base of your mod project. There are two main **WolvenKit system directories** inside the Project Explorer. These directory folders themselves are _not_ part of your mod, and will _not_ be included in the packed mod.&#x20;

* The **Mod** directory is home to all REDengine [**CR2W**](../../help/glossary.md#cr-2-w) files. These files are automatically included in the archive when packing your mod project.
* The **Raw** directory is home to your source assets such as meshes and textures. These files will not be included in the packed mod project, however they are extremely valuable to have nearby with our content pipeline.

![](../../.gitbook/assets/8.4.3\_ProjectExplorer\_generic.png)

{% hint style="info" %}
****[**Click here to learn more about using the Asset Browser to add files to your project**](asset-browser.md)****
{% endhint %}

## Using the Project Explorer

### Opening Files

WolvenKit allows us to edit the contents of any [**CR2W**](../../help/glossary.md#cr-2-w) file by double-clicking the file inside the Project Explorer. These files can be added to the Mod directory of your project by using the Asset Browser.

Non-CR2W files which are typically stored in the Raw directory can be accessed with the Project Explorer as well. Select files such as blend, psd, png, and many more can be opened with your preferred system application. For example, double-clicking a glb (glTF binary) file will result in opening the mesh file with Windows 3D Viewer.

### Deleting, Renaming, Copy and Pasting

For any file operation, right-click the file within the Project Explorer and navigate the submenu under the **File** button. Alternatively the context **Ribbon** can be used as well.

![Context Ribbon for Project Explorer](../../.gitbook/assets/8.2\_ribbon\_pe\_actions.png)

### Expanding or collapsing folders

The folders and files in the Project Explorer can be seen as nodes. To collapse/expand all folders or a child, choose an option from the context Ribbon while a folder is selected within the Project Explorer.

### Locating files with file explorer

To find a project file with your system file explorer, right-click any file within the Project Explorer or use the context Ribbon, then select **Open In file explorer.**

