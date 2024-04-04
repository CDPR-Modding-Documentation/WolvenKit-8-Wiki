---
description: Wolvenkit showed me a popup, how do I fix this?
---

# Long file path support

## Why is this a problem?

If your file paths are longer than 256 characters and your operating system does not support long paths, Wolvenkit will run into errors when importing/exporting files.&#x20;

## How to enable long filepath support?

### Windows

Find the full guide at [microsoft.com](https://learn.microsoft.com/en-us/windows/win32/fileio/maximum-file-path-limitation?tabs=registry#enable-long-paths-in-windows-10-version-1607-and-later)

#### TL;DR

1. Open a Powershell window as administrator \
   _(Keyboard shortcuts: `Windows+R`, type `powershell`, press`Ctrl+Shift+Enter)`_
2. Paste the following command:

```powershell
New-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem" `
-Name "LongPathsEnabled" -Value 1 -PropertyType DWORD -Force
```

3. Press `Enter`

### Linux

This feature is supported out-of-the-box. Just try to stay under 4000 characters.
