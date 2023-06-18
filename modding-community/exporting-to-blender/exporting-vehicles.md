---
description: Step-by-step guide for exporting vehicles to Blender
---

# Exporting Vehicles

## Summary

**Created by** [Simarilius](http://localhost:5000/u/G2MqNkfgTlQ1R3G4B5s6WefLjdy2 "mention") \
**Published May 2023**&#x20;

This guide aims to walk you through finding and exporting a vehicle to blender.&#x20;

#### This guide uses the following versions:

* Cyberpunk 2077 game version 1.61
* Blender 3.3 stable
* Cyberpunk add-on for Blender 1.3.0 (development build as of 26 May 2023 or newer)

### Requirements

* [**WolvenKit 8.9**](https://github.com/WolvenKit/WolvenKit) **or newer**
* [**Blender 3.3**](https://www.blender.org/) **or newer (hasnt been tested on older)**
* [**Cyberpunk add-on for Blender 1.3.0**](https://github.com/WolvenKit/Cyberpunk-Blender-add-on/releases) **or newer**

Vehicles have some different challenges than the characters, but the blender addon has been updated to deal with them, as long as you give it the right info.&#x20;

Importing vehicles to blender needs the ent, app & rig files as jsons, and all the meshes and the main anim file for the vehicle as glbs.&#x20;

{% hint style="info" %}
Ent files for pretty much all the vehicles are listed on the Cyberpunk modding wiki [here](https://wiki.redmodding.org/cyberpunk-2077-modding/modding-know-how/references-lists-and-overviews/files-for-modding/vehicles).
{% endhint %}

Once you've added the ent to your project you can either do the right click used files method to manually find and add the app, anim, rig and mesh files to the project or you can use the wscript below to do it automatically. Its set to ignore proxy, shadow & fx meshes, change the variables to true if you want them.

```javascript
// Entity export script FOR VEHICLES dont use if you dont need all the anims and rig.
// By Simarilius & DZK
// Exports ent files and all referenced files (recursively)
import * as Logger from 'Logger.wscript';

// Rather than a manual list does it for all ents in the project. 

var ents=[]
for (var filename of wkit.GetProjectFiles('archive')) {
        //Logger.Info(filename)
        var ext=filename.split('.').pop();
        if (ext === "ent") {
            ents.push(filename)
        }
    }
   
// sets of files that are parsed for processing
const parsedFiles = new Set()
const projectSet = new Set()
const exportSet = new Set()
const jsonSet = new Set()
const rigs = new Map()

// Set these to true if you want proxys/shadow meshes
var include_proxys=false
var include_shadows=false
var include_fx=false

// loop over every entity in `ents` and find rigs
for (var ent in ents) {
    Logger.Info('Finding rigs in '+ ents[ent])
    FindEntRigs(ents[ent])
    FindEntAnims(ents[ent])
    Logger.Info('')
    for (const [key, value] of rigs) 
    {
  	Logger.Info(`${key} = ${value}`);
  	if (value.includes("base_rig")!=true){
  	    projectSet.add(value)
            jsonSet.add(value)
  	}
	}
    Logger.Info('')
}
// now find the mesh files
for (var ent in ents) {
    Logger.Info(ents[ent])
    ParseFile(ents[ent])
}

// save all our files to the project and export JSONs
for (const fileName of projectSet) {
        // skip shadows if the variable is set
	if ((include_shadows==false) && (fileName.includes("shadow"))){
		continue
		}
	// skip proxies if the variable is set
	if ((include_proxys==false) && (fileName.includes("proxy"))){
		continue
		}
	// skip fx bodies if the variable is set
	if ((include_fx==false) && (fileName.includes("fx"))){
		continue
		}
    var file = wkit.GetFileFromBase(fileName)
    wkit.SaveToProject(fileName, file)

    if (jsonSet.has(fileName)) {
        var path = ""
        if (file.Extension === ".ent") {
            path = wkit.ChangeExtension(file.Name, ".ent.json")
        }
        if (file.Extension === ".app") {
            path = wkit.ChangeExtension(file.Name, ".app.json")
        }
        if (file.Extension === ".rig") {
            path = wkit.ChangeExtension(file.Name, ".rig.json")
        }
        if (path.length > 0) {
            var json = wkit.GameFileToJson(file)
            wkit.SaveToRaw(path, json)
        }
    }
}

// export all of our files with the default export settings
wkit.ExportFiles([...exportSet])


// begin helper functions
function* GetPaths(jsonData) {
    for (let [key, value] of Object.entries(jsonData || {})) {
        if (key === "DepotPath" && value != null && value != 0) {
            yield value;
        }

        if (typeof value === "object") {
            yield* GetPaths(value)
        }
    }
}

// Parse a CR2W file
function ParseFile(fileName) {
    // check if we've already worked with this file and that it's actually a string
    if (parsedFiles.has(fileName) || typeof fileName !== "string") {
        return
    }
    parsedFiles.add(fileName)
	var ext=fileName.split('.').pop();
	if (ext==='mesh' || ext==='app' || ext==='ent'){
    // try to get the file
    var file = wkit.GetFileFromBase(fileName)
    if (file === null) {
        Logger.Error(fileName + " could not be found")
        return
    }
    
    // handle the file types we want
    if (file.Extension === ".mesh") {
        projectSet.add(fileName)
        exportSet.add(fileName)
        // meshes need json'ing too for the bits with 
        jsonSet.add(fileName)
    }
    if (file.Extension === ".ent") {
        projectSet.add(fileName)
        jsonSet.add(fileName)
    }
    if (file.Extension === ".app") {
        projectSet.add(fileName)
        jsonSet.add(fileName)
    }
    if (file.Extension === ".anim") {
        projectSet.add(fileName)
        exportSet.add(fileName)
    }
    if (file.Extension === ".rig") {
        projectSet.add(fileName)
        jsonSet.add(fileName)
    }

    // now check if there are referenced files and parse them
    if (file.Extension === ".app" || file.Extension === ".ent" || file.Extension === ".mesh" ){
	    var json = JSON.parse(wkit.GameFileToJson(file))
	    for (let path of GetPaths(json["Data"]["RootChunk"])) {
	        ParseFile(path)
		}
    }
    }
}

// Parse a ent file for rigs
function FindEntRigs(fileName) {
	var file = wkit.GetFileFromBase(fileName)
	var json = JSON.parse(wkit.GameFileToJson(file))
	//find the rigs in the base ent components (normally root and deformations)
	for (let comp of json["Data"]["RootChunk"]["components"]) {
		if (!("rig" in comp)==0)
		{
		//Logger.Info(comp["name"])
		//Logger.Info(comp["rig"]["DepotPath"])
		rigs.set(comp["name"],comp["rig"]["DepotPath"])
		}
	}
	// find any rigs referenced in the appearances (head and dangle)
	for (let app of json["Data"]["RootChunk"]["appearances"])
	{
		var appfileName=app["appearanceResource"]["DepotPath"]
		//Logger.Info(appfileName)
		var appfile = wkit.GetFileFromBase(appfileName)
		var appjson = JSON.parse(wkit.GameFileToJson(appfile))
		for (let appApp of appjson["Data"]["RootChunk"]["appearances"])
		{
				for (let appcomp of appApp["Data"]["components"]) 
				{
					if (!("rig" in appcomp)==0)
					{
					//Logger.Info(appcomp["name"])
					//Logger.Info(appcomp["rig"]["DepotPath"])
					rigs.set(appcomp["name"],appcomp["rig"]["DepotPath"])
					}
				}	
		}			
	}
}

// Parse a ent file for rigs
function FindEntAnims(fileName) {
	var file = wkit.GetFileFromBase(fileName)
	var json = JSON.parse(wkit.GameFileToJson(file))
	//find the anims in the ent resolved dependencies
	for (let dep of json["Data"]["RootChunk"]["resolvedDependencies"]) {
		Logger.Info(dep["DepotPath"])
		projectSet.add(dep["DepotPath"])
		exportSet.add(dep["DepotPath"])
	}
}

function get_filename(str) {
    return str.split('\\').pop().split('/').pop();
}
```

Once the ent, app and rig files are json'd and the rest exported to glb, simply use the Cyberpunk Entity import option and select the entity json file. To get a specific appearance you need to enter it in the text entry in the blender open dialog, otherwise you get the default. it's the appearanceName from inside the appearance entry in the appearances list in the entity file that you need to put in there.

<img src="../../.gitbook/assets/image.png" alt="" data-size="original">

The vehicle should be imported, with the meshes aligned to the bones and with ChildOf constraints applied to the bones that their meant to be bound to so that the doors etc work if you play the anims. Anims can be found in the dope sheet>action editor, then use the drop down list with the rig selected.

Have noticed some bits are still coming in slightly misaligned, but haven't worked out why yet. Steering wheels seem to be a common one, applying a copy rotation constraint to them aimed at the armature seems to fix them. The following code will apply one to everything selected, you may need to change the target object name.

```
import bpy
objs=bpy.context.selected_objects
for obj in objs:
    co=obj.constraints.new(type='COPY_ROTATION')
    co.target=bpy.data.objects['Armature']
```

I've built shaders for most of the materials that I've encountered in my testing. Exception is the dashboards, their driven by inkwidgets not normal materials, so aren't implemented, if you want them then dig in the interior\_ui component in the applicable appearance, then open the inkwidget and in the preview use the export to images button to export a bitmap. Import that as the basecolor on the material on the dash.

Importing multiple ents to the same file may go screwy, not isolated why, if you want multiple vehicles together in a scene then import each to a separate blend and append the blends.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
