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

* [**WolvenKit 8.7**](https://github.com/WolvenKit/WolvenKit)****

## Finding the required sector

* first of all you will need your in-game player coordinates you can use `print(GetPlayer():GetWorldPosition())` in the CET console to get them.
* after that search for `streaming block` in the asset browser and open the block then click on `sector preview`
* use the player cords to find the area you are looking for

<figure><img src="../../.gitbook/assets/‏‏لقطة الشاشة (1970).png" alt=""><figcaption><p>veri nise</p></figcaption></figure>

*   After finding the sector you need add it to your project then open it then click on `sector preview` again, from the menu on the right find the object you want to move or delete, click on the small red box to confirm if its the right object or not **(you will see it disappear when you do that)**&#x20;

    <figure><img src="../../.gitbook/assets/‏‏لقطة الشاشة (1974) (1).png" alt=""><figcaption><p>amazing</p></figcaption></figure>
* After finding the object you want to move or delete go back to the **WorldStreamingSector** tab then click on **nodeData** then find the object in the list `(You can memorize where the node is from the sector preview menu)` (edited)
*   after finding the object node in the list click on it to expand the node there you will find **Postion, Orientation and scale**

    <figure><img src="../../.gitbook/assets/‏‏لقطة الشاشة (1972) (1).png" alt=""><figcaption><p>nise</p></figcaption></figure>
* from there you may change the object coordinates `(remember to save after making any changes)`
*   you may right click the node then delete it like you see in this image `(this will delete the object from the world)`\


    <figure><img src="../../.gitbook/assets/‏‏لقطة الشاشة (1973).png" alt=""><figcaption><p><code>deletus</code></p></figcaption></figure>

**`Note:`** when you delete a object and you see a low res mesh in its place in the game that means the object has a proxy assigned you will have to find the sector the proxy is in and delete the proxy mesh. `(you may do that following the same steps)`

\




