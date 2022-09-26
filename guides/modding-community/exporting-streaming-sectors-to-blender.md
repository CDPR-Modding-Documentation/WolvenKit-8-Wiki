---
description: Exporting locations to Blender
---

# Exporting Streaming Sectors to Blender

## Summary

**Created by @Simarilius** \
**Published September 23 2022**

This is very much a work in progress, and only gets Streaming Sectors out and into Blender so far. Based on some posts by @123321 in the Discord _#mapeditor_ channel back in May, so all credit to him for working it out in the first place.

#### This guide uses the following versions:

* Cyberpunk 2077 game version 1.6
* WolvenKit-8.7.0-nightly.2022-09-17
* Blender 3.3 stable
* Cyberpunk add-on for Blender 1.0.8

### Requirements

* [**WolvenKit nightly release version 8.7**](https://github.com/WolvenKit/WolvenKit)****
* [**Blender 3.3**](https://www.blender.org/)****
* [**Cyberpunk add-on for Blender 1.0.8**](https://github.com/dragonzkiller/cp77research)****

## Exporting Streaming Sectors to Blender

The first challenge is finding the sector for the location you want, as they have names that I havent worked out how to interpret yet. The easiest way to locate them I've found so far is if theres anything unique in the location, to find the mesh then use where used to track back to the streaming sector. So for instance to find El Coyote has the sign which is findable with a search for coyote as el\_coyote\_cojo\_bar\_signage\_a.mesh _._ From that you can do used by to find interior\_-20\_-16\_0-1.streamingsector.

You can preview the sector in wolvenkit to confirm its what your after.

Once you've found the location you want to export, add the sector to your project, then right click and export to JSON.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Now right click the sector in the Asset Browswer and do Find Used Files&#x20;

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Filter by kind then select all the mesh files and add to your project.&#x20;

Goto the import/export tool, double click a mesh and switch to withMaterials, and turn LOD off. Then apply to all of this kind, and process all.

the last step for WolvenKit is to open the streamingsector file, go to `nodeData`, then right click on any line and press `Export NodeData to JSON`, save to a file named for example  `worldNodeData.json` and remember the location, as you'll need it in a minute.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Now fire up Blender, I'm using 3.3. Create an empty file, and go to the scripting page. Paste the script below into a new script.

```python
import json
import glob
import os
import bpy
path = 'F:\\CPmod\\coyote\\source\\raw\\base'

C = bpy.context
coll_scene = C.scene.collection
Masters=bpy.data.collections.new("MasterInstances")
coll_scene.children.link(Masters)

# Set target collection to a known collection 
coll_target = coll_scene.children.get("MasterInstances")


meshes =  glob.glob(path+"\**\*.glb", recursive = True)
for mesh in meshes:
    try:
       bpy.ops.io_scene_gltf.cp77(filepath=mesh)
       objs = C.selected_objects
       
       
       move_coll= coll_scene.children.get( objs[0].users_collection[0].name )
       coll_target.children.link(move_coll) 
       coll_scene.children.unlink(move_coll)

    except:
        print("Failed on ",mesh)
```

Set the path variable to the project raw folder, then run it. That will pull all the glbs in your project into the Blender file, including materials. These will be put in a Collection called MasterInstances. This step may take a few minutes as loading the meshes with materials isnt the fastest process. After this add a second script to the file, and paste the script below in it.

```python
import json
import glob
import os
import bpy
C = bpy.context
path = 'F:\\CPmod\\coyote\\source\\raw'
path2 = 'F:\\CPmod\\StreamingSector\\worldNodeData.json'

Masters = bpy.context.scene.collection.children.get("MasterInstances")

jsonpath = glob.glob(path+"\**\*.streamingsector.json", recursive = True)
filepath = jsonpath[0]

with open(filepath,'r') as f: 
      j=json.load(f) 
      
with open(path2,'r') as f: 
      t=json.load(f) 
      
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
       
print('Finished')
```

The path variable needs to point to the raw folder of the project that you extracted your meshes and streamingsector to. The path2 variable points to the worldNodeData.json you created above.

Run the script and it should instance the meshes, and position them all. I'm doing it via instances as if you just pull meshes in for each item the script takes 6+hrs to pull in Coyote Cojo. This may be a problem for modding in terms of getting it back into CP, so I do have a version that can pull meshes in and I've put a switch that lets you turn on or off the material import, as the time difference is huge, just meshes takes 30 secs or so, with materials is at an several hours. Open to discussions on this on the Discord, and happy to provide the other version if people want it.

As you can see in the script there are several node types in the sector file not being processed currently, and these included decals and decoration meshes that add the detail to the scene, but the bones of it are there with the above script. Will try and get these extras added soon. The code is not by any stretch of the imagination optimised, but it mostly works.

It doesn't bring in things that are entities, so the ceiling fans & burrito machines for instance, but the meshes for those aren't linked from the scene itself, so adding that level of understanding may be a push. May look at adding named empties at the locations and doing another script that can pull meshes in later.

Missing a bunch of tables and stools too, not worked out where they are meant to be defined, they are in the preview in wkit but I haven't located them in the nodes yet.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Things to do still on it:

* implement the other node types (how the heck do decals work?)
* Work out why some things are missing (should be more girders above the bar for instance)
* ~~have an option to do just meshes or withMaterials~~
* ~~Optimise the code, I know its doing some bits for every instance that could probably be done once per mesh and saved if I rearrange a bit.~~
* ~~use duplicates rather than importing every instance (its horrifically inefficient) - not sure if this would break the possibility of going back into CP though~~.
* Import only the materials for the appearance called up in the sector file?
* See if I can work out where lights are defined, lighting would be nice.
* Test it on somewhere other than just the El Coyote Cojo
* make a list of interesting sectors so you don't have to hunt

I don't really have a clue where to start on the getting changes back in side of things, so if someone wants to dig into that feel free. I know dragonzkiller was working on both the in/out bits of the process, sods law says doing this will mean he publishes something tomorrow.

The code below does the import without using linked duplicates, no need for the first script, and you can export without materials. The bool property at the start will let you explicitly not import materials. I STRONGLY advise against using this withMaterials, as its orders of magnitude slower to import.

```python
import json
import glob
import os
import bpy
path = 'F:\\CPmod\\coyote\\source\\raw'
path2 = 'F:\\CPmod\\StreamingSector\\worldNodeData.json'

withMaterials=False

#Masters=bpy.data.collections.new("MasterInstances")
#bpy.context.scene.collection.children.link(Masters)

jsonpath = glob.glob(path+"\**\*.streamingsector.json", recursive = True)
filepath = jsonpath[0]

with open(filepath,'r') as f: 
      j=json.load(f) 
      
with open(path2,'r') as f: 
      t=json.load(f) 
      
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
                   
       
print('Finished')
```
