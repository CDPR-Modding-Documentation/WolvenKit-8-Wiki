# Materials

{% hint style="info" %}
****[**Learn more about REDengine materials on our dedicated REDengine 4 wiki page**](https://wiki.redmodding.org/redengine4-research/assets/shaders/materials)****
{% endhint %}

## Material JSON I/O

WolvenKit supports importing and exporting REDengine material information in the form of a bespoke **material json** file. In lieu of a full-blown file editor to tweak materials directly, we support adjusting materials through the material json. When exporting meshes the application presents an option for `WithMaterials` which generates the material json. [**Read more about that process here**](models.md#withmaterials).\
\
The mechanism for generating material json files is baked deeply into the WolvenKit pipeline.&#x20;

* We rely on a local [**Material Repository**](../../ribbon/tools/material-repository.md#what-is-the-material-repository) which contains all material dependencies for any given mesh.\

* For each `WithMaterials` mesh export the dependencies are analyzed, located within the Material Repository (or dumped into the repo if not already present)\

* The material json is encoded by looking at the complete daisy chain of materials. Meaning every single dependency is reviewed and the top-most properties that REDengine sees are written to the material json file.\

* Currently the material json does not differentiate between properties exposed in the last material instance, compared to the material instances underneath. This means that meshes imported with the material json file will write **all material properties**, negating any post-import changes to materials underneath.\
  i.e. Importing Judy's freckle mesh will now ignore any changes to the freckle mi files underneath it.\

* The REDengine values written into the material json file can be interpreted by the Blender Cyberpunk glTF importer to automatically set up shaders within Blender Cycles. [**Read more about Blender integration here**](blender-integration.md#importing-cyberpunk-meshes-with-blender).

