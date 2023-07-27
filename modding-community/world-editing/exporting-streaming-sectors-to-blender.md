---
description: Exporting locations to Blender
---

# Editing locations in Blender

## Summary

**Created by @Simarilius** \
**Updated 19 March 2023 \~** [Simarilius](http://127.0.0.1:5000/u/G2MqNkfgTlQ1R3G4B5s6WefLjdy2 "mention")\
**Updated 7 May 2023 \~** [manavortex](http://127.0.0.1:5000/u/NfZBoxGegfUqB33J9HXuCs6PVaC3 "mention")\
**Script updated 1 June 2023 \~** [Simarilius](http://127.0.0.1:5000/u/G2MqNkfgTlQ1R3G4B5s6WefLjdy2 "mention")

The original exporter was based on some posts by **@123321** in the Discord _#mapeditor_ channel back in May, so all credit to him for working it out in the first place.

Theres a video which outlines this process [Here](https://youtu.be/JVCbPr67mgw).

### Versions and requirements

This guide was initially written with game version 1.6 of Cyberpunk 2077.

* [**Wolvenkit**](https://github.com/WolvenKit/WolvenKit) **>= 8.8.1 or the latest** [**Nightly**](https://github.com/WolvenKit/WolvenKit-nightly-releases/releases)
* [**Blender 3.3**](https://www.blender.org/) **or newer**
* [**Cyberpunk add-on for Blender 1.2.0**](https://github.com/WolvenKit/Cyberpunk-Blender-add-on/releases)

## Exporting Streaming Sectors to Blender

To export a location, you need to know its files — you can either [pick them from our list](interesting-sectors.md) or [go and find them](../../guides/modding-community/exporting-streaming-sectors-to-blender/finding-a-specific-sector.md) (and add them to the list, please).

Open the script manager by going Tools > Script Manager and open Export\_Sector.wscript (included in Wolvenkit >= 8.9.1). If you're on an older version of Wolvenkit, you should either update or install the latest [Nightly](https://github.com/WolvenKit/WolvenKit-nightly-releases/releases).

You have two options to export streaming sectors now:&#x20;

#### Run the script

This will export all .streamingsector files inside your project.

#### Adjust the script

You can filter your present sectors by adjusting the list at the top of the file:

```javascript
// You can add sectors to the list, or add them to the project 
// list of sector files (paths need double slashes) you can leave empty if in project
// can use just filenames if their in the _compiled\default folder
var sectors=[
    "interior_-48-31_2_0.streamingsector",
    "interior_-24-16_1_1.streamingsector",
]
```

This will add all the sector files and the files needed to export them to your project, and exported the files to json/glb.

{% hint style="success" %}
Depending on your computer and the sectors you're exporting, the script may take a few minutes. Just wait until the Stop button becomes inactive again and the Run button turns green.
{% endhint %}

{% hint style="info" %}
You might see a bunch of error messages about files that couldn't be found in the Wolvenkit log. Those usually only affect materials, your mesh should still show up in Blender, it will just be blank,
{% endhint %}

## Importing to Blender

1. Open Blender, then select `File` -> `Import` -> `Cyberpunk Streaming Sector`.

<figure><img src="../../.gitbook/assets/SSector_Import_1.png" alt=""><figcaption></figcaption></figure>

2. Select the `.cdmodproj` file in the root of your Wolvenkit project directory.
3. Wait - import may take a few minutes.
4. As the meshes will be scaled and positioned according to the map coordinates, they're probably off-screen. Since they are selected, you can hit `.` on the numpad (`/` on German keyboard), moving the camera to selection.

{% hint style="info" %}
The script will find all streamingsector .json files under the `raw` directory and import them. If you are editing multiple streaming sectors but want to import only one at a time, remove or rename the json files under `raw`.
{% endhint %}

TODO: \
There are still some node types in the sector file not being processed currently, or not fully instanced. These include **decals** (which just get an empty with details of what the decal is) and lights which I haven't gotten round to.&#x20;

<figure><img src="../../.gitbook/assets/El_Coyote_latest.png" alt=""><figcaption><p>Export of <em>El Coyote Cojo</em></p></figcaption></figure>

<figure><img src="../../.gitbook/assets/El_Coyote_latest_shaded.png" alt=""><figcaption><p>Export of <em>El Coyote Cojo, generated materials!</em></p></figcaption></figure>

## Importing back into Cyberpunk

1. Download this script ([raw link](https://raw.githubusercontent.com/Simarilius-uk/CP2077\_BlenderScripts/main/export\_to\_JSONs.py)) from [Sim's github](https://github.com/Simarilius-uk/CP2077\_BlenderScripts/blob/main/export\_to\_JSONs.py)&#x20;
2. Switch to Blender's scripting perspective and paste the code there
3. Adjust line 30 and change the path assigned to 'project' to the path of your cyberpunk project. Make sure to double the backslashes.\
   Example: \
   before:  `project = 'F:\\CPmod\\meshdecal_parralax'`\
   after:     `project = 'D:\\Cyberpunk_Modding\\world_editing\\myproject'`
4. In your Wolvenkit project's root folder, create the folder `output`
5. Run the script by clicking the ▷ button\
   _If the script throws errors and you can't resolve them on your own or with the help of ChatGPT, find us on_ [_Discord_](https://discord.gg/redmodding)_!_
6. Via Windows Explorer, copy the json file from the `output` directory in your Wolvenkit project over the file with the same name in the `raw` directory.
7. In Wolvenkit, right-click on the file you just copied and select "Import from json"
8. You're done!





