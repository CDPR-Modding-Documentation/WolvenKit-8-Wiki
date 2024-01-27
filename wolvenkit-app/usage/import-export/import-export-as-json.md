---
description: How to import or export to/from JSON with Wolvenkit
---

# Import/Export as JSON

{% hint style="info" %}
This is not the only means of export! See [tools-import-export.md](../../tools/tools-import-export.md "mention") for documentation of the other.
{% endhint %}

Converting files **to** JSON will serialize[^1] their content to a .json file in your project's `raw` folder.&#x20;

Importing them back will re-create the corresponding file under `archive`.

This is easiest way to [quickly change paths in projects](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-creators/modding-guides/everything-else/moving-and-renaming-in-existing-projects) and a perquisite for several modding workflows.

### Export as JSON

This option is **in the right-click menu**:

<figure><img src="../../../.gitbook/assets/export_convert_to_json.png" alt=""><figcaption></figcaption></figure>

### Import as JSON

This option is **in the right-click menu**:

{% hint style="info" %}
JSON import will be available for any file in your `raw` folder with the extension `.json`. **However**, if the file hasn't been created via "`Convert to JSON`", the import will fail.&#x20;
{% endhint %}

<figure><img src="../../../.gitbook/assets/import_convert_from_json.png" alt=""><figcaption></figcaption></figure>

[^1]: Netrunner for "create a text file representation with all information needed to re-create the file"  &#x20;
