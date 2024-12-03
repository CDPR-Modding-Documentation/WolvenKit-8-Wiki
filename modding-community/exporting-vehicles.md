---
description: Step-by-step guide for exporting vehicles to Blender
---

# Exporting Vehicles

## Summary

**Created by** [Simarilius](https://app.gitbook.com/u/G2MqNkfgTlQ1R3G4B5s6WefLjdy2 "mention") \
**Published May 2023**&#x20;

This guide aims to walk you through finding and exporting a vehicle to blender.&#x20;

If you'd rather watch a video Boe6 goes through a basic example in the second of his vehicle modding videos [here](https://youtu.be/nrJKP5rr6Uc?si=fyDl99t4EQ6htcYp\&t=118). You still have to read below if you want an non default appearance.

### Requirements

* [**Wolvenkit 8.9.1**](https://github.com/WolvenKit/WolvenKit-nightly-releases/releases) **or newer**
* [**Blender 3.6**](https://www.blender.org/download/releases/3-6/) **or newer (hasnt been tested on older)**
* [**Cyberpunk add-on for Blender 1.4.0**](https://github.com/WolvenKit/Cyberpunk-Blender-add-on) **or newer**

Vehicles have different challenges from the characters, but the [Blender Addon](https://github.com/WolvenKit/Cyberpunk-Blender-add-on) is fully up to the task, as long as you give it the right info.&#x20;

Importing vehicles to blender needs the `.ent`, `.app` & `.rig` files in .json format, along with all the meshes and the main `.anim` file for the vehicle as `.glb`. Fortunately, there is a script to do the heavy lifting – and this guide will tell you how to use it.

{% hint style="info" %}
.ent files for pretty much all the vehicles are listed on the Cyberpunk modding wiki [here](https://wiki.redmodding.org/cyberpunk-2077-modding/modding-know-how/references-lists-and-overviews/files-for-modding/vehicles).

You need to find the one for your vehicle, and add it to your project.
{% endhint %}

Once you've added the `.ent` to your project, you now have two options, of which you can use either:

1. "Find Used Files" from the context menu, then manually add them all to your project
2. Use the script from Tools -> Script Manager -> `Export_Vehicle_Ent` (the [box below](exporting-vehicles.md#script-add-all-dependencies-to-the-project) has documentation)

Being lazy people, we naturally recommend the second option.

<details>

<summary>Script documentation</summary>

The most recent version of this script is shipped with Wolvenkit (find it in Tools -> Script Manager -> `Export_Vehicle_Ent`). The code below is here for the purpose of documentation and will not be kept up-to-date, so **do not run it**. If you want to get the script's most recent version, find it in the [Wolvenkit-Resources Repository](https://github.com/WolvenKit/Wolvenkit-Resources/blob/main/Scripts/Export_Vehicle_Ent.wscript).&#x20;

By default, it will  ignore shadows, proxy and FX meshes. To include them anyway, set the corresponding flags to `true` – find `include_proxys`, `include_shadows`, `include_fx`. (If you don't know why you'd want them, you won't!)

```javascript
// Entity export script FOR VEHICLES dont use if you dont need all the anims and rig.
// @author Simarilius, DZK & Seberoth
// @version 1.1
// Exports ent files and all referenced files (recursively)
import * as Logger from 'Logger.wscript';
import * as TypeHelper from 'TypeHelper.wscript';

const fileTemplate = '{"Header":{"WKitJsonVersion":"0.0.7","DataType":"CR2W"},"Data":{"Version":195,"BuildVersion":0,"RootChunk":{},"EmbeddedFiles":[]}}';
const jsonExtensions = [".app", ".ent", ".mesh", ".rig"];
const exportExtensions = [".anims", ".mesh"];
const exportEmbeddedExtensions = [".mesh", ".xbm", ".mlmask"];

// Rather than a manual list does it for all ents in the project.
var ents = [];

// if you dont want to process any entities already in the project set this to false
var add_from_project = true;

// sets of files that are parsed for processing
const parsedFiles = new Set();
const projectSet = new Set();
const exportSet = new Set();
const jsonSet = new Set();
const rigs = new Map();

if (add_from_project) {
    for (var filename of wkit.GetProjectFiles('archive')) {
        //Logger.Info(filename)
        var ext = filename.split('.').pop();
        if (ext === "ent") {
            ents.push(filename);
        }
        if (ext === "anims") {
            exportSet.add(filename);
        }
    }
}

// Set these to true if you want proxys/shadow meshes
var include_proxys = false;
var include_shadows = false;
var include_fx = false;

// loop over every entity in `ents` and find rigs
for (var ent in ents) {
    Logger.Info('Finding rigs in ' + ents[ent]);
    FindEntRigs(ents[ent]);
    FindEntAnims(ents[ent]);
    Logger.Info('');
    for (const [key, value] of rigs) {
        Logger.Info(`${key} = ${value}`);
        if (!value.includes("base_rig")) {
            projectSet.add(value);
            jsonSet.add(value);
        }
    }
    Logger.Info('');
}

// now find the mesh files
for (var ent in ents) {
    Logger.Info(ents[ent]);
    ParseFile(ents[ent], null);
}

// save all our files to the project and export JSONs
for (const fileName of projectSet) {
    // skip shadows if the variable is set
    if ((include_shadows == false) && (fileName.includes("shadow"))) {
        continue;
    }
    // skip proxies if the variable is set
    if ((include_proxys == false) && (fileName.includes("proxy"))) {
        continue;
    }
    // skip fx bodies if the variable is set
    if ((include_fx == false) && (fileName.includes("fx"))) {
        continue;
    }
    // Load project vesion if it exists, otherwise add to the project
    if (wkit.FileExistsInProject(fileName)) {
        var file = wkit.GetFileFromProject(fileName, OpenAs.GameFile);
    }
    else {
        var file = wkit.GetFileFromBase(fileName);
        wkit.SaveToProject(fileName, file);
    }

    if (jsonSet.has(fileName)) {
        var path = "";
        if (file.Extension === ".ent") {
            path = wkit.ChangeExtension(file.Name, ".ent.json");
        }
        if (file.Extension === ".app") {
            path = wkit.ChangeExtension(file.Name, ".app.json");
        }
        if (file.Extension === ".rig") {
            path = wkit.ChangeExtension(file.Name, ".rig.json");
        }
        if (file.Extension === ".mesh") {
            path = wkit.ChangeExtension(file.Name, ".mesh.json");
        }
        if (path.length > 0) {
            var json = wkit.GameFileToJson(file);
            wkit.SaveToRaw(path, json);
        }
    }
}

// export all of our files with the default export settings
wkit.ExportFiles([...exportSet]);

// begin helper functions
function* GetPaths(jsonData) {
    for (let [key, value] of Object.entries(jsonData || {})) {
        if (value instanceof TypeHelper.ResourcePath && !value.isEmpty()) {
            yield value.value;
        }

        if (typeof value === "object") {
            yield* GetPaths(value);
        }
    }
}

function convertEmbedded(embeddedFile) {
    let data = TypeHelper.JsonParse(fileTemplate);
    data["Data"]["RootChunk"] = embeddedFile["Content"];
    let jsonString = TypeHelper.JsonStringify(data);

    let cr2w = wkit.JsonToCR2W(jsonString);
    wkit.SaveToProject(embeddedFile["FileName"], cr2w);
}

// Parse a CR2W file
function ParseFile(fileName, parentFile) {
    // check if we've already worked with this file and that it's actually a string
    if (parsedFiles.has(fileName)) {
        return;
    }
    parsedFiles.add(fileName);

    let extension = 'unkown';
    if (typeof (fileName) === 'string') {
        extension = "." + fileName.split('.').pop();
    }

    if (extension !== 'unkown') {
        if (!(jsonExtensions.includes(extension) || exportExtensions.includes(extension))) {
            return;
        }

        if (parentFile != null && parentFile["Data"]["EmbeddedFiles"].length > 0) {
            for (let embeddedFile of parentFile["Data"]["EmbeddedFiles"]) {
                if (embeddedFile["FileName"] === fileName) {
                    convertEmbedded(embeddedFile);

                    if (jsonExtensions.includes(extension)) {
                        jsonSet.add(fileName);
                    }

                    if (exportEmbeddedExtensions.includes(extension)) {
                        exportSet.add(fileName);
                    }

                    return;
                }
            }
        }
    }

    if (typeof (fileName) === 'bigint') {
        fileName = fileName.toString();
    }

    if (typeof (fileName) !== 'string') {
        Logger.Error('Unknown path type');
        return;
    }

    // Load project vesion if it exists, otherwise get the basegamefile
    if (wkit.FileExistsInProject(fileName)) {
        var file = wkit.GetFileFromProject(fileName, OpenAs.GameFile);
    }
    else {
        var file = wkit.GetFileFromBase(fileName);
    }

    if (file === null) {
        Logger.Error(fileName + " could not be found");
        return;
    }

    extension = file.Extension;

    if (!(jsonExtensions.includes(extension) || exportExtensions.includes(extension))) {
        return;
    }

    projectSet.add(fileName);

    if (jsonExtensions.includes(extension)) {
        jsonSet.add(fileName);
    }

    if (exportExtensions.includes(extension)) {
        exportSet.add(fileName);
    }

    if (extension === ".app" || extension === ".ent" || extension === ".mesh" || extension === ".anims") {
        var json = TypeHelper.JsonParse(wkit.GameFileToJson(file));
        for (let path of GetPaths(json["Data"]["RootChunk"])) {
            ParseFile(path, json);
        }
    }
}

// Parse a ent file for rigs
function FindEntRigs(fileName) {
    if (wkit.FileExistsInProject(fileName)) {
        var file = wkit.GetFileFromProject(fileName, OpenAs.GameFile);
    }
    else {
        var file = wkit.GetFileFromBase(fileName);
    }
    var json = TypeHelper.JsonParse(wkit.GameFileToJson(file));
    //find the rigs in the base ent components (normally root and deformations)
    for (let comp of json["Data"]["RootChunk"]["components"]) {
        if (!("rig" in comp) == 0) {
            //Logger.Info(comp["name"]);
            //Logger.Info(comp["rig"]["DepotPath"]);
            rigs.set(comp["name"].toString(), comp["rig"]["DepotPath"].toString());
        }
    }
    // find any rigs referenced in the appearances (head and dangle)
    for (let app of json["Data"]["RootChunk"]["appearances"]) {
        var appfileName = app["appearanceResource"]["DepotPath"];
        //Logger.Info(appfileName);
        var appfile = wkit.GetFileFromBase(appfileName.toString());
        var appjson = TypeHelper.JsonParse(wkit.GameFileToJson(appfile));
        for (let appApp of appjson["Data"]["RootChunk"]["appearances"]) {
            for (let appcomp of appApp["Data"]["components"]) {
                if (!("rig" in appcomp) == 0) {
                    //Logger.Info(appcomp["name"]);
                    //Logger.Info(appcomp["rig"]["DepotPath"]);
                    rigs.set(appcomp["name"].toString(), appcomp["rig"]["DepotPath"].toString());
                }
            }
        }
    }
}

// Parse a ent file for rigs
function FindEntAnims(fileName) {
    if (wkit.FileExistsInProject(fileName)) {
        var file = wkit.GetFileFromProject(fileName, OpenAs.GameFile);
    }
    else {
        var file = wkit.GetFileFromBase(fileName);
    }
    var json = TypeHelper.JsonParse(wkit.GameFileToJson(file));
    //find the anims in the ent resolved dependencies
    for (let dep of json["Data"]["RootChunk"]["resolvedDependencies"]) {
        Logger.Info(dep["DepotPath"].toString());
        projectSet.add(dep["DepotPath"].toString());
        exportSet.add(dep["DepotPath"].toString());
    }
}

function get_filename(str) {
    return str.split('\\').pop().split('/').pop();
}

```

</details>

Check your project tree to make sure that you have the vehicle's .anims file. If there is one, you can go directly to the [next section](exporting-vehicles.md#your-entity-in-blender).

<details>

<summary>If the script hasn't found an .anims file</summary>

If no .anims file is exported (as for example with thee Arch), you need to find it yourself.&#x20;

You can either&#x20;

* browse through the folder  `\base\animations\vehicle`
* or put `\base\animations\vehicle > .anims` into Wolvenkit's [search bar](../wolvenkit-app/usage/wolvenkit-search-finding-files.md).

Once you have found the .anims file, add it to your project and export it to .glb with the export tool. (The script should now pick it up, but – better safe than sorry!

</details>

### Get a specific appearance

If you're fine with the default appearance, you can go to the [next section](exporting-vehicles.md#your-entity-in-blender) and import your project into Blender.

Otherwise, you need to enter the exact **appearanceName** into the Blender open dialog. You can find the appearance name in your `.ent` file inside the `appearances` list:

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>The same file that you picked in Step 1</p></figcaption></figure>

## Your entity in Blender

In Blender, select `File` -> `Import` -> `Cyberpunk Entity`. You need to point it at your exported vehicle entity – find it in your project's `raw` folder, it should be the only file with the extension of `ent.json`.

{% hint style="info" %}
If parts of the vehicle are missing, undo the import (ctrl+Z) and use `Export All` in Wolvenkit's Export Tool, then do it again.
{% endhint %}

At this point, you should have a full vehicle. The meshes should be

* aligned to the armature bones
* bound to special bones such as doors etc. via `ChildOf` constraints

You can find animations in the `dope sheet` > `action` editor. If you select the rig, you can select them from the dropdown to play them.

<details>

<summary>If you have misaligned parts</summary>

Have noticed some bits are still coming in slightly misaligned, but haven't worked out why yet. Steering wheels seem to be a common one, applying a copy rotation constraint to them aimed at the armature seems to fix them. The following code will apply one to everything selected, you may need to change the target object name.

```
import bpy
objs=bpy.context.selected_objects
for obj in objs:
    co=obj.constraints.new(type='COPY_ROTATION')
    co.target=bpy.data.objects['Armature']
```

</details>

I've built shaders for most of the materials that I've encountered in my testing. Exception is the dashboards, which are controlled by [inkwidgets](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators-theory/files-and-what-they-do/inkwidgets-a-custom-interface) rather than normal materials. If you want the texture, open the corresponding inkwidget in Wolvenkit, switch to the Preview tab and use the `Export to Images` button. You can now use this texture for the dashboard material's `BaseColor` attribute.

Importing multiple entities at once might be screwy. If you want several vehicles in a scene, import each into a separate blend file, then use File -> Append to merge them.

<figure><img src="../.gitbook/assets/image (1) (1) (2).png" alt=""><figcaption></figcaption></figure>
