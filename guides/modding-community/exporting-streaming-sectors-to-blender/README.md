---
description: Exporting locations to Blender
---

# Exporting Streaming Sectors to Blender

## Summary

**Created by @Simarilius** \
**Updated September 27 2022**

This is very much a work in progress, and only gets Streaming Sectors out and into Blender so far. Based on some posts by @123321 in the Discord _#mapeditor_ channel back in May, so all credit to him for working it out in the first place.

#### This guide uses the following versions:

* Cyberpunk 2077 game version 1.6
* WolvenKit-8.7.0-nightly.2022-10-26 or newer
* Blender 3.3 stable
* Cyberpunk add-on for Blender 1.0.9

### Requirements

* [**WolvenKit nightly release version 8.7**](https://github.com/WolvenKit/WolvenKit) **(use the latest)**
* [**Blender 3.3**](https://www.blender.org/)****
* [**Cyberpunk add-on for Blender 1.0.9**](https://github.com/WolvenKit/Cyberpunk-Blender-add-on)

## Background on Streaming Sectors

So Streaming Sectors are the files that define the world to the Cyberpunk Engine, and contain the data to point to all the models and entities that populate it. There are several types of Streaming Sector, including ones to define navigation, sound collision bodies and illumination, but the ones we're dealing with here are primarily the interior and exterior ones.

The world is broken up into a grid, with several sizes of squares available (bit like graph paper with major and minor grid lines). The size of the grid in use is dependent on the Level of Detail (LOD) of the sector file your looking at, which is the last digit of the filename. Chunk sizes are as below.

| LOD | Interior | Exterior |
| --- | -------- | -------- |
| 0   | 32       | 64       |
| 1   | 64       | 128      |
| 2   | 128      | 256?     |

For every location there can be multiple levels of LOD sectors overlapping, with progressively more detail defined as you go down the levels, so for instance Lizzies bar, is located at approximately -1200, 1562, 22 as you can see from the screenshot below of interrogating the bouncers position with AMM.&#x20;

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Filenames are   `sectortype_X_Y_Z.streamingsector`  in the AMM co-ords. If you preview a sector in wkit the axes are shown rotated so Z=-Y and Y=Z.

From those co-ordinates we can calculate the sector files for interior/exterior sectors by dividing by the grid size for the LOD and rounding. (ie 1200/32=38 etc)

| LOD | Interior   | Exterior   |
| --- | ---------- | ---------- |
| 0   | -38\_49\_0 | -19\_24\_0 |
| 1   | -19\_24\_0 | -9\_12\_0  |
| 2   | -9\_12\_0  | -5\_6\_0   |

At the level 0 files the whole building isn't covered by 1 sector, so you end up needing 4, conversely the exterior level 2 is several city blocks. In the end to totally define the bar you need the following as far as I can tell

![](<../../../.gitbook/assets/image (2).png>)

In some locations bit are defined inside quest sectors that have bunch of bits to do with triggering the story bits that occur there, half vs apartment seems to be tucked away inside several of those. Their something todo with the nodeRefs inside the main sector files, but I'm still trying to work out how to work out one from the other.

An easy way to locate sectors from inside wkit is if theres anything unique in the location, if you find the mesh then use 'Find files using this' to track back to the streaming sector. So for instance to find El Coyote has the sign which is findable with a search for coyote as el\_coyote\_cojo\_bar\_signage\_a.mesh _._ From that you can do used by to find interior\_-20\_-16\_0\_1.streamingsector. Thats the Level 1 LOD sector though, which just has the big stuff, you also need the LOD 0 ones, which are done on a chunk size half the size, so the numbers in the filename double. For El Coyote these are interior\_-39\_-31\_0\_0.streamingsector, interior\_-39\_-32\_0\_0.streamingsector, interior\_-40\_-31\_0\_0.streamingsector & interior\_-40\_-32\_0\_0.streamingsector.

The other approach is to go in game and use CET and AMM to interrogate an entity at the location and use the director tools to get its world co-ords. So el coyote is at approx x,y,z of -1260,-996,12. Dividing those by 64 and rounding (not sure how they decide that) gets us -20 -16 0 for the filename above.&#x20;

You can preview the sectors in wolvenkit to confirm their what you're after.

## Exporting Streaming Sectors to Blender

Once you've found the location you want to export, add the sectors to your project, then right click and export to JSON. You can right click the folder in the project explorer to export all sectors inside to JSON.

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Now right click the sector in the Asset Browser and do Find Used Files&#x20;

<figure><img src="../../../.gitbook/assets/image (3) (2).png" alt=""><figcaption></figcaption></figure>

Filter by kind then select all the mesh files and add to your project. Repeat these steps for each streaming sector that you added.

Goto the import/export tool, double click a mesh and switch to withMaterials if you want to use them, and turn LOD off. Then apply to all of this kind, and process all.

## With Materials

If you want to have meshes with materials, follow this section, otherwise skip down to the just meshes bit below. It may be worth doing the just the meshes first to check you've got all the files and so on, the with Materials bit can take quite some time, so doing it the other way first to check is a sensible idea.

Time to fire up Blender, I'm using 3.3. Create an empty file, and go to the scripting page. Paste the script below into a new script.

```python
import json
import glob
import os
import bpy
from pathlib import Path

# Print iterations progress
def printProgressBar (iteration, total, prefix = '', suffix = '', decimals = 1, length = 100, fill = '█', printEnd = "\r"):
    """
    Call in a loop to create terminal progress bar
    @params:
        iteration   - Required  : current iteration (Int)
        total       - Required  : total iterations (Int)
        prefix      - Optional  : prefix string (Str)
        suffix      - Optional  : suffix string (Str)
        decimals    - Optional  : positive number of decimals in percent complete (Int)
        length      - Optional  : character length of bar (Int)
        fill        - Optional  : bar fill character (Str)
        printEnd    - Optional  : end character (e.g. "\r", "\r\n") (Str)
    Thanks Greenstick:    
    https://stackoverflow.com/questions/3173320/text-progress-bar-in-terminal-with-block-characters
    """
    percent = ("{0:." + str(decimals) + "f}").format(100 * (iteration / float(total)))
    filledLength = int(length * iteration // total)
    bar = fill * filledLength + '-' * (length - filledLength)
    print(f'\r{prefix} |{bar}| {percent}% {suffix}', end = printEnd)
    # Print New Line on Complete
    if iteration == total: 
        print()

path = 'F:\\CPmod\\coyote\\source\\raw\\base'

C = bpy.context
coll_scene = C.scene.collection
if 'MasterInstances' in  coll_scene.children.keys():
    Masters=bpy.data.collections['MasterInstances']
else:
    Masters=bpy.data.collections.new("MasterInstances")
    coll_scene.children.link(Masters)

# Set target collection to a known collection 
coll_target = coll_scene.children.get("MasterInstances")

meshes =  glob.glob(path+"\**\*.glb", recursive = True)
total=len(meshes)
print(total)
i=0
printProgressBar(i, total, prefix = 'Progress:', suffix = 'Complete', length = 50)
for m,mesh in enumerate(meshes):
    if Path(mesh).stem not in Masters.children.keys():
        try:
           bpy.ops.io_scene_gltf.cp77(filepath=mesh)
           objs = C.selected_objects
           move_coll= coll_scene.children.get( objs[0].users_collection[0].name )
           coll_target.children.link(move_coll) 
           coll_scene.children.unlink(move_coll)
        except:
            print("Failed on ",mesh)
        i=i+1
        printProgressBar(i, total, prefix = 'Progress:', suffix = 'Complete', length = 50)
        #Uncomment the lines below to save the blend file every 100 imports
        #if (m % 100==0):
        #    bpy.ops.wm.save_mainfile()
            
```

Set the path variable to the project raw folder. In the Window menu, select toggle system console so its visible, then run it. That will pull all the glbs in your project into the Blender file, including materials. These will be put in a Collection called MasterInstances, if there are any that arent (I get some random unnamed meshes, not worked out why yet) I tend to tidy them into another collector, but DONT delete them. This step may take a while as loading the meshes with materials isn't the fastest process, the system console should show its progress, and if you need to kill it select the console and hold down Ctrl+C till it stops.&#x20;

After this add a second script to the file, and paste the script below in it.

```python
import json
import glob
import os
import bpy
C = bpy.context
path = 'F:\\CPmod\\coyote\\source\\raw'

Masters = bpy.context.scene.collection.children.get("MasterInstances")

jsonpath = glob.glob(path+"\**\*.streamingsector.json", recursive = True)

for filepath in jsonpath:    
    with open(filepath,'r') as f: 
          j=json.load(f) 
          
    t=j['Data']['RootChunk']['nodeData']['Data']
          
    meshes =  glob.glob(path+"\**\*.glb", recursive = True)
    
    glbnames = [ os.path.basename(x) for x in meshes]
    meshnames = [ os.path.splitext(x)[0]+".mesh" for x in glbnames]
    
    nodes = j["Data"]["RootChunk"]["nodes"]
    print(len(nodes))
    for i,e in enumerate(nodes):
    
        #if i > 2: break
        data = e['Data']
        type = data['$type']
        
        match type:
            case 'worldEntityNode': 
                print('worldEntityNode',i)
                pass
            case 'worldInstancedMeshNode':
                #print('worldInstancedMeshNode')
                meshname = data['mesh']['DepotPath'] 
                num=data['worldTransformsBuffer']['numElements']
                start=data['worldTransformsBuffer']['startIndex']
                if(meshname != 0):
                                #print('Mesh - ',meshname, ' - ',i, e['HandleId'])
                                groupname = os.path.splitext(os.path.split(meshname)[-1])[0]
                                group=Masters.children.get(groupname)
                                if (group):
                                    print('Group found for ',groupname)                               
                                    for i in range(start, start+num):
                                        #create the linked copy of the group of mesh
                                        
                                        new=bpy.data.collections.new(groupname)
                                        C.scene.collection.children.link(new)
                                        
                                        for old_obj in group.all_objects:                            
                                            obj=old_obj.copy()  
                                            new.objects.link(obj)                                    
                                            if 'Data' in data['worldTransformsBuffer']['sharedDataBuffer'].keys():
                                                inst_trans=data['worldTransformsBuffer']['sharedDataBuffer']['Data']['buffer']['Data']['Transforms'][i]
                                                       
                                            elif 'HandleRefId' in data['worldTransformsBuffer']['sharedDataBuffer'].keys():
                                                bufferID = int(data['worldTransformsBuffer']['sharedDataBuffer']['HandleRefId'])
                                                ref=e
                                                for n in nodes:
                                                    if n['HandleId']==str(bufferID-1):
                                                        ref=n
                                                inst_trans = ref['Data']['worldTransformsBuffer']['sharedDataBuffer']['Data']['buffer']['Data']['Transforms'][i]       
                                            else :
                                                print(e)
                                            obj.location.x = inst_trans['translation']['X'] /100
                                            obj.location.y = inst_trans['translation']['Y'] /100
                                            obj.location.z = inst_trans['translation']['Z'] /100
                                            if obj.location.x == 0:
                                                print('Mesh - ',meshname, ' - ',i,'HandleId - ', e['HandleId'])      
                                            
                                            #print(i,obj.name,' x= ',obj.location.x, ' y= ', obj.location.y, ' z= ',obj.location.z)
                                     
                                            obj.rotation_quaternion.x = inst_trans['rotation']['i']
                                            obj.rotation_quaternion.y = inst_trans['rotation']['j']
                                            obj.rotation_quaternion.z = inst_trans['rotation']['k']
                                            obj.rotation_quaternion.w = inst_trans['rotation']['r']
                                            
                                            obj.scale.x = inst_trans['scale']['X'] /100
                                            obj.scale.y = inst_trans['scale']['Y'] /100
                                            obj.scale.z = inst_trans['scale']['Z'] /100
                                                    
                                else:
                                    print('Mesh not found - ',meshname, ' - ',i, e['HandleId'])
                                                
            case 'worldDecorationMeshNode': 
                #print('worldDecorationMeshNode',i)
                pass
            case 'worldInstancedOccluderNode':
                #print('worldInstancedOccluderNode')
                pass
            case 'worldStaticDecalNode':
                #print('worldStaticDecalNode')
                pass
            case 'worldStaticOccluderMeshNode':
                #print('worldStaticOccluderMeshNode',i)
                pass
            case 'worldCollisionNode':
                #print('worldCollisionNode',1)
                pass
            case 'worldStaticMeshNode': 
                if isinstance(e, dict) and 'mesh' in data.keys():
                    meshname = data['mesh']['DepotPath']
                    #print('Mesh name is - ',meshname, e['HandleId'])
                    if(meshname != 0):
                                #print('Mesh - ',meshname, ' - ',i, e['HandleId'])
                                groupname = os.path.splitext(os.path.split(meshname)[-1])[0]
                                group=Masters.children.get(groupname)
                                if (group):
                                    print('Group found for ',groupname) 
                                    instances = [x for x in t if x['NodeIndex'] == i]
                                    for inst in instances:
                                        new=bpy.data.collections.new(groupname)
                                        C.scene.collection.children.link(new)
                                        
                                        for old_obj in group.all_objects:                            
                                            obj=old_obj.copy()  
                                            new.objects.link(obj)                             
                                            
                                            if 'Properties' in inst['Position'].keys():
                                                obj.location.x = inst['Position']['Properties']['X'] /100
                                                obj.location.y = inst['Position']['Properties']['Y'] /100
                                                obj.location.z = inst['Position']['Properties']['Z'] /100          
                                            else:
                                                obj.location.x = inst['Position']['X'] /100
                                                obj.location.y = inst['Position']['Y'] /100
                                                obj.location.z = inst['Position']['Z'] /100
                                            if obj.location.x == 0:
                                                print('Mesh - ',meshname, ' - ',i,'HandleId - ', e['HandleId'])      
                                            
                                           #print(i,obj.name,' x= ',obj.location.x, ' y= ', obj.location.y, ' z= ',obj.location.z)
                                            if 'Properties' in inst['Orientation'].keys():
                                                obj.rotation_quaternion.x = inst['Orientation']['Properties']['i']
                                                obj.rotation_quaternion.y = inst['Orientation']['Properties']['j']
                                                obj.rotation_quaternion.z = inst['Orientation']['Properties']['k']
                                                obj.rotation_quaternion.w = inst['Orientation']['Properties']['r']
                                            else:                                    
                                                obj.rotation_quaternion.x = inst['Orientation']['i']
                                                obj.rotation_quaternion.y = inst['Orientation']['j']
                                                obj.rotation_quaternion.z = inst['Orientation']['k']
                                                obj.rotation_quaternion.w = inst['Orientation']['r']
                                            if 'Properties' in inst['Scale'].keys():                       
                                                obj.scale.x = inst['Scale']['Properties']['X'] /100
                                                obj.scale.y = inst['Scale']['Properties']['Y'] /100
                                                obj.scale.z = inst['Scale']['Properties']['Z'] /100
                                            else:
                                                obj.scale.x = inst['Scale']['X'] /100
                                                obj.scale.y = inst['Scale']['Y'] /100
                                                obj.scale.z = inst['Scale']['Z'] /100
                                else:
                                    print('Mesh not found - ',meshname, ' - ',i, e['HandleId'])
                                  
            case 'worldInstancedDestructibleMeshNode':
                #print('worldInstancedDestructibleMeshNode',i)
                if isinstance(e, dict) and 'mesh' in data.keys():
                    meshname = data['mesh']['DepotPath']
                    #print('Mesh name is - ',meshname, e['HandleId'])
                    if(meshname != 0):
                                #print('Mesh - ',meshname, ' - ',i, e['HandleId'])
                                groupname = os.path.splitext(os.path.split(meshname)[-1])[0]
                                group=Masters.children.get(groupname)
                                if (group):
                                    #print('Glb found - ',glbfoundname)     
                                    #print('Glb found, looking for instances of ',i)
                                    instances = [x for x in t if x['NodeIndex'] == i]
                                    for inst in instances:
                                        #print('Inst - ',i, ' - ',meshname)
                                        
                                        new=bpy.data.collections.new(groupname)
                                        C.scene.collection.children.link(new)
                                        
                                        for old_obj in group.all_objects:                            
                                            obj=old_obj.copy()  
                                            new.objects.link(obj)   
                                            
                                            if 'Properties' in inst['Position'].keys():
                                                obj.location.x = inst['Position']['Properties']['X'] /100
                                                obj.location.y = inst['Position']['Properties']['Y'] /100
                                                obj.location.z = inst['Position']['Properties']['Z'] /100          
                                            else:
                                                obj.location.x = inst['Position']['X'] /100
                                                obj.location.y = inst['Position']['Y'] /100
                                                obj.location.z = inst['Position']['Z'] /100
                                            if obj.location.x == 0:
                                                print('Mesh - ',meshname, ' - ',i,'HandleId - ', e['HandleId'])      
                                            
                                           #print(i,obj.name,' x= ',obj.location.x, ' y= ', obj.location.y, ' z= ',obj.location.z)
                                            if 'Properties' in inst['Orientation'].keys():
                                                obj.rotation_quaternion.x = inst['Orientation']['Properties']['i']
                                                obj.rotation_quaternion.y = inst['Orientation']['Properties']['j']
                                                obj.rotation_quaternion.z = inst['Orientation']['Properties']['k']
                                                obj.rotation_quaternion.w = inst['Orientation']['Properties']['r']
                                            else:                                    
                                                obj.rotation_quaternion.x = inst['Orientation']['i']
                                                obj.rotation_quaternion.y = inst['Orientation']['j']
                                                obj.rotation_quaternion.z = inst['Orientation']['k']
                                                obj.rotation_quaternion.w = inst['Orientation']['r']
                                            if 'Properties' in inst['Scale'].keys():                       
                                                obj.scale.x = inst['Scale']['Properties']['X'] /100
                                                obj.scale.y = inst['Scale']['Properties']['Y'] /100
                                                obj.scale.z = inst['Scale']['Properties']['Z'] /100
                                            else:
                                                obj.scale.x = inst['Scale']['X'] /100
                                                obj.scale.y = inst['Scale']['Y'] /100
                                                obj.scale.z = inst['Scale']['Z'] /100
                                else:
                                    print('Mesh not found - ',meshname, ' - ',i, e['HandleId'])
                                            
            case _:
                print('None of the above',i)
                
                pass
    print('Finished with ',filepath)
print('Finished')

```

The path variable needs to point to the raw folder of the project that you extracted your meshes and streamingsectors to. I suggest doing window>toggle system console before running it if you didnt earlier already so you can see the output to check its running or kill it if needed.

Run the script and it should instance the meshes, and position them all. I'm doing it via instances as if you just pull meshes with materials in for each item the script takes 6+hrs to pull in Coyote Cojo. This may be a problem for modding in terms of getting it back into Cyberpunk, so I do have a version that can pull meshes in and I've put a switch that lets you turn on or off the material import, as the time difference is huge, just meshes takes 30 secs or so, with materials is at an several hours. That version is in the next section of this tutorial.

The meshes are scaled and positioned based on the map co-ords, so come in kinda small and off in a weird place. Hide the MeshInstances Collector, then do A to select all and . on the keypad to frame selected and you should hopefully see it.

As you can see in the script there are several node types in the sector file not being processed currently, and these included decals and decoration meshes that add the detail to the scene, but the bones of it are there with the above script. Havent done foliage yet either. Will try and get these extras added soon. The code is not by any stretch of the imagination optimised, but it mostly works.

It doesn't bring in things that are entities, so the ceiling fans & burrito machines for instance, but the meshes for those aren't linked from the scene itself, so adding that level of understanding may be a push. May look at adding named empties at the locations and doing another script that can pull meshes in later.

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

## Just the Meshes

The code below does the import without using linked duplicates, no need for the first script, and you can export without materials. The bool property at the start will let you explicitly not import materials. I STRONGLY advise against using this withMaterials, as its orders of magnitude slower to import. I've updated it to handle multiple streamingsectors in one go.

fire up Blender, I'm using 3.3. Create an empty file, and go to the scripting page. Paste the script below into a new script.

```python
import json
import glob
import os
import bpy
path = 'F:\\CPmod\\coyote\\source\\raw'

withMaterials=False

meshes =  glob.glob(path+"\**\*.glb", recursive = True)
glbnames = [ os.path.basename(x) for x in meshes]
meshnames = [ os.path.splitext(x)[0]+".mesh" for x in glbnames]

jsonpath = glob.glob(path+"\**\*.streamingsector.json", recursive = True)
for filepath in jsonpath:
    with open(filepath,'r') as f: 
          j=json.load(f) 
    t=j['Data']['RootChunk']['nodeData']['Data']
    nodes = j["Data"]["RootChunk"]["nodes"]
    #print(len(nodes))
    for i,e in enumerate(nodes):

        #if i > 2: break
        data = e['Data']
        type = data['$type']
        
        match type:
            case 'worldEntityNode': 
                print('worldEntityNode',i)
                pass
            case 'worldInstancedMeshNode':
                #print('worldInstancedMeshNode')
                meshname = data['mesh']['DepotPath'] 
                num=data['worldTransformsBuffer']['numElements']
                start=data['worldTransformsBuffer']['startIndex']
                if(meshname != 0):
                                #print('Mesh - ',meshname, ' - ',i, e['HandleId'])
                                glbfoundname = [ x for x in meshes if os.path.splitext(str(meshname))[0] in x] 
                                if(len(glbfoundname) == 1):
                                    #print('Glb found - ',glbfoundname)     
                                    
                                    for i in range(start, start+num):
                                        if withMaterials:
                                            try:
                                                bpy.ops.io_scene_gltf.cp77(filepath=glbfoundname[0])                                        
                                            except:
                                                bpy.ops.import_scene.gltf(filepath=glbfoundname[0])
                                        else:
                                            bpy.ops.import_scene.gltf(filepath=glbfoundname[0])
                                         
                                        objects = bpy.context.selected_objects
                                        for obj in objects:                            
                                            nn= str(data['debugName']).replace('{','').replace('}','')
                                            nn = [nn[1:],nn][nn[0].isalnum()]
                                            #print(nn)                            
                                            obj.name = nn
                                            #print(inst['Position'].keys())
                                            
                                            if 'Data' in data['worldTransformsBuffer']['sharedDataBuffer'].keys():
                                                inst_trans=data['worldTransformsBuffer']['sharedDataBuffer']['Data']['buffer']['Data']['Transforms'][i]
                                                       
                                            elif 'HandleRefId' in data['worldTransformsBuffer']['sharedDataBuffer'].keys():
                                                bufferID = int(data['worldTransformsBuffer']['sharedDataBuffer']['HandleRefId'])
                                                ref=e
                                                for n in nodes:
                                                    if n['HandleId']==str(bufferID-1):
                                                        ref=n
                                                inst_trans = ref['Data']['worldTransformsBuffer']['sharedDataBuffer']['Data']['buffer']['Data']['Transforms'][i]       
                                            else :
                                                print(e)
                                            obj.location.x = inst_trans['translation']['X'] /100
                                            obj.location.y = inst_trans['translation']['Y'] /100
                                            obj.location.z = inst_trans['translation']['Z'] /100
                                            if obj.location.x == 0:
                                                print('Mesh - ',meshname, ' - ',i,'HandleId - ', e['HandleId'])      
                                            
                                            #print(i,obj.name,' x= ',obj.location.x, ' y= ', obj.location.y, ' z= ',obj.location.z)
                                     
                                            obj.rotation_quaternion.x = inst_trans['rotation']['i']
                                            obj.rotation_quaternion.y = inst_trans['rotation']['j']
                                            obj.rotation_quaternion.z = inst_trans['rotation']['k']
                                            obj.rotation_quaternion.w = inst_trans['rotation']['r']
                                            
                                            obj.scale.x = inst_trans['scale']['X'] /100
                                            obj.scale.y = inst_trans['scale']['Y'] /100
                                            obj.scale.z = inst_trans['scale']['Z'] /100
                                                    
                                else:
                                    print('Mesh not found - ',meshname, ' - ',i, e['HandleId'])
                                                
            case 'worldDecorationMeshNode': 
                #print('worldDecorationMeshNode',i)
                pass
            case 'worldInstancedOccluderNode':
                #print('worldInstancedOccluderNode')
                pass
            case 'worldStaticDecalNode':
                #print('worldStaticDecalNode')
                pass
            case 'worldStaticOccluderMeshNode':
                #print('worldStaticOccluderMeshNode',i)
                pass
            case 'worldCollisionNode':
                #print('worldCollisionNode',1)
                pass
            case 'worldStaticMeshNode': 
                if isinstance(e, dict) and 'mesh' in data.keys():
                    meshname = data['mesh']['DepotPath']
                    #print('Mesh name is - ',meshname, e['HandleId'])
                    if(meshname != 0):
                                #print('Mesh - ',meshname, ' - ',i, e['HandleId'])
                                glbfoundname = [ x for x in meshes if os.path.splitext(str(meshname))[0] in x] 
                                if(len(glbfoundname) == 1):
                                    #print('Glb found - ',glbfoundname)     
                                    #print('Glb found, looking for instances of ',i)
                                    instances = [x for x in t if x['NodeIndex'] == i]
                                    for inst in instances:
                                        #print('Inst - ',i, ' - ',meshname)
                                        
                                        if withMaterials:
                                            try:
                                                bpy.ops.io_scene_gltf.cp77(filepath=glbfoundname[0])                                        
                                            except:
                                                bpy.ops.import_scene.gltf(filepath=glbfoundname[0])
                                        else:
                                            bpy.ops.import_scene.gltf(filepath=glbfoundname[0])
                                        
                                        objects = bpy.context.selected_objects
                                        #obj = bpy.context.object
                                        #print(data.keys())
                                        for obj in objects:                            
                                            nn= str(data['debugName']).replace('{','').replace('}','')
                                            nn = [nn[1:],nn][nn[0].isalnum()]
                                            #print(nn)                            
                                            obj.name = nn
                                            #print(inst['Position'].keys())
                                            if 'Properties' in inst['Position'].keys():
                                                obj.location.x = inst['Position']['Properties']['X'] /100
                                                obj.location.y = inst['Position']['Properties']['Y'] /100
                                                obj.location.z = inst['Position']['Properties']['Z'] /100          
                                            else:
                                                obj.location.x = inst['Position']['X'] /100
                                                obj.location.y = inst['Position']['Y'] /100
                                                obj.location.z = inst['Position']['Z'] /100
                                            if obj.location.x == 0:
                                                print('Mesh - ',meshname, ' - ',i,'HandleId - ', e['HandleId'])      
                                            
                                           #print(i,obj.name,' x= ',obj.location.x, ' y= ', obj.location.y, ' z= ',obj.location.z)
                                            if 'Properties' in inst['Orientation'].keys():
                                                obj.rotation_quaternion.x = inst['Orientation']['Properties']['i']
                                                obj.rotation_quaternion.y = inst['Orientation']['Properties']['j']
                                                obj.rotation_quaternion.z = inst['Orientation']['Properties']['k']
                                                obj.rotation_quaternion.w = inst['Orientation']['Properties']['r']
                                            else:                                    
                                                obj.rotation_quaternion.x = inst['Orientation']['i']
                                                obj.rotation_quaternion.y = inst['Orientation']['j']
                                                obj.rotation_quaternion.z = inst['Orientation']['k']
                                                obj.rotation_quaternion.w = inst['Orientation']['r']
                                            if 'Properties' in inst['Scale'].keys():                       
                                                obj.scale.x = inst['Scale']['Properties']['X'] /100
                                                obj.scale.y = inst['Scale']['Properties']['Y'] /100
                                                obj.scale.z = inst['Scale']['Properties']['Z'] /100
                                            else:
                                                obj.scale.x = inst['Scale']['X'] /100
                                                obj.scale.y = inst['Scale']['Y'] /100
                                                obj.scale.z = inst['Scale']['Z'] /100
                                else:
                                    print('Mesh not found - ',meshname, ' - ',i, e['HandleId'])
                                  
            case 'worldInstancedDestructibleMeshNode':
                #print('worldInstancedDestructibleMeshNode',i)
                if isinstance(e, dict) and 'mesh' in data.keys():
                    meshname = data['mesh']['DepotPath']
                    #print('Mesh name is - ',meshname, e['HandleId'])
                    if(meshname != 0):
                                #print('Mesh - ',meshname, ' - ',i, e['HandleId'])
                                glbfoundname = [ x for x in meshes if os.path.splitext(str(meshname))[0] in x] 
                                if(len(glbfoundname) == 1):
                                    #print('Glb found - ',glbfoundname)     
                                    #print('Glb found, looking for instances of ',i)
                                    instances = [x for x in t if x['NodeIndex'] == i]
                                    for inst in instances:
                                        #print('Inst - ',i, ' - ',meshname)
                                        
                                        if withMaterials:
                                            try:
                                                bpy.ops.io_scene_gltf.cp77(filepath=glbfoundname[0])                                        
                                            except:
                                                bpy.ops.import_scene.gltf(filepath=glbfoundname[0])
                                        else:
                                            bpy.ops.import_scene.gltf(filepath=glbfoundname[0])
                                        
                                        objects = bpy.context.selected_objects
                                        #obj = bpy.context.object
                                        #print(data.keys())
                                        for obj in objects:                            
                                            nn= str(data['debugName']).replace('{','').replace('}','')
                                            nn = [nn[1:],nn][nn[0].isalnum()]
                                            #print(nn)                            
                                            obj.name = nn
                                            #print(inst['Position'].keys())
                                            if 'Properties' in inst['Position'].keys():
                                                obj.location.x = inst['Position']['Properties']['X'] /100
                                                obj.location.y = inst['Position']['Properties']['Y'] /100
                                                obj.location.z = inst['Position']['Properties']['Z'] /100          
                                            else:
                                                obj.location.x = inst['Position']['X'] /100
                                                obj.location.y = inst['Position']['Y'] /100
                                                obj.location.z = inst['Position']['Z'] /100
                                            if obj.location.x == 0:
                                                print('Mesh - ',meshname, ' - ',i,'HandleId - ', e['HandleId'])      
                                            
                                           #print(i,obj.name,' x= ',obj.location.x, ' y= ', obj.location.y, ' z= ',obj.location.z)
                                            if 'Properties' in inst['Orientation'].keys():
                                                obj.rotation_quaternion.x = inst['Orientation']['Properties']['i']
                                                obj.rotation_quaternion.y = inst['Orientation']['Properties']['j']
                                                obj.rotation_quaternion.z = inst['Orientation']['Properties']['k']
                                                obj.rotation_quaternion.w = inst['Orientation']['Properties']['r']
                                            else:                                    
                                                obj.rotation_quaternion.x = inst['Orientation']['i']
                                                obj.rotation_quaternion.y = inst['Orientation']['j']
                                                obj.rotation_quaternion.z = inst['Orientation']['k']
                                                obj.rotation_quaternion.w = inst['Orientation']['r']
                                            if 'Properties' in inst['Scale'].keys():                       
                                                obj.scale.x = inst['Scale']['Properties']['X'] /100
                                                obj.scale.y = inst['Scale']['Properties']['Y'] /100
                                                obj.scale.z = inst['Scale']['Properties']['Z'] /100
                                            else:
                                                obj.scale.x = inst['Scale']['X'] /100
                                                obj.scale.y = inst['Scale']['Y'] /100
                                                obj.scale.z = inst['Scale']['Z'] /100
                                else:
                                    print('Mesh not found - ',meshname, ' - ',i, e['HandleId'])
                                            
            case _:
                print('None of the above',i)
                
                pass
                   
    print("Done with ",filepath)   
print('Finished')

```

Once you run it it will pull all the models in and position them, their liable to be tiny and off in one corner, if its worked you'll have loads of collections in the model tree, just select all with A and hit the numpad . to frame selection.



#### Things Still to do:

* implement the other node types (how the heck do decals work?)
* ~~Work out why some things are missing (should be more girders above the bar for instance)~~
* ~~have an option to do just meshes or withMaterials~~
* ~~Optimise the code, I know its doing some bits for every instance that could probably be done once per mesh and saved if I rearrange a bit.~~
* ~~use duplicates rather than importing every instance (its horrifically inefficient) - not sure if this would break the possibility of going back into CP though~~.
* Import only the materials for the appearance called up in the sector file?
* See if I can work out where lights are defined, lighting would be nice.
* ~~Test it on somewhere other than just the El Coyote Cojo~~
* ~~make a list of interesting sectors so you don't have to hunt~~

I don't really have a clue where to start on the getting changes back in side of things, so if someone wants to dig into that feel free. I know dragonzkiller was working on both the in/out bits of the process, sods law says doing this will mean he publishes something tomorrow.
