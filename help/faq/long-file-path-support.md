---
description: Wolvenkit showed me a popup, how do I fix this?
---

# Long file path support

## What are long filepaths, and why do I need them?&#x20;

{% hint style="info" %}
This should be a standard setting in every operating system. Unfortunately, Windows doesn't care.
{% endhint %}

In the year of our lord 2025, Windows does not (by default) support file paths longer than 256 characters — and if you're somebody who likes to use subfolders, this **will** break Wolvenkit's mod packing.

We decided to show you a warning at every startup, because

* the fix is super easy
* we can't solve the problem in Wolvenkit
* if you run into this, you'll be unable to create mods

## How to enable long filepath support?

### Windows

{% hint style="success" %}
If you don't trust something you read on a random modding wiki, find the full guide at [microsoft.com](https://learn.microsoft.com/en-us/windows/win32/fileio/maximum-file-path-limitation?tabs=registry#enable-long-paths-in-windows-10-version-1607-and-later).&#x20;
{% endhint %}

1. Open a Powershell window as administrator \
   &#xNAN;_(Keyboard shortcuts: `Windows+R`, type `powershell`, press`Ctrl+Shift+Enter)`_
2. Paste the following command:

```powershell
New-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem" `
-Name "LongPathsEnabled" -Value 1 -PropertyType DWORD -Force
```

3. Press `Enter`

That's it! You now have long path support enabled.

### Linux

This feature is supported out-of-the-box. Just try to stay under 4000 characters.
