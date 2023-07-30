---
description: >-
  To make sure the modding tools were setup correctly, you will use the below
  steps to create a very basic color swap mod.
---

# Validate Functionality

## Section Brief

This section is about validating the modding tools and potentially building your first mod.

Learning objectives:

* Understand how file types relate to each other,
* Identify assets with clothes in the game,
* Create and add assets to projects,
* Searching the Asset Browser,
* Understand the Project Explorer,&#x20;
* Review log for activity,&#x20;
* Understand the purpose of the Archive folders versus Raw folders,&#x20;
* Look at assets in File Editor,&#x20;
* Convert to-and-from JSON files,&#x20;
* Opening files from the Asset Browser to plugins,&#x20;
* Use the Import/Export tool,&#x20;
* Install a REDmod type of mod,&#x20;
* Look at installed mods in WolvenKit Mod Manager.

### Overview steps

1. Use the name of the game item to find the asset files in WolvenKit,
2. Find all the asset files for the item,,
3. Create the GLB and DDS file for MlSetupBuilder models,
4. Open an asset in MlSetupBuilder and change its color from green to orange,
5. Import the edited asset back into your project,
6. Install the mod,
7. Party like it’s 2077 in your new orange tank.

{% hint style="info" %}
Some of the steps below are unnecessary, but it's important to see how:

* An in-game item is used to find the ENT file,
* The ENT file is used to find the APP file,
* The APP file is used to find the MESH file,&#x20;
* The MESH file is used to find the MLMASK and MLSETUP files,
* The MLSETUP file is used to find the MLTEMPLATE file,
* MLMASK file is used to find the DDS files,
* DDS file is used to find the XBM file.

Understanding this topology will help with your future mod development.
{% endhint %}

{% hint style="danger" %}
These steps get confusing. Just remember that we’re using the entity file **tshirt\_08\_old\_02\_w.ent** to find the material layer file **t1\_080\_\_leather\_croc.mlsetup**
{% endhint %}

## Steps

