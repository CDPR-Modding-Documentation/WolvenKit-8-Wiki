---
description: If you want to find a specific .streamingsector, here's how
---

# Finding a specific sector

## Finding a specific sector

### Perquisite: Getting the coordinates

You need to grab the sector's coordinates from the game first. Go there, then open the CET console and type the following command:

```
print(GetPlayer():GetWorldPosition())
```

Copy the result and put it into a txt file somewhere. You're now good to go.

### Method 1: the Wolvenkit preview

1. In Wolvenkit, open the file `base\worlds\03_night_city\_compiled\default\blocks\all.streamingblock`
2. Switch to the second tab "All Sector Preview"
3. In the panel to the right, enter the coordinates that you copied from the game in step 2
4. Click "Search for Coordinate"
5. Optional: Zoom in

{% hint style="info" %}
You can double-click on the red text to load the corresponding streamingsector file into the streamingblock's preview!
{% endhint %}

<figure><img src="../../../.gitbook/assets/streamingsector_finding_sector (1).png" alt=""><figcaption><p>veri nise</p></figcaption></figure>

{% hint style="success" %}
For details on how to find other LOD levels, check [here](https://wiki.redmodding.org/cyberpunk-2077-modding/modding-know-how/files-and-what-they-do/the-whole-world-.streamingsector#calculating-the-files).&#x20;
{% endhint %}

### Method 2: Following the meshes

If you know a mesh that's used inside the location, you can right-click the mesh file inside Wolvenkit's asset browser and use "**Find files using this**".&#x20;

{% hint style="info" %}
You might want to consider using a unique mesh rather than a standard cup or bottle.
{% endhint %}

<figure><img src="../../../.gitbook/assets/streamingsectors_find_files_using_this.png" alt=""><figcaption></figcaption></figure>

### Method 3: Via script

Go [here](https://colab.research.google.com/github/Simarilius-uk/sectorStuff/blob/main/AllBlocks\_colab\_w\_streamingblock.ipynb) and either use the script in your webbrowser (recommended) or download the script locally to run it with Python.&#x20;

#### When running from browser:

Change the x, y and z coordinate to the coordinates that you found [via CET](finding-a-specific-sector.md#perquisite-getting-the-coordinates):

<figure><img src="../../../.gitbook/assets/export_streaming_blender_search_script.png" alt=""><figcaption></figcaption></figure>

#### When running locally:

The script requires you to have a local json export of `all.streamingblock` somewhere.&#x20;

Change line 11 to the absolute path of your json (remember the double slashes):

```
11     filepath = 'C:\\CyberpunkModding\\Files\\all.streamingblock.json'
```

You'll find the coordinates in line 31. Change them to the coordinates that you found [via CET](finding-a-specific-sector.md#perquisite-getting-the-coordinates):

```
31     player_loc={'X':-1604.0522,'Y':353.99716,'Z':49.200005}
```

Now, run the script via Python. It'll give you a list of interior/exterior sector files together with the distance from your coordinates.

The blocks at the bottom can be used to generate a streamingblock json file for just the results, which can be imported to wolvenkit to preview them as per Method 1. if running the script locally you will need to download the sectors.streamingblock file from the github and edit the templatepath variable to point at it.

