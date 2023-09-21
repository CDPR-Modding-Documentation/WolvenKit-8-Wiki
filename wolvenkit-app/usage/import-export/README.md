---
description: Wolvenkit Import and Export explained
---

# Import/Export

## Section Brief

This section contains **general information** and **workflow documentation** about importing and exporting files with Wolvenkit.

## UI/Workflow documentation

### Export

[tools-import-export](../../tools/tools-import-export/ "mention") -> [#export-tool](../../tools/tools-import-export/#export-tool "mention")

[import-export-as-json.md](import-export-as-json.md "mention") -> [#export-as-json](import-export-as-json.md#export-as-json "mention")

### Import

[tools-import-export](../../tools/tools-import-export/ "mention") -> [#import-tool](../../tools/tools-import-export/#import-tool "mention")

[import-export-as-json.md](import-export-as-json.md "mention") ->[#import-as-json](import-export-as-json.md#import-as-json "mention")



## File Structure

{% hint style="info" %}
Moving or renaming files usually breaks the import. Read on to find out why.
{% endhint %}

When exporting a resource, Wolvenkit puts the exported file into your project's `raw` folder. The relative paths (starting under `archive`/`raw`) are the same, as will the file name (without extensions).&#x20;

#### These files are connected:

```
source/archive/base/path/your_file.mesh
source/raw/base/path/your_file.glb
```

You can import `your_file.glb` via **Import Tool**.

#### These files are **not** connected:

```
source/archive/base/path/your_file.mesh
source/raw/base/path/your_file_mesh_export.glb
```

You can **not** import `your_file_mesh_export.glb` via **Import Tool**, because Wolvenkit won't know where to put it.

## Exporting

Wolvenkit knows to ways of exporting files: [to JSON](import-export-as-json.md#export-as-json), or via the [Export Tool](../../tools/tools-import-export/#export-tool).

Exported files will be created in your project's **raw** folder. The [relative path](#user-content-fn-1)[^1] will be the same.

## Importing

Unless importing [from JSON](./#import-from-json), Wolvenkit can't **create files**.&#x20;

When using the [Import Tool](./#import-tool), we can only import into already existing containers (see [#file-structure](./#file-structure "mention") for more information)

The easiest way to do that is:&#x20;

1. export an existing file
2. overwrite the new file in `raw` with your changes
3. import the file



### Import from JSON

This option is **in the right-click menu.**

[^1]: Path inside the game files, e.g. `tutorial\my_first_mod\meshes\my.mesh`
