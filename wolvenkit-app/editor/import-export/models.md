# Models

## Exporting mesh files

WolvenKit is capable of exporting Cyberpunk mesh files _natively_ to glTF format. We can export static, skinned, and fully rigged models. Mesh files are exported into distinct submeshes, each representing a different material.

LOD meshes are filtered from exports by default. To export with LOD submeshes, uncheck the `LOD Filter` option within the **Default Export Settings** panel. This is particularly desirable for decal meshes to prevent clipping with the main mesh and vice versa.

Morph targets are automatically included inside the glTF file. You can find the morphs as shapekeys within Blender or blendshapes with Maya.

![](../../../.gitbook/assets/ImportExportTool\_default\_settings.png)

### Export types

#### Default

The default export is versatile enough for most use cases. Any mesh, static or skinned can be exported and imported with this setting. For skinned meshes the bone parenting hierarchy will not be included, however this does not matter for importing meshes. Meshes will be divided into submeshes by material, however they will not include the [**material json**](materials.md#json-i-o) used for Blender integration or editing the material instance.

{% hint style="info" %}
[Learn more about REDengine materials on our dedicated REDengine 4 wiki page](https://wiki.cybermods.net/redengine4-research/assets/shaders/materials)
{% endhint %}

#### WithMaterials

Using the `WithMaterials` export option allows us to edit materials and preview meshes with [**Blender Integration**](blender-integration.md). A bespoke json file will be encoded from the material dependency stack and exported alongside the Raw mesh file. The material json is encoded by leveraging the [**Material Repository**](../../ribbon/tools/material-repository.md). The entire daisy chain of materials is analyzed and written to file top-down, meaning all properties are written as they appear in game.\
\
The material json file can be edited with any text-based editor. Any changes saved to the json file will be written to the mesh file upon each import.\
\
The material json file is necessary for previewing meshes with [Hitman's Blender add-on](blender-integration.md#how-does-it-work). The REDengine data written to json is interpreted by Python script to setup _somewhat_ accurate representations of REDengine shaders.

#### WithRig

Using the `WithRig` export option allows us to export skinned meshes with parented bones. By default exported meshes are correctly skinned, but the skeleton contains no parenting information. Bone-parented rigs are especially useful for posing/animating using a 3d software.

{% hint style="info" %}
Bone parents are not required for successful mesh imports
{% endhint %}

Mesh files themselves do not contain the bone parents, so it's required to select a **rig** file to accompany each mesh export. To select a rig, navigate to the `WithRig Settings` section, and press the **`...`** (Collections) button. This opens the collections menu where you will select your rig file.

#### WithRig usage

Choose a rig file from the panel on the left side, then use the opposing left/right arrows to add or remove a rig. The selected rig will be added to the right panel. Only one rig can be used, so adding more than one rig will result in the 1st rig in the list being selected.

![Navigating the rig menu](../../../.gitbook/assets/8.2\_withrig\_mega\_tutorial.png)

#### Choosing rigs correctly

Generally for NPC heads, weapons, or vehicle meshes you can find the associated rig file similarly named to the mesh in the same or nearest directory. For other meshes such an NPC body, a more generic rig is used.\
\
e.g. Johnny Silverhand is a man with average body proportion so his body uses the following rig:\
`base\characters\base_entities\man_base\deformations_rigs\man_base_deformations.rig` \
\
If the wrong/incompatible rig is used, an error will be displayed within the [**Log**](../log.md)**.**

#### MultiMesh

The `MultiMesh` export option is similar in functionality to [**WithRig**](models.md#withrig)**,** with the addition of support for multiple rigs and meshes. **** This option was implemented because some meshes use more than one rig.\
\
e.g. Judy's mesh **l1\_001\_wa\_pants\_\_judy** uses the following rigs:`base\characters\base_entities\woman_base\deformations_rigs\woman_base_deformations.rig` \
`base\characters\main_npc\judy\l1_001_wa_pants__judy_dangle_skeleton.rig`\
\
Where the dangle rig is used in addition to the base rig to animate Judy's belt.

#### MultiMesh usage

Navigate to the `MultiMesh Settings` and configure the export options for additional meshes and rigs. The functionality is identical to [**WithRig**](models.md#withrig-usage), so the same instructions should be followed.

{% hint style="warning" %}
Remember to add the same mesh that you selected in import/export also in the **mesh collection**
{% endhint %}

![](../../../.gitbook/assets/8.2\_multimesh\_megatut.png)

## Importing mesh files

WolvenKit is able to import custom mesh files. The Import/Export tool expects meshes to be in the glTF format, stored as a .glb file (binary format). The tool supports rigged or rigid (static) models.

{% hint style="warning" %}
By default the mesh importer uses a strict glTF validation check, which can prevent mesh imports with unusual geometry by throwing an error within the Log. The validation error can be bypassed by using **Skip** instead of **Strict**.
{% endhint %}

### Guidelines for successful imports

* Be sure your mesh is **triangulated** and does not contain loose geometry
* Submeshes are ordered by name, adding or removing submeshes will be detrimental\
  e.g. submesh01, submesh\_02, submesh\_03, etc.
* Include **tangent space** on export
* Submeshes should not exceed more than **65535** triangles
* Using Blender? [**Check out our recommend settings below**](models.md#blender-gltf-settings)****

## Blender glTF Settings

### Import

Meshes can be imported with the pre-installed Blender glTF add-on with the default glTF import options. To learn about importing models with the Cyberpunk Blender add-on for shader previews, visit the [**Blender Integration page.**](blender-integration.md) **** The Cyberpunk add-on is not required for modifying meshes.

### **Export**

The following settings are _recommended_ for using Blender with WolvenKit. Unlisted export options can use the **Operator Default** preset (no change). These options may not cover all cases, however it's a good baseline for getting started.

*   Geometry

    * [x] Apply Modifiers
    * [x] Tangents

    &#x20;<mark style="color:blue;">****</mark>**  Materials:** No Export
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

## MorphTargets

{% hint style="warning" %}
Morphtarget I/O is highly experimental, some assets are not handled correctly
{% endhint %}

WolvenKit can export **morphtarget** files from the game to glTF format, these morphtargets files are used to morph a base mesh that exists in the game. For example, the character that you create in the game with different types of nose, eyes, and mouth is formed using the shape keys that exists in the morphtarget files. **You can use Import/Export Tool to export them to glb/glTF,** any morph texture(s) existing in file will also export along in dds format.

![](../../../.gitbook/assets/Blender\_morph\_target\_comparison.png)
