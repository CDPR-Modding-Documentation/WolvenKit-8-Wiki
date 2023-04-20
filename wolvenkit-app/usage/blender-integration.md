# Blender Integration

{% embed url="https://user-images.githubusercontent.com/65016231/130711162-301926fa-c7a0-4e08-b7c7-414bfa558205.png" %}

## How does it work?

WolvenKit is able to generate a bespoke **material json** file when exporting mesh files using the **WithMaterials** argument. The material json file writes the REDengine shader values and paths to a plaintext json file which can be used in conjunction with the Cyberpunk Blender add-on.

_For the latest info about the Cyberpunk Blender add-on please visit the GitHub page directly._

{% embed url="https://github.com/WolvenKit/Cyberpunk-Blender-add-on" %}

### How do I use the Blender integration features?

Preparing a material json with WolvenKit is simple, when exporting a mesh just check the Export Materials checkbox:

<figure><img src="../../.gitbook/assets/meshexportoptions.png" alt=""><figcaption></figcaption></figure>

Material export now works will all export modes. You will see a material json file created within the Raw directory with the exported glb mesh file.

### Importing Cyberpunk meshes with Blender

After installing and enabling the Cyberpunk Blender add-on, simply navigate to **File** tab, navigate to **Import** then select **Cyberpunk GLTF**. Entity and Streaming sector import are also available in the latest plugin, see the plugin page for details.

{% hint style="warning" %}
Not all Cyberpunk shaders are supported! Programming shaders can be very tedious. If you're interested in contributing a new shader please consider reaching out on Discord!
{% endhint %}

<figure><img src="../../.gitbook/assets/SSector_Import_1.png" alt=""><figcaption></figcaption></figure>

![](../../.gitbook/assets/BlenderHitmanAddonImageType.png)

{% hint style="warning" %}
Be sure to select the same Image Extension used during the WithMaterials export! The default extension is PNG.
{% endhint %}

### Viewing material meshes with Blender

We recommend using Blender Cycles to view meshes with Cyberpunk materials. While some materials can be previewed with Eevee, the multilayered supershader often exceeds the hard-coded limit of 24 image resources.

{% hint style="info" %}
Cycles viewport performance can be dramatically improved by upgrading to Blender 3.0, using Optix rendering with RTX, and using the Optix viewport denoiser.
{% endhint %}
