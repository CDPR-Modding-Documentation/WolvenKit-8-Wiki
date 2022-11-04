---
description: So we got Jackie out, can we make him move?
---

# Exporting Rigs & Anims

## Summary

**Created by @Simarilius** \
**Published October 15 2022**

This guide aims to walk you through adding the rig and some anims to the  character to blender previously exported. Guide is using nightly WolvenKit, Cyberpunk add-on for Blender 1.0.9, and Blender 3.3.

#### This guide uses the following versions:

* Cyberpunk 2077 game version 1.6
* Blender 3.3 stable
* Cyberpunk add-on for Blender 1.0.9rc1 (release has a bug)
* WolvenKit 8.7 nightly&#x20;

### Requirements

* [**WolvenKit nightly release version 8.7**](https://github.com/WolvenKit/WolvenKit) **or higher**&#x20;
* [**Blender 3.3**](https://www.blender.org/)
* [**Cyberpunk add-on for Blender 1.0.9**](https://github.com/dragonzkiller/cp77research) **or newer**

## Exporting to Blender

So exported characters are cool, but how do we get them out of that annoying pose? We need the rig, and maybe some animations.&#x20;

To be more specific, we need 2 rigs, the main body rig, and the head/face rig. We're going to bring them in, bind every thing to them, then attach the head to the body. (recapitate?!?)

First step is to locate the rigs and export them with the head and body. I'm going to carry on using Jackie as my example, the process should work for any character.

There is a head rig in Jackies folder with the same name as his head, probably the one we want, you'll want to make a note of the name as your going to need to type it into wkit:&#x20;

![](<../../../.gitbook/assets/SIM Jackie head rig.png>)

So we just need to locate the rig his body is using. Inside the components list of the  `jackie_welles.ent` file you'll find item 3 is deformations, which lists his rig as `man_big_deformations.rig.`

<figure><img src="../../../.gitbook/assets/SIM Jackie main rig.png" alt=""><figcaption></figcaption></figure>

So now we have the 2 rigs we need we need to rexport a couple of the parts, you want to do this after you already exported all the parts using withMaterials so that the material JSON and images have been generated as withRig doesnt do that.&#x20;

Select the body (`t0_001_mb_body__jackie_welles.mesh` in Jackies case) and double click the export Task to get at his options. Select WithRig as the mesh export type, then click the ... button on the far right in the Select Rig row down in the WithRig settings bit. In the panel that pops up you can type the name in the empty row below File Name at the top of the left column to filter it down, `man_big` was enough to let me select the `man_big_deformations.rig` that I need, then click the right pointing arrow on the divider to put it in the Selected Files column. Confirm back out of that and then confirm again at the top. Do the same process for your head mesh object to select the head rig. Now select just those two and process selected.

<figure><img src="../../../.gitbook/assets/SIM WithRig Export Settings.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/SIM Rig Selection.png" alt=""><figcaption></figcaption></figure>

Now import those freshly exported models into Blender, I'm gonna add them to the file I already created for the previous guide but if your doing this for the first time you may want to get this bit out the way first.&#x20;

So File>Import>Cyberpunk GLTF and pick the two files out.

Jackies an interesting example as his default appearance barely has any actual body, for some reason they just modelled his chest and hands, most characters bring full bodys in. If the WithRig has worked you should notice that rather than the mass of unorganised huge bones, you've got a skeleton structure that kinda makes sense. The head will have 2 massive bones that get rather in the way, so I normally change the bone display settings of that armature to Stick rather than Octahedral as it is by default.

![](<../../../.gitbook/assets/SIM Bone display.png>)

Now you can either do the next bit the manual way, and go through the skeletons working out which bones are in both and deleting the duplicates, then joining it and reparenting anything that got messed up in the deletions, or you can rename a couple of things and then use the script I wrote.&#x20;

Assuming your going for option b, rename the head Armature to HeadArmature, and the body Armature to BodyArmature. This is the orange dudes in the outliner, not the green dudes at the level below them.

&#x20;![](<../../../.gitbook/assets/SIM Renamed Armatures.png>)

Now create a new empty script and paste the script below in, Select the body Armature and hit run. The rigs should merge and the armature should disappear from one of the head object. (I've had some weird cases where it didnt associate right, and think its to do with not having the body selected when running it, still testing)

&#x20;

```python
#
# Merge exported head and body rig, you need to rename the armatures to HeadArmature and BodyArmature
# Script by Simarilius Oct 2022
# v1
import bpy
C = bpy.context
D = bpy.data

head = bpy.data.objects['HeadArmature']
body = bpy.data.objects['BodyArmature']
head_coll= head.users_collection[0]
dupes = []
relate={}

for bone in head.data.bones:
    if bone.name in body.data.bones.keys() and bone.name!='Root':
        dupes.append(bone.name)
        relate[bone.name]=bone.children.keys()

obs = bpy.context.scene.objects["HeadArmature"]   
obs.select_set(True) 
bpy.ops.object.mode_set(mode='EDIT')
for bone in dupes:
    bn=head.data.edit_bones[bone]
    head.data.edit_bones.remove(bn)

bpy.ops.object.mode_set(mode='OBJECT')

ob = bpy.context.scene.objects["BodyArmature"]  # Get the armature
bpy.ops.object.select_all(action='DESELECT')    # Deselect all objects
bpy.context.view_layer.objects.active = ob      # Make the armature the active object 
ob.select_set(True)                             # Select the armature

obs = [bpy.data.objects['BodyArmature'], bpy.data.objects['HeadArmature']]

c = {}
c["object"] = bpy.data.objects['BodyArmature']
c["active_object"] = bpy.data.objects['BodyArmature']
c["selected_objects"] = obs
c["selected_editable_objects"] = obs

with C.temp_override(active_object=c["active_object"], selected_editable_objects=obs):
    bpy.ops.object.join()

bpy.ops.object.mode_set(mode='EDIT')
for bn in dupes:
    for bone in relate[bn]:
        if bone not in body.data.bones[bn].children.keys():
            #print(bone)
            #child = body.data.bones[bone]
            if bone!='Root':
                body.data.edit_bones[bone].parent = body.data.edit_bones[bn]

bpy.ops.object.mode_set(mode='OBJECT')

for obj in head_coll.objects:
    obj.modifiers['Armature'].object=body

```



Hopefully it looks something like below, with all the bones selecting at once, and just the one green dude in the outliner named BodyArmature.

<figure><img src="../../../.gitbook/assets/SIM Merged Armatures.png" alt=""><figcaption></figcaption></figure>

At this point the only thing left to do is to associate all the other meshs to the rig, and to import some animations. If you have a lot of meshes you may want to skip down to the importing an anim and check your rig is behaving first.&#x20;

To associate other items, delete their armatures, then select each submesh item, and in the modifiers tab, select the Armature modifier and select your new BodyArmature as the object. This should snap the item to the body and it will follow with correct weights when animated. So go ahead and do that to all the other items that you imported if you followed the first guide (or follow the rest of it and come back)&#x20;

![](<../../../.gitbook/assets/SIM armature modifier.png>)

To find some anims to test with, in my case I've simply searched Jackie anim in the asset browser. if you do a search for just anim the list is huge, and a lot of them will work with anything using the right base skeleton to a decent degree. If you look inside your characters ent file the list of anims that the engine associates with them for general stuff like walking is inside the resolved dependancies bit.&#x20;

I recommend you avoid anims from the lip sync and facial tracking folders, they seem to go a bit nuts and I havent worked out how to make them usable (if you do let us know on Discord!)&#x20;

Once you find one you want to try, add it to your wkit project, export it from the import/export panel (no settings changes needed) and then import like any other glb file. you can hide the new armature once its imported.

Select your BodyArmature, go to the animation workspace, and in the dope sheet at the bottom change the drop down that says Dope Sheet to Action editor. Theres a drop down in the middle that lets you pick between the animations that you just imported. You can keep importing more anim files and the list just grows.&#x20;

Anyway, cheers Chooms, hope this has been helpful, have fun!

<figure><img src="../../../.gitbook/assets/SIM_Jackie_Cheers_0001-0298_AdobeExpress (2).gif" alt=""><figcaption></figcaption></figure>

Note:

Most of the animations seem to work flawlessly, some don't and I don't know enough about blender animation to know why, if anyone has a better idea whats going on please enlighten me! Occasionally the process gos screwy somewhere and the model freaks out when you attach the anims, I've mostly just repeated the process and its come out fine so I haven't worked out exactly whats causing that. As always happy to try and help on the Discord, normally in #textures-and-models.
