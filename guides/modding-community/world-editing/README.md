---
description: >-
  Step by step guide on how to move or delete a object from the world of
  cyberpunk 2077.
---

# World Editing

## Summary

**Created by @Krat0es**\
**Published October 10 2022**

This guide aims to teach you moving and deleting objects from the world.

### Requirements

* [**WolvenKit 8.7**](https://github.com/WolvenKit/WolvenKit)

{% hint style="info" %}
This guide assumes that you already know which sector file to edit. If you need to find it first, check [here](../../../modding-community/world-editing/interesting-sectors.md#finding-a-specific-sector).&#x20;
{% endhint %}

1. Add your sector file to the Wolvenkit project
2. Open it
3. Click on `Sector Preview` again
4. Click into the preview to highlight an object. \
   _This will print the object's node name and -index to the log._
5. In the list on the right, find the object that you want to delete.\
   _You can toggle the red checkmark(s) to show/hide objects in the preview_

<figure><img src="../../../.gitbook/assets/‏‏لقطة الشاشة (1974) (1).png" alt=""><figcaption><p>amazing</p></figcaption></figure>

5. Go back to the **WorldStreamingSector** tab&#x20;
6. Click on expand nodeData to find the object in the list. It is easiest to go by index, which should have been printed to the log when you selected the object in step 4.
7. Expand the node and find `Position`, `Orientation` and `Scale`:

<figure><img src="../../../.gitbook/assets/‏‏لقطة الشاشة (1972) (1).png" alt=""><figcaption><p>nise</p></figcaption></figure>

You can now

* change the object's coordinates or scale
* delete the object from the world by right-clicking the node and deleting it (see screenshot `deletus`)

{% hint style="info" %}
Remember to save the file after making changes!
{% endhint %}

<figure><img src="../../../.gitbook/assets/‏‏لقطة الشاشة (1973).png" alt=""><figcaption><p><code>deletus</code></p></figcaption></figure>

## Troubleshooting

### My deleted object is low-resolution now!

That means that it has a proxy mesh, which you **also** need to delete.&#x20;

1. Search the game for your sector file's name without the last digit\
   Example: \
   You're editing `interior_-23_15_0_1`\
   You're searching `interior_-23_15_0_`

**`Note:`** when you delete a object and you see a low res mesh in its place in the game that means the object has a proxy assigned you will have to find the sector the proxy is in and delete the proxy mesh. `(you may do that following the same steps)`

\




