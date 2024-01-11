---
description: The command-line modding tool
---

# WolvenKit Console

## What is the WolvenKit Console?

WolvenKit Console is the core "Modkit" that drives the WolvenKit application. The Console supersedes the original CP77 Tools application created by rfuzzo. The same core functionalities of WolvenKit are available from command line for simplicity and extendibility for power users.

* For a documentation of the individual commands, see [command-list.md](usage/command-list.md "mention")
* For further instructions on using it, see [usage](usage/ "mention")

{% hint style="warning" %}
As of January 2024, Wolvenkit.CLI does not work under Linux. You can run it though qemu and virtofs.
{% endhint %}

## Installing Wolvenkit Console

### As a dotnet tool

For a global install, you can install it as a dotnet tool. Open up the windows command line (`Windows+R`, type `cmd`, hit `return`) or Powershell, then enter the following:

```
dotnet tool install -g wolvenkit.cli 
```

Verify if the installation was successful:

```
wolvenkit.cli -help
```

### By downloading it from the repository

You can download Wolvenkit Console from the Releases page on the github repository ([Release](https://github.com/WolvenKit/WolvenKit/releases) | [Nightly](https://github.com/WolvenKit/WolvenKit-nightly-releases/releases)). Select the download starting with `Wolvenkit.Console`.

Extract it to a directory of your choice (for example `C:\Cyberpunk_Modding\Wolvenkit.Console`).&#x20;

You can run Wolvenkit console from that directory, for example:&#x20;

```
C:\Cyberpunk_Modding\Wolvenkit.Console\Wolvenkit.CLI.exe -help
```

To make the command globally available, add the directory to your [Windows Path](https://www.architectryan.com/2018/03/17/add-to-the-path-on-windows-10/).
