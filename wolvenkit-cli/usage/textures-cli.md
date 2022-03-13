---
description: How to unbundle, uncook, rebuild and pack texture files
---

# Textures (CLI)

## Exporting

1.  **Extract** the textures with `uncook -p` into a folder of your choice. TGA is recommended for CLI version 1.5.1 (latest).


2.  **Edit** the TGA file with software such as Photoshop or Krita.


3. Choose the textures you wish to repack and **copy** them to another folder (e.g. `MODDED`), keeping the subfolder structure (the \base folder needs to be the first folder inside the MODDED folder)

{% hint style="info" %}
**Both** .tga and .xbm files are required in the MODDED folder

e.g. `judy_body_wet.xbm` AND `judy_body_wet.tga`
{% endhint %}

## Importing

{% hint style="danger" %}
Do **not** replace existing vanilla archives
{% endhint %}

1.  **Import**

    Run `import -p "MODDED FOLDER PATH" -k` this will apply the new TGA texture to the XBM.


2.  **Pack**

    Run `pack -p "MODDED FOLDER PATH"`, this will create a new .archive file.


3.  **Install**

    **Copy the packed .archive file int**o the **mod folder** of your game: `Cyberpunk 2077\archive\pc\mod` (create this folder if necessary)
