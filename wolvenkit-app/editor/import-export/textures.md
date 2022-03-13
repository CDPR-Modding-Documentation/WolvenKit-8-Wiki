# Textures

## XBM

## Exporting textures

WolvenKit is capable of exporting Cyberpunk XBM files to DDS format natively. Additional formats such as TGA are supported seamlessly by automatic conversion.

![Advanced texture export options](../../../.gitbook/assets/ImportExportTool\_textures\_advanced.png)

{% hint style="warning" %}
Textures exported with WolvenKit will appear upside-down. **This is not a bug!**\
Textures in Cyberpunk 2077 are upside-down. 🙃
{% endhint %}

### Export Options

#### XBM Export Type

Choose a common image format for exported textures. DDS or TGA is recommended because these formats can be Imported directly with WolvenKit.

#### Flip Image

Vertically invert textures for convenience

## Importing textures

WolvenKit is capable of importing custom images as Cyberpunk XBM files. The Import/Export Tool can replace an existing XBM or generate new standalone XBM.&#x20;

### Import Options

#### Texture Group

(Read Only) Compression method for XBM

#### Use existing file

* When checked WolvenKit requires an existing "source" file. Typically the source file is the original XBM used to export the selected texture. The "rebuilt" texture will retain the original compression method the texture size must remain the same.
* When unchecked WolvenKit creates a new standalone texture, or completely overwrites the source XBM. The XBM compression method will be defaulted (not extensively tested), and the texture size is set dynamically to match the imported texture resolution.

### Supported texture import formats

#### DDS

While DDS is the most tried-and-true format, there are a few drawbacks. When exporting DDS textures from Image Editing Software, the compression method _must match_ the original DDS/XBM or the texture will be corrupted. To verify the compression method, the DDS metadata must be analyzed with a tool such as Visual Studio. Alternatively when the **Use existing file** advanced import option is _disabled_, a new standalone texture with "default" compression is created. This method is currently experimental. The DDS format is also [lossy](https://en.wikipedia.org/wiki/Lossy\_compression), and generally cumbersome to work with in most art applications.

#### TGA

TGA is highly recommended for modding applications due to its lossless nature and support within art pipelines. When importing a TGA image, the correct compression method is _always automatically determined_ by the source XBM. This can make TGA imports much more hassle-free when compared to DDS. Initial support for TGA with WolvenKit 8.4 has a few quirks:

* Most texture formats (such as character diffuse) will freeze WolvenKit during the import operation. To circumvent this issue, deselect the **Use existing file** advanced import option.
* **Color textures** imported without using files must be edited after import. Within the XBM, the **isGamma** boolean must be set to true to display color textures as sRGB. Without **isGamma** checked color textures will appear bright and washed out.

## MLMASK

Creating or modifying multilayer mask files is possible with WolvenKit starting with version 8.3.

{% hint style="info" %}
[Learn more about the functionality of mlmask files on the REDengine 4 Wiki](https://wiki.redmodding.org/redengine4-research/assets/shaders/multilayer.mt/mlmask)
{% endhint %}

### Exporting MLMASK files

Mask files can be exported with the Import/Export tool in a similar fashion to texture files. [**Read about exporting textures above**](textures.md#exporting-textures).

### Importing MLMASK files

Mask files can be created by using a custom helper file in addition to an array of textures. The helper file is essentially a text document with the unique **masklist** extension to be recognized by the Import/Export tool. Use the **import** view of the Import/Export tool to select any masklist file within the **Raw** directory of the Project Explorer. It's important to consider the name and location of the masklist file. The newly created mlmask file will inherit the name and path of the masklist.

### Creating MLMASK files

To create a new masklist, create a new text document (txt) and rename the extension to **masklist**. Paths are absolute meaning you can link textures stored inside your project, or anywhere else on your desktop. Up to 19 mask layers can be utilized.

{% hint style="danger" %}
While using WovenKit 8.3 **DO NOT** link layer 0 (zero)! Layer 0 is created automatically by the import process because l**ayer 0 is always an empty white texture**.
{% endhint %}

```
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_1.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_2.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_3.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_4.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_5.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_6.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_7.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_8.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_9.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_10.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_11.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_12.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_13.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_14.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_15.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_16.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_17.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_18.dds
Q:\...\Raw\base\characters\main_npc\judy\textures\ml_t1_001_wa_tank__judy_masksset_19.dds
```

{% hint style="warning" %}
You must edit this template for use with your local files! Be sure to choose the correct drive letter for your project in addition to replacing `...` with the path to your WolvenKit project!
{% endhint %}
