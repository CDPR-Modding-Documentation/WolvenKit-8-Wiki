# Import/Export: Models

{% hint style="info" %}
For a step-by-step workflow and troubleshooting, see \
[Cyberpunk 2077 Modding](http://127.0.0.1:5000/o/-MP5ijqI11FeeX7c8-N8/s/4gzcGtLrr90pVjAWVdTc/ "mention") -> [Exporting and importing meshes](http://127.0.0.1:5000/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators/3d-modelling/exporting-and-importing-meshes "mention")&#x20;
{% endhint %}

## Exporting mesh files

WolvenKit is capable of exporting Cyberpunk mesh files _natively_ to glTF format. We can export static, skinned, and fully rigged models. Mesh files are exported into distinct submeshes, each representing a different material.

Morph targets are automatically included inside the glTF file. You can find the morphs as shapekeys within Blender or blendshapes with Maya.

<div align="left">

<img src="../../../.gitbook/assets/ImportExportTool_default_settings.png" alt="">

</div>

### Default Export Settings

#### LOD Filter

If selected extra LOD models will be removed from the export

#### Is Binary

If selected mesh exports will be in binary from as **GLB** rather than **glTF** format. (Recommended)

Export Materials

If selected a helper Material.json file is generated to allow materials to be edited with exported models. After performing a WithMaterials export, a JSON helper file will be nested with the exported mesh within the _raw directory_. Material exports also allow for detailed mesh previews with the [**Cyberpunk add-on for Blender**](../blender-integration.md).

### Export types

#### <mark style="color:red;">MeshOnly</mark>

The default export is versatile enough for most use cases. Any mesh, static or skinned can be exported and imported with this setting. For skinned meshes the bone parenting hierarchy will not be included, however this does not matter for importing meshes. Meshes will be divided into submeshes by material.

#### <mark style="color:red;">WithRig</mark>

{% hint style="info" %}
Bone parents are not required for successful mesh imports
{% endhint %}

Using the `WithRig` export option allows us to export skinned meshes with parented bones. By default exported meshes are correctly skinned, but the skeleton contains no parenting information. Bone-parented rigs are especially useful for posing/animating using a 3d software.

Mesh files themselves do not contain the bone parents, so it's required to select a **rig** file to accompany each mesh export. To select a rig, in the `WithRig Settings` section of the right panel press the **`...`** (Collections) button. This opens the collections menu where you will select your rig file.

#### WithRig usage

Choose a rig file from the panel on the left side, then use the opposing left/right arrows to add or remove a rig. The selected rig will be added to the right panel. Only one rig can be used, so adding more than one rig will result in the 1st rig in the list being selected.

<img src="../../../.gitbook/assets/8.2_withrig_mega_tutorial.png" alt="Navigating the rig menu" data-size="original">

#### Choosing rigs correctly

Generally for NPC heads, weapons, or vehicle meshes you can find the associated rig file similarly named to the mesh in the same or nearest directory. For other meshes such an NPC body, a more generic rig is used.\
\
e.g. Johnny Silverhand is a man with average body proportion so his body uses the following rig:\
`base\characters\base_entities\man_base\deformations_rigs\man_base_deformations.rig` \
\
If the wrong/incompatible rig is used, an error will be displayed within the [**Log**](../../editor/log.md)**.**

#### <mark style="color:red;">MultiMesh</mark>

The `MultiMesh` export option is similar in functionality to [**WithRig**](models.md#withrig)**,** with the addition of support for multiple rigs and meshes. This option was implemented because some meshes use more than one rig.\
\
e.g. Judy's mesh **l1\_001\_wa\_pants\_\_judy** uses the following rigs:`base\characters\base_entities\woman_base\deformations_rigs\woman_base_deformations.rig` \
`base\characters\main_npc\judy\l1_001_wa_pants__judy_dangle_skeleton.rig`\
\
Where the dangle rig is used in addition to the base rig to animate Judy's belt.

#### MultiMesh usage

Navigate to the `MultiMesh Settings` and configure the export options for additional meshes and rigs. The functionality is identical to [**WithRig**](models.md#withrig-usage), so the same instructions should be followed.

![](../../../.gitbook/assets/8.2\_multimesh\_megatut.png)

## Importing mesh files

WolvenKit is able to import custom mesh files. The Import/Export tool expects meshes to be in the glTF format, stored as a .glb file (binary format). The tool supports skinned (animated) or rigid (static) models.

### Guidelines for successful imports

* Be sure your mesh is **triangulated** and does not contain loose geometry
* Submeshes are ordered by name, adding or removing submeshes will be detrimental\
  e.g. submesh01, submesh\_02, submesh\_03, etc.
* Include **tangent space** on export
* Submeshes should not exceed more than **65535** triangles
* Using Blender? [**Check out our recommend settings below**](models.md#blender-gltf-settings)

### Import Settings

#### Import Material.json Only

Useful for updating material information only, without disturbing the original geometry data.

#### GLTF Validation Checks

Use the GLTF library to run some basic checks to detect bad geometry.

#### Import As REDengine File Format

Select the desired destination format. (mesh/morphtarget)

#### Use existing file

Rebuild the existing mesh file. (Required)

{% hint style="info" %}
Having trouble modifying a mesh file? Keep in mind WolvenKit always uses an existing mesh file for each import. Once a mesh file is corrupted, all subsequent imports will be corrupted as well. [**Try replacing the source mesh with the original!**](../../editor/project-explorer.md#replace-with-original)
{% endhint %}

## Blender glTF Settings

### Import

Meshes can be imported with the pre-installed Blender glTF add-on with the default glTF import options. To learn about importing models with the Cyberpunk Blender add-on for shader previews, visit the [**Blender Integration page.**](../blender-integration.md) The Cyberpunk add-on is not required for modifying meshes.

### **Export**

The following settings are _recommended_ for using Blender with WolvenKit. Unlisted export options can use the **Operator Default** preset (no change). These options may not cover all cases, however it's a good baseline for getting started.

*   Geometry

    * [x] Apply Modifiers
    * [x] Tangents

    &#x20;** Materials:** No Export
* Shape Keys
  * [x] Shape Key Tangents

{% hint style="warning" %}
New to Blender and/or modding? Remember to remove all extra assets before exporting! Do not include lights, cameras, or other meshes such as the default cube.
{% endhint %}

## Submeshes

Meshes are sorted and given materials based on the submesh index. LOD variants are numbered as 1, 2, 4, and 8 which corresponds to the REDengine value. _These are not the distances at which the LOD is applied._

{% hint style="info" %}
It's important to remember the submesh name is determined by the **Data Block** not the **Object Name**. The orange colored icon represents the Blender object name, while the green polygon represents the _actual_ name of the mesh.
{% endhint %}

It's possible to reference the material structure of the original mesh file using WolvenKit to see how each submesh is mapped to a distinct material.

![Example of material list inside a mesh file](../../../.gitbook/assets/ImportExportTool\_materials\_example.png)

In the example above, you can see the material list which repeats after reaching `glass1` meaning this is the final submesh. We now know this mesh has 12 distinct submeshes (0-11). It also contains four LOD's because each material list is repeated for a total of four lists.

{% hint style="info" %}
For a detailed breakdown of each material, use the [**WithMaterials**](models.md#withmaterials) option for mesh exports.
{% endhint %}

## Material JSON I/O

WolvenKit supports importing and exporting REDengine material information in the form of a bespoke **material json** file.  [**Learn more above**](models.md#withmaterials)

The material json file is necessary for previewing meshes with the [**Cyberpunk Blender add-on**](../blender-integration.md). The REDengine data written to json is interpreted by Python script to setup _somewhat_ accurate representations of REDengine shaders.

{% hint style="info" %}
Just looking to edit materials? WolvenKit can directly edit materials within **.mesh** or **.mi** files using the File Editor.
{% endhint %}

### Technical Details

A bespoke json file will be generated from the material dependency stack and exported alongside the raw mesh file. The entire daisy chain of materials is analyzed and written to file top-down, meaning all properties are written as they appear in game. The material json file can be edited with any text-based editor. Any changes saved to the json file will be written to the mesh file upon each import.

* We rely on the [**Depot**](../../settings.md#depot-path) (a local file cache) which contains all material dependencies for any given mesh.\

* For each `WithMaterials` mesh export, the material dependencies are analyzed and missing resources are dumped to the Depot.\

* The material json is generated by looking at the complete daisy chain of materials. Meaning every single dependency is reviewed and the top-most properties that REDengine sees are written to the material json file.\

* The REDengine values written into the material json file can be interpreted by the Blender Cyberpunk glTF importer to automatically set up shaders within Blender Cycles. [**Read more about Blender integration here**](../blender-integration.md#importing-cyberpunk-meshes-with-blender).

## MorphTargets

{% hint style="warning" %}
Morphtarget I/O is highly experimental, some assets are not handled correctly
{% endhint %}

WolvenKit can export **morphtarget** files from the game to glTF format, these morphtargets files are used to morph a base mesh that exists in the game. For example, the character that you create in the game with different types of nose, eyes, and mouth is formed using the shape keys that exists in the morphtarget files. **You can use Import/Export Tool to export them to glb/glTF,** any morph texture(s) existing in file will also export along in dds format.

![](../../../.gitbook/assets/Blender\_morph\_target\_comparison.png)
