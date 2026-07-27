---
description: How to configure Wolvenkit Console
---

# Settings

You edit the settings for Wolvenkit.CLI by editing `appsettings.json` in a text editor.

Runnning `Wolvenkit.CLI settings` will open that for you.

### Property Documentation

As a rule of thumb, the settings correspond to their names in the Wolvenkit UI in CamelCase.&#x20;

{% hint style="danger" %}
TODO: Need _much_ better documentation here.
{% endhint %}

### Example settings file

An example file (as of PL) can look like this:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Warning"
    }
  },
  "XbmExportArgs": {
    "Flip" : false,
    "UncookExtension": "png"
  },
  "MeshExportArgs": {
    "MaterialRepo": "C:\\depot\\goes\\here",
    "UncookExtension": "glb"
  }
}

```

The supported arguments can be found in the Wolvenkit repository for both [Import](https://github.com/WolvenKit/WolvenKit/blob/main/WolvenKit.Common/Model/Arguments/ImportArgs.cs) and [Export](https://github.com/WolvenKit/WolvenKit/blob/main/WolvenKit.Common/Model/Arguments/ExportArgs.cs).
