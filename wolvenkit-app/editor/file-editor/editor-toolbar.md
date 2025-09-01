---
description: The CR2W Editor's toolbar, and what you can do there
---

# Editor Toolbar

## Summary

**Created:** Sep 01 2025 by [mana vortex](https://app.gitbook.com/u/NfZBoxGegfUqB33J9HXuCs6PVaC3 "mention")\
**Last documented update:** Sep 01 2025 by [mana vortex](https://app.gitbook.com/u/NfZBoxGegfUqB33J9HXuCs6PVaC3 "mention")

This page documents the editor menu bar.

<figure><img src="../../../.gitbook/assets/image (19).png" alt="" width="563"><figcaption><p>The editor toolbar as seen in a .mesh file as of Wolvenkit 8.16.2</p></figcaption></figure>

## Editor Mode

Here you can toggle the [editor-difficulty-mode.md](editor-difficulty-mode.md "mention"). Please see the corresponding wiki page for details.

## Materials

Only visible in `.mesh` and `.mi` files.

### Copy materials from other mesh

{% hint style="info" %}
Hold shift to turn this into `Copy materials to other meshes`&#x20;
{% endhint %}

Only visible in `.mesh` files. Lets you copy appearances, material definitions, and materials from a different file.

You have the following options:

* **From ArchiveXL patch mesh**: Requires the mod to be installed. Will read the .xl file and find the corresponding patch mesh, then copy all materials and definitions.\
  This does not work if you custompathed your file already.
* **From project mesh:** The dropdown lets you select a project mesh
* **Enter by hand:** Put a depot path here. Order of evaluation is project files > mod files > game files. If you have multiple mod files at the same depot path, the first match will be used.

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

### Generate missing materials

If you have chunk materials that do not yet have material entries, you can use this button to generate `localMaterialInstances` for them.&#x20;

{% hint style="info" %}
Consider using [ArchiveXL: dynamic materials](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/modding-guides/textures-and-luts/archivexl-dynamic-materials "mention")instead!
{% endhint %}

### Toggle "EnableMask"

Only visible with one or more `materialEntries` selected. Will toggle `IsMasked` flag for all of them.

### Toggle "IsLocalInstance"

Only visible with one or more `materialEntries` selected. Will toggle `IsLocalInstance` flag for all of them.

### Add material dependencies

{% hint style="info" %}
You can hold down the Shift key to include base game files.
{% endhint %}

NPV modders love it: This button collects all required .mi files and textures into a directory in your mod, then updates the internal paths. [Custompathing](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/modding-guides/items-equipment/custompathing-assets) made easy!

## Clean up

Only visible in `.mesh`, `.json`, `.app`

### Mesh files

#### Delete unused materials

Hold Shift for `Clear all materials` (for ArchiveXL material patching)

Run this directly after you deleted appearances. Will delete material definitions and materials, adjusting the index properties.&#x20;

{% hint style="info" %}
If you are running this on an eye mesh (name must contain `he_`), a dialogue will ask for your eyelash colour.
{% endhint %}

#### Convert preload materials to local

Only visible if you have materials in `preloadLocalMaterialInstances` or `preloadExternalMaterialInstances` - will move them to `materials`.`localMaterialInstances` instead.

#### Delete chunk by submesh index

If you deleted a submesh in Blender, use this to remove all the corresponding chunks (e.g. you deleted submesh\_02 out of 11)

#### Adjust submesh counts

Useful for cleaning up those ancient template meshes: this will make sure that the chunkMaterials of each appearance will have an entry for every submesh. This will ignore empty chunkMaterials - use [#un-dynamify-appearances](editor-toolbar.md#un-dynamify-appearances "mention") to expand)

### App files

#### Delete unused animated components

Will remove animated components that aren't used as `skinning` or `parentTransform` by other components

#### Find unused files in project

Does the same as `Project` -> `Clean Up` -> `Find Unused Files`, but will only consider file extensions that can be used in `.app` files (`.mesh`, `.rig`, `.animgraph`, `.morphtarget`). Will let you find those backup files you forgot to delete.

### JSON files

#### Delete duplicate entries

Will delete translation entries that have the same `secondaryKey`.

## ArchiveXL

Only visible in `.mesh` files.

### Un-dynamify appearances

Will un-do the effect of [ArchiveXL: dynamic materials](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/modding-guides/textures-and-luts/archivexl-dynamic-materials "mention"). This is useful for NPVs and personal ports.

### Clear chunk materials

Deletes the chunk materials for multiple selected appearances (quickly convert something to [Mesh Appearance: Auto Expansion](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/modding-guides/textures-and-luts/archivexl-dynamic-materials#mesh-appearance-auto-expansion "mention"))

### Convert hair to CCXL material

Convert a vanilla hair mesh to be CCXL-ready. You should have the corresponding .mi files in your project already.

## Appearances/Components

Only visible in `.app` and `.ent` files

### Generate CRUIDs in selection

### Regenerate visual controllers

Regenerates the `visualControllers` array. This is required for e.g. vehicle mods.

### Regenerate resolved dependencies

Regenerates the `resolvedDependencies` array. Use this to make the game preload the files in your mod.

### Edit Components -> Change mesh component properties

Only visible in .app files

Quickly edit component properties over multiple appearances:

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

### Edit Components -> Create new component from existing

Only visible in .app files

Create a new component by duplicating an existing one across multiple appearances. You can use [#edit-components-greater-than-change-mesh-component-properties](editor-toolbar.md#edit-components-greater-than-change-mesh-component-properties "mention") after.

### Delete... -> Delete component by name

Only visible in .app files

Delete a component across multiple appearances.

### Clear PartsOverrides

Only visible in .app files

Deletes everything in the `partsOverrides` array.

{% hint style="info" %}
ArchiveXL uses PartsOverrides to load mesh appearances, so delete at own risk.
{% endhint %}

### Clear PartsValues

Only visible in .app files

Deletes everything in the `partsValues` array.

### Connect to .ent file

Only visible in .app files

Registers all appearances in the .app file in the selected `.ent` file. You can use that to quickly update your NPV entities.&#x20;

{% hint style="info" %}
For clothes, do yourself a favour and use[ItemAdditions: Dynamic Appearances](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/modding-guides/items-equipment/adding-new-items/archivexl-dynamic-variants "mention")instead!
{% endhint %}

### Force LOD level 0

Change all components to be always visible.

{% hint style="info" %}
This will impact performance, so do this **only** for your NPV and not for your world addition.
{% endhint %}

### Change facial animations

Only visible in .app files

Change a characters's facial animation setup by picking from a dialogue.

### Generate CRUID(s)

Generates new CRUIDs for all components in the selection / for all nested components. The game tells things apart via `name` and `id`, so if your stuff isn't unique enough, consider running this.

## File Validation

### Run WScript

Will run [#file-validation](editor-toolbar.md#file-validation "mention") script on the active tab

### Find broken references

Will scan the current file for broken references (depot paths that are neither in the game files nor in your project)