1.  To make sure you do not have any mod conflicts, please uninstall all Cyberpunk mods except for Material and Texture Override. This can normally be done by disabling the mods in Vortex or whatever mod managing application you use for your normal gameplay.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S01.png" alt=""><figcaption></figcaption></figure>
2. Launch Cyberpunk 2077 and either load an existing woman character, or start a new one if you have to. If you start a new game, then you'll have to play up to the scav hunt with Jackie before you can swap your clothes.
3. Once you reach a point in the game when you can change your clothes, run the Cyber Engine Tweaks (CET) command “Game.AddToInventory("Items.TShirt\_08\_old\_02",1)”. This will load Judy’s Tank in your torso inventory.
4.  Wear the shirt, take a screenshot, save the game, and then exit the game. This screenshot will be your reference to compare against when you have made the edit.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S04.png" alt=""><figcaption></figcaption></figure>
5. The name of the shirt is **Secondhand Knotted Tank** and it’s an **Inner Torso** item
6.  Navigate to Fandom’s Cyberpunk clothing page and find the asset name for Judy’s tank. Since we know the item is an inner torso shirt, please add #Inner\_Torso to the end of the URL. This convention works for all other items as well. If we want to find V’s Pants then you would add #Legs to the end of the URL. If you’re looking for blades, use Fandom’s menu to navigate to the weapons section Gameplay > Items > [Weapons and then add #Blade](https://cyberpunk.fandom.com/wiki/Cyberpunk\_2077\_Weapons#Blade) to the end of the URL. But in this case, we’re looking for Judy’s shirt.

    [https://cyberpunk.fandom.com/wiki/Cyberpunk\_2077\_Clothing#Inner\_Torso](https://cyberpunk.fandom.com/wiki/Cyberpunk\_2077\_Clothing#Inner\_Torso)

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S06-01.png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S06-02.png" alt=""><figcaption></figcaption></figure>
7.  Launch WolvenKit and create a new project called Judy’s Orange Tank with the Creation Location as C:\Cyberpunk2077Mod\Projects

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S07.png" alt=""><figcaption></figcaption></figure>
8.  In the menu bar click on View and click on Reset Layout to make sure your screen matches the screenshots in this guide.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S08.png" alt=""><figcaption></figcaption></figure>
9.  Click on the Asset Browser and search for the asset name we found on Fandom. Start by searching for the entire name “tshirt\_08\_old\_02” and then slowly start deleting characters from the right side until the entity (ENT) file shows up.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S09.png" alt=""><figcaption></figcaption></figure>
10. Right click the t1\_tshirt\_08.ent file and open the file without adding it to your project. Notice that the file opens in the File Editor and is not listed in the Project Explorer.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S10.png" alt=""><figcaption></figcaption></figure>
11. In the File Editor, expand appearance and locate the full asset name we found on the Fandom website. Notice that in the appearances array, the name ends in “w” which stands for woman (aka “wa” which stands for woman average). Cyberpunk uses postfixes m, ma, mb, mf, w, wa, wb, and wf to describe the gender of the asset and the body type it goes to. A is average, and b and f are synonymous for big/fat. There are other postfixes, but that’s the general concept.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S11.png" alt=""><figcaption></figcaption></figure>
12. In the File Editor, expand appearance 7 for “tshirt\_08\_old\_02\_w”. Click on the blue button for apperanceResource to open the APP file without adding it to the project.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S12.png" alt=""><figcaption></figcaption></figure>
13. In the File Editor, select the APP file, and expand the appearances array. The asset name we got from the Fandom website is <mark style="color:yellow;">**tshirt\_08**</mark>**\_**<mark style="color:green;">**old\_02**</mark>, which is a mashup of its entity name <mark style="color:yellow;">**tshirt\_08**</mark> and one of its appearance names <mark style="color:green;">**old\_02**</mark>. We want the woman version of that appearance, so we're looking for <mark style="color:green;">**old\_02\_w**</mark>. Expand the old\_02\_w **appearance** and expand its **components**. This is where you will start seeing the pseudo name of the asset which is Judy’s Tank. The **meshAppearance** has a value of **leather\_croc**, and the mesh file is listed right next to it. That mesh file is used to create the GLB file that MlSetupBuilder uses to generate the tank's 3D model. Click on the **yellow button** for the mesh file to add it to your project, only files added to your project will show up in the Import/Export Tool.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S13 (1).png" alt=""><figcaption></figcaption></figure>
14. In **Project Explorer**, hover your mouse cursor over the mesh file and click on the blue button to open the file in **File Editor**. Expand the arrays **localMaterialBuffer** > **Materials** > **leather\_croc CMaterialInstance** > **values** > **0** and **1**. \[**0**] contains the **MLSETUP** file which you'll import into MlSetupBuilder to change Judy's Tank from green to orange. \[**1**] contains the **MLMASK** file which you'll use with **Export/Import Tool** to generate the **DDS** files that you'll need to view the 3D model in MlSetupBuilder. Click on the yellow buttons for the **MLSETUP** file and the **MLMASK** file to add them to your project.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S14.png" alt=""><figcaption></figcaption></figure>
15. Right click the **mlsetup** file and convert it to JSON

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S15.png" alt=""><figcaption></figcaption></figure>
16. Right click the JSON file and open it in MlSetupBuilder (aka mlsb). MLSB should automatically open for you. If it doesn't, then first check the Windows task bar to make sure it's not open but hidden, and then check click on HOME > Plugins to make sure it is installed.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S16.png" alt=""><figcaption></figcaption></figure>
17. Over in MlSetuipBuilder (MLSB), close the developer tool, then savagely and with mercy throw more coffee at Neurolinked#4973 (the author of this guide is not Neurolinked), and then click anywhere off the Welcome popup to get into the building tool.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S17.png" alt=""><figcaption></figcaption></figure>
18. Notice that the material layers loaded but not the model. Click on Library to bring up the frame with the available models.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S18.png" alt=""><figcaption></figcaption></figure>
19. Search for the mesh name from step 13 and then double-click on the model. Depending on how you created your Depot, you may see up to two errors. The errors are saying that the model requires two files, and those files are not in the locations that MLSB expects. One is the GLB 3D binary and the other the DDS flat image.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S19.png" alt=""><figcaption></figcaption></figure>
20. To generate these two files, you will use the WolvenKit Import/Export Tool. First thing is to find out where MLSB is expecting these files. Close the Library by clicking the X icon in the orange bar on the top-right of the library. Then click on the warning icon on the bottom-left to open the error log.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S20.png" alt=""><figcaption></figcaption></figure>
21. The error log says MLSB wants the DDS file in C:\Cyberpunk2077Mod\Depot\base\characters\main\_npc\judy\textures and the GLB file in C:\Cyberpunk2077Mod\Depot\base\characters\garment\player\_equipment\torso. If you decided not to create an Asset Depot then you will need to manually create these folders for the files you are about to create.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S21.png" alt=""><figcaption></figcaption></figure>
22. Back in WolvenKit, on the right-side of the screen, click on the tab Import/Export Tool to expand the tool's window. Notice that the MLMASK file is currently set to export as a PNG, but MlSetupBuilder asked for a DDS file. To change that, right click on the MLMASK file and then click on Show Settings. Click on the export type dropdown and change png to dds, and then click on Confirm.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S22.png" alt=""><figcaption></figcaption></figure>
23. Now that the **mesh** is configured to export as a **GLB** and the **mask** as a **DDS**, you are ready to export. You can either check the boxes next to each file and click on Process Selected, or since you need to export all the files anyway, ignore the checkboxes and click on Process All. Depending on the speed of your computer, the exported files will eventually show up in Project Explorer in the RAW folders. Notice how several DDS files were exported? This is because each DDS file represents an appearance layer on the 3D model. You can figure out which DDS file you need in three different ways:
    * On step 18, the leather\_croc layer is listed as layer 0 which matches to the numbering system of the DDS files: masksset\_0.dds, masksset\_1.dds, masksset\_2.dds, masksset\_3.dds, etc...
    * On Step 21, MlSetupBuilder told you which DDS file it needed ml\_t1\_001\_wa\_tank\_\_judy\_masksset\_0.dds
    *   Back in WolvenKit you can open the MLSETUP file and expand the appearances list to see which layer number is needed. This is the exact same information as the layer information displayed in MlSetupBuilder (MLSB).

        <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S23.png" alt=""><figcaption></figcaption></figure>
24. From the error logs on Step 21, and create the folders:
    * C:\Cyberpunk2077Mod\Depot\base\characters\main\_npc\judy\textures
    * C:\Cyberpunk2077Mod\Depot\base\characters\garment\player\_equipment\torso
25. Back in WolvenKit, hover your mouse over the GLB file and click on the yellow button to open the file's location in File Explorer. Right click the file and copy it, and then paste it in the folder you created back on step 21 (C:\Cyberpunk2077Mod\Depot\base\characters\garment\player\_equipment\torso\\)

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S25.png" alt=""><figcaption></figcaption></figure>
26. Back in WolvenKit, hover your mouse over the MASKSSET\_0.DDS file and click on the yellow button to open the file's location in File Explorer. Right click the file and copy it, and then paste it in the folder you created back on step 21 (C:\Cyberpunk2077Mod\Depot\base\characters\main\_npc\judy\textures\\)

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S26.png" alt=""><figcaption></figcaption></figure>
27. Back in MlSetupBuilder, click the refresh button at the bottom of the screen. The model should load without errors and the multilayers display on the right.

    > <mark style="color:red;">**Attention:**</mark> As of MlSetupBuilder version 1.6.5, the model does not change with the material selections (e.g. color Normals, Metal Outside, etc.). The model only shows the relationship of the layers with each other. You can see this by clicking through the layers, and the colored region on the model is the currently selected layer.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S27.png" alt=""><figcaption></figcaption></figure>
28. You can leave the leather\_croc material and only change the color to orange (in the case of this guide’s example), but I feel that the orange color looks better in spandex. Select the leather\_croc layer and then click the Material dropdown. Type spandex into the search box and select the spandex\_clean\_02\_30 material, and then click the Material dropdown again to close the dropdown.

    > <mark style="color:red;">**Attention:**</mark> Please take a mental note that each layers’ name starts with a number that is in sequence from 0 through however many layers the asset has. The layer we’re editing starts with a 0, which means we’re editing layer 0.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S28.png" alt=""><figcaption></figcaption></figure>
29. These four settings alter how the material is rendered to physically represent how light interacts with its surface. The dropdown values are not color HEX, but instead reference numbers. The important numbers are inside the brackets (#).
    * **Normals**: A texture mapping technique used for faking the lighting of bumps and dents.
    * **Metal Outside**: Defines the outside of the material as diffuse with a white dielectric coating (0.0) or metallic (1.0)
    * **Rough Inside**/**Rough Outside**: Sets the roughness of the surface, where 0.0 is completely smooth, and 1.0 is completely rough (wholly diffuse).
30. Set the Normals to 1.66, Metal and Rough Inside to null, and Rough Outside to 0.3333,0.6666.

    <div align="left">

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S30.png" alt=""><figcaption></figcaption></figure>

    </div>
31. Scroll down the color grid, select orange, and then click the Apply Edits button. Notice that the wording in the layer changes to match your selections.&#x20;

    > <mark style="color:red;">**Attention:**</mark> While you’re here, make sure the Opacity is 1.0 which means this layer is 100% visible.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S31.png" alt=""><figcaption></figcaption></figure>
32. With the layer updated, click on Export and selected the Wkit version that matches what you have installed, and as of 10/20/2022 that is WolvenKit 8.7. The Save Dialog Window should open to your Project folder and have the same name as the JSON you converted in WolvenKit. When you click on Save, also click on Yes to replace the existing file. There is no need to save a copy of the original because you can repeat step 16 to re-create it.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S32.png" alt=""><figcaption></figcaption></figure>
33. Back in WolvenKit, right click on the JSON file and click on Import from JSON. Normally a log would be created to show you the import occurred, but currently that isn’t happening so I cannot show you that. Regardless, if you look at the modified date of the mlsetup file in File Explorer, you will see an updated datetime.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S33.png" alt=""><figcaption></figcaption></figure>
34. Notice the button Pack as REDmod. This button packs your asset files into an archive file, generates the required info.json, puts them into the necessary folder structure to install the mod into your game. This package can be viewed on the PACKED tab. Feel free to click the button Pack as REDmod to see what it does, it will not harm the mod, or else you can skip this step and just look at the screenshot below to see what it does.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S34.png" alt=""><figcaption></figcaption></figure>
35. Click the button **Install as REDmod**. This button will pack your mod just like **Pack as REDmod** did, and then it will also install the mod into your game folder. Let me repeat myself but with different words,
    * Pack as REDmod generates the archive file,
    *   Install as REDmod also generates the archive file and then install it to your gaming folder.

        <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S35.png" alt=""><figcaption></figcaption></figure>
36. Your new mod will be listed in the Cyberpunk 2077 REDmod folder

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S36.png" alt=""><figcaption></figcaption></figure>
37. Launch the Cyberpunk 2077 game and load your saved game from step 4. How you launch the game doesn’t matter because the mod is deployed directly to the game’s install directory. Enter your inventory and you’ll notice that the tank you created in step 3 changed from green leather to orange spandex.

    <figure><img src="../../../.gitbook/assets/ELI5_GetStart_Validate_S37.png" alt=""><figcaption></figcaption></figure>
38. Congratulations! You have now validated that WolvenKit is deployed and setup correctly on your computer. Happy modding!
