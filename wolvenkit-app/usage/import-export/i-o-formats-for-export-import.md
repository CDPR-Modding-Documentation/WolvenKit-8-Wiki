---
description: Overview of supported I/O formats
---

# I/O formats for export/import

The following formats are supported by WolvenKit for imports and exports

* [x] **mesh  ↔  glb/glTF**\
  Rigged and static 3d models can be converted to and from REDengine. \
  \
  For a detailed guide, see [here](http://127.0.0.1:5000/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators/3d-modelling/exporting-and-importing-meshes).\
  \
  Our I/O supports simple non-targeted skinned meshes for extreme efficiency. Advanced methods support multi-mesh, multi-rig, and material embedded meshes. Meshes with embedded morph targets are automatically included as shapekeys. WolvenKit can also export to virtually any 3d format (non-natively) through the built-in renderer Ab3d. You can read more [about Ab3d here.](https://www.ab4d.com/DXEngine.aspx)\

* [x] **xbm  ↔  png, tga, dds, jpg, bmp, tiff**\
  Textures can be converted to and from REDengine.\
  \
  For a detailed guide, see [here](http://127.0.0.1:5000/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators/modding-guides/textures-and-luts/images-importing-editing-exporting).\

* [x] **mlmask** ↔ **png, tga, dds, jpg, bmp, tiff**\
  REDengine mlmask files can be exported as an array of textures. These texture arrays can be encoded as a new mlmask with a bespoke masklist helper file.\
  \
  For a detailed guide, see [here](http://127.0.0.1:5000/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators/modding-guides/textures-and-luts/custom-multilayermasks).\

* [x] **wem ↔ wav, mp3**\
  Audio files can be converted to and from REDengine. Use the Sound Modding Tool to import new audio.\

* [x] **bk2 ↔ avi**\
  Video files can be converted to and from REDengine. (Currently implemented with Project Explorer instead of the Import/Export tool)\

* [x] **morphtarget ↔ glb/glTF (experimental)**\
  REDengine morphtargets can be exported to glTF format. The morphs can be viewed as shapekeys/blendshapes with a 3d package. glTF files can be used to recreate morphtarget files, however only one morph is preserved.\

* [x] **anims ↔ glb (experimental)**\
  Animation files can be exported to glTF format. \
  To import a .glb file as animation, switch `Target File Format` to `anims` in the export settings.\
  You can find a detailed guide about this process [here](http://127.0.0.1:5000/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators/modding-guides/animations/poses-animations-make-your-own). \
  \
