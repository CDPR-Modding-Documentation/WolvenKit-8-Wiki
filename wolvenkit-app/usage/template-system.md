---
description: Overview of WolvenKits Template System
---

# Template System

{% hint style="info" %}
If you are looking for documentation regarding the usage of the template system from a nuget package see [Dev Wiki: Red Type Template Service](https://wolvenkit.github.io/WolvenKit/code-documentation/Subprojects/WolvenKit.Common/RedTypeTemplateService.html).
{% endhint %}

### Templates as Reusable Components

Templates are designed to make reusing game structures possible in a streamlined and portable manner.&#x20;

This allows you to create for example templates for entity components or materials that you use frequently so you do not have to manually copy paste them from other files.&#x20;

\
Core to the system is the RedTypeTemplate (or simply "Template") which contains the json serialized data and metadata including author, description and version. \
Almost anything in the game files can be templated except for primitives (elementary types like strings, numbers, etc.)

### Applying a Template

Whenever you are creating a new instance of something like in the "New File" dialog or the yellow "+" button in the tree view you will have an option to select a template if any are available.

{% hint style="info" %}
Templates named "default" will be preselected and can be auto applied in certain cases if it is the only template available without confirmation.&#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### Managing and Editing Templates

Just like wscripts, templates have a template manager that is for the most part analogous to the script manager. \
Here you can create a new template, delete or edit existing ones.&#x20;

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

### Creating new Templates

New templates can either be created using the template manager or via right click > create template in the tree view.

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

### Sharing Templates&#x20;

User templates are stored in `%appdata%\REDModding\WolvenKit\Templates` and can easily be copy pasted between devices.&#x20;

If you have a template that you want to share to be part of the system templates set distributed to every WolvenKit user feel free to open a pull request on [WolvenKit/WolvenKit-Resources](https://github.com/WolvenKit/Wolvenkit-Resources).

{% hint style="warning" %}
Only the root "Templates" folder is scanned, sub folders are deliberately not considered.&#x20;
{% endhint %}

