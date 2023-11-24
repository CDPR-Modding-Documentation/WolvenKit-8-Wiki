# Wolvenkit.CLI: Usage

## Summary

This page contains information on the general use of Wolvenkit's command line interface. For more specific information, please see the corresponding sub-pages:

* &#x20;[settings.md](settings.md "mention")&#x20;
* [command-list.md](command-list.md "mention")
* &#x20;[textures-cli.md](textures-cli.md "mention")
* [video-and-audio-files-cli.md](video-and-audio-files-cli.md "mention")

## Help

* Display general help/list all commands: `--help`
* Display help for a specific command: `archive -h`

## Using WolvenKit Console globally

&#x20;You can now install and update the Wolvenkit Command Line Tools (wolvenkit.cli) as a _dotnet global tool_. The console can be used anywhere directly from the command line, with no custom installation, and easy update.

&#x20;Open command prompt/powershell and type in:

`dotnet tool install -g wolvenkit.cli`&#x20;

WolvenKit Console can now be run from anywhere using CMD/Powershell:

`wolvenkit.cli uncook -p "D:\SteamLibrary\steamapps\common\Cyberpunk 2077\archive\pc\content\basegame_1_engine.archive"`

For updates to WolvenKit console, open CMD/Powershell and type:&#x20;

`dotnet tool update --global wolvenkit.cli`

## Video Guide for launching CLI

{% embed url="https://www.youtube.com/watch?v=cwjO_z8pr6A" %}
