# Import/Export

## What is the Import/Export tool?

The Import/Export tool is an all-purpose method for exporting and importing REDengine files. Game files such as models and textures can be exported from REDengine formats such as XBM and MESH into generic assets such as TGA and glTF. As the name of the tool suggests, these files can be edited externally and imported back into REDengine format and packed as a mod.

![](../../../.gitbook/assets/8.4.3\_ImportExport\_generic\_example.png)

## Supported I/O Formats

The following formats are supported by WolvenKit for imports and exports

* [x] **mesh  ↔  glb/glTF**\
  Rigged and static 3d models can be converted to and from REDengine. Our I/O supports simple non-targeted skinned meshes for extreme efficiency. Advanced methods support multi-mesh, multi-rig, and material embedded meshes. Meshes with embedded morph targets are automatically included as shapekeys. WolvenKit can also export to virtually any 3d format (non-natively) through the built-in renderer Ab3d. You can read more [about Ab3d here.](https://www.ab4d.com/DXEngine.aspx)\

* [x] **xbm  ↔  tga, dds**\
  Textures can be converted to and from REDengine. While various formats including PNG and JPG are supported for exports, only TGA and DDS can be imported directly.\

* [x] **mlmask** ↔ **png, dds**\
  REDengine mlmask files can be exported as an array of textures. These texture arrays can be encoded as a new mlmask with a bespoke masklist helper file.\
  ****
* [x] **bk2 ↔ avi**\
  Video files can be converted to and from REDengine. (Currently implemented with Project Explorer instead of the Import/Export tool)\

* [x] **morphtarget ↔ glb/glTF (unstable)**\
  ****REDengine morphtargets can be exported to glTF format. The morphs can be viewed as shapekeys/blendshapes with a 3d package. glTF files can be used to recreate morphtarget files, however only one morph is preserved.\

* [x] **anims** → **glb/glTF (unstable)**\
  ****Animation files can be exported to glTF format. However this feature is highly experimental. New anims files cannot be imported at this time.\


### Conversions

The following non-REDengine formats are supported by WolvenKit using the converter

**glTF  ↔  FBX \***\
****Models can be converted from glTF to FBX, and vice versa.\
_\*Only static FBX files are supported for conversion at this time._

## Using the Import/Export tool

From the main Editor click the Utilities tab of the [**Ribbon**](../../ribbon/). Open the Import/Export tool by clicking the icon within the ribbon. The Import/Export tool can then be accessed similarly to other WolvenKit tools such as the Asset Browser.

{% hint style="warning" %}
Most imports require an existing REDengine file! For successful imports, ensure that the Mod directory contains a "mirrored" file.\
\
_For example, **both** files below must be present for a successful mesh import:_\
**Mod\base\characters\main\_npc\judy\g1\_001\_wa\_glove\_\_judy.mesh**\
**Raw\base\characters\main\_npc\judy\g1\_001\_wa\_glove\_\_judy.glb**
{% endhint %}

### Simple Import/Export

* Choose the import or export view by selecting the circular icon\

* Select the files you want to import or export by checking the box icon in the left column, then click **Process Selected** to perform the export operation\

* **Process All** will process all files regardless of selection\

* Processed files will be available inside the Raw directory of the Project Explorer

### Advanced Import/Export

* Choose the import or export view by selecting the circular icon\

* Double-click any file within the Import/Export grid to view advanced options\

* (Optional) Check the subpages for Import/Export to learn more about these options by reading the respective wiki pages for each file\

* (Optional) Check `Apply to all files of the same Extension` to temporarily adjust advanced options for all files of the same type. This can be useful for batch exports\

* Click **Confirm** to save advanced options\

* Select the files you want to import or export by checking the box icon in the left column, then click **Process Selected** to perform the export operation\

* **Process All** will process all files regardless of selection\

* Processed files will be available inside the Raw directory of the Project Explorer

![Advanced mesh export settings with 8.4.3](../../../.gitbook/assets/8.4.3\_ImportExport\_mesh\_advanced.png)

#### Import/Export Templates

Within the Import/Export grid files can be "locked" as a template. For example, advanced options can be used to set XBM export type to PNG.

1. Select a file and press the **Lock icon**
2. Select other files of the same extension within the grid
3. Choose **Selected in Grid**, or **All in Grid**
4. Press **Copy Settings** to to apply the advanced options
