---
description: 'Display help for a specific command: e.g. unbundle -h'
---

# Wolvenkit.CLI: Command List

{% hint style="info" %}
For a way to configure Wolvenkit CLI, see  the [settings.md](settings.md "mention") page.
{% endhint %}

## Unbundle

#### Separating archives into distinct compressed REDengine files

`unbundle -p "PATH TO ARCHIVE" -o "OUTPUT PATH" -w *.mesh`

* Extracts all files from archive
* `-w` Use optional search pattern (e.g. \*.ink), if both regex and pattern is defined, pattern will be prioritized.
* `-r` Use optional regex pattern
* -`-hash`: Extract single file with a given hash. If a path is supplied, all hashes will be extracted

The `unbundle` command also takes folder paths as input (will recursively extract all .archives in a folder), or a list of paths (e.g. `unbundle -p "C:\MODDING\archives\basegame_4_gamedata.archive" "C:\MODDING\archives\basegame_1_engine.archive"`

You can filter the files to extract from an archive with the `-w` (Wildcard) or the `-r` (Regex) filters: `unbundle -p "PATH TO ARCHIVE" -w *.mesh` e.g. will **only** extract files with the extension .mesh.

## Uncook

#### Separating archives into distinct _uncompressed_ REDengine files with external buffers

`uncook --uext png -p "PATH TO ARCHIVE" -o "OUTPUT PATH" -or "RAW FOLDER OUTPUT PATH"`

* Extract all textures from archive, common formats (tga, bmp, jpg, png, dds) supported
* `-w` Use optional search pattern (e.g. \*.ink), if both regex and pattern is defined, pattern will be prioritized.
* `-r` Use optional regex pattern
* `-hash`: Extract single file with a given hash. If a path is supplied, all hashes will be extracted
* `--flip`Use boolean option (e.g. 'true' or 'false') : Flip textures vertically (can help with legibility if there's text)
* `--forcebuffers`: Force uncooking to buffers for given extension. e.g. mesh

{% hint style="info" %}
The REDengine extension for textures is **XBM**
{% endhint %}

There are a number of files that support Uncook, including mesh, csv, xbm, and mlmask.

Cyberpunk textures use DDS format, but WolvenKit Console supports conversions to the most common image formats such as TGA, PNG, etc.

For example, textures can be converted to PNG using:&#x20;

`uncook -p "PATH TO ARCHIVE" --uext png`

The same options apply here as well: When using

`uncook -p "PATH TO ARCHIVE" -w *.xbm`&#x20;

Only files with the XBM extension will be uncooked.

## Import

#### Converting raw files to REDengine files

`import -p "INPUT PATH" -o "OUTPUT PATH" --keep`

* Convert raw files to REDengine files
* -p can be a folder or file
* -o (optional) is the output path where the REDengine files are created
* -k (optional) use this parameter if you have already existing REDengine files in your output folder

{% hint style="info" %}
When using -k you need both .dds/.buffer and .xbm/.mesh files

e.g. judy\_body\_wet.xbm AND judy\_body\_wet.dds

When using -o, then the REDengine files need to be located in that folder, while the raw files have to be in the folder specified with -p.
{% endhint %}

## Export

#### Converting REDengine files to raw files

`export --uext png -p "PATH TO FILE"`

* Convert REDengine file (mesh, xbm) to the corresponding raw files (gltf/glb, dds)&#x20;

You can specify a folder to export, or multiple files `pack -p "FILE 1" "FILE 2"`

There are a number of files that support exporting: .mesh, .csv, .xbm, .mlmask and many more.

The in-game textures have .dds fileformat, but WolvenKit Console supports conversions to the most common image formats (png, jpg, tga). E.g. to convert the game textures to png use: `export -p "PATH TO FILE" --uext png`

## Pack

#### Usage

`pack -p <path> [-o output]` (backward compatibility)

`pack [-o output] <path1> <pathN>`



* `-p` is an alias for `--path`
* `-o` is an alias for `--outpath`

#### Description

This command **pack** a folder of REDengine files. It will create a new **.archive** file. You can provide multiple paths to create multiple archives at once.

It will output archive(s) in the current working directory by default. Use the option `-o output` to change the directory path where to output archive(s).

{% hint style="info" %}
This command is not behaving exactly like the button `Build Project` of the WolvenKit application. It will only generate **.archive** file(s) and ignore any extra files (such as **.xl**).
{% endhint %}

{% hint style="danger" %}
Do not replace existing vanilla archives
{% endhint %}

#### Example

* you have a WolvenKit project in `C:\Documents\Modding\Cyberpunk2077\Awesome`
* you are currently in `C:\Documents\Modding\Cyberpunk2077\` with your terminal
* run the command `pack -p "Awesome"`
* output of the archive will be  `C:\Documents\Modding\Cyberpunk2077\Awesome.archive`.

{% hint style="warning" %}
You can provide multiple paths (WKit projects), but only one output path. This is a limitation due to the .NET framework.
{% endhint %}

## \~\~CR2W/W2RC\~\~ (Deprecated)

* Convert a REDengine file into human readable form: `cr2w -s "<PATH TO FILE>"`
* Convert a json file into a REDengine file: `cr2w -d "<PATH TO JSON>"`

## Convert

* Convert a REDengine file into human readable form: `convert -s "<PATH TO FILE>"`
* Convert a json file into a REDengine file: `convert -d "<PATH TO JSON>"`

## Tweak

* Convert .tweak files (in YAML format) to a TweakDB .bin file that can be loaded with [TweakDBext](https://github.com/WopsS/TweakDBext/)
* `tweak -p "<input directory>" -o "<output directory>"`
* Defaults to current directory if `-p` or `-o` are not specified.

The .tweak file must be in the following format, with either `flats` or `groups` declared:

```yaml
flats:
  Mycustom.flat:
    type: Float
    value: 1.0
groups:
  MyOtherCustomRecordOrGroup.mine:
    type: Vehicle
    members:
      affiliation:
        type: TweakDBID
        value: Factions.Unaffiliated 
      animals:
        type: array:String
        value:
          - cow
          - pig
          - horse
          - cat
```

### Groups

Flats for the groups (also called records) are automatically created by appending the member's name to the end of the record's name. Using the example above, the following flats would be created:

```
Mycustom.flat
MyOtherCustomRecordOrGroup.mine.affiliation
MyOtherCustomRecordOrGroup.mine.animals
```

A group's `type` (`Vehicle` in the example above) should exist in CP2077 for it to be useful. The compiler will not warn you if the type doesn't exist, but TweakDBext will let you know upon loading it (watch for messages in `red4ext\logs\tweakdb.log`). Generally a TweakDB type is the RTTI type without `gamedata` or `_Record` ([a full list can be see here](https://github.com/WopsS/RED4ext.SDK/tree/a2c1adcaad3eb2eff28953499ff24e0ff2deb137/include/RED4ext/Scripting/Natives/Generated/game/data), where the `gamedata` is already omitted from the filenames) - as an example, the a `Vehicle`'s RTTI type is `gamedataVehicle_Record`.

### Types

Flats and group members must have one of the following as a base `type` :

```
CName
String
TweakDBID
raRef:CResource
Float
Bool
Uint8
Uint16
Uint32
Uint64
Int8
Int16
Int32
Int64
Color
EulerAngles
Quaternion
Vector2
Vector3
LocKey
```

Types can be prepended with `array:` to create an array, like `array:String` in the example. Arrays can be formatted with hyphens & newlines as in the example, or specified with square brackets and commas. The same array could look like this:

```yaml
      animals:
        type: array:String
        value: [ cow, pig, horse, cat ]
```

Strings can left unenclosed, and optionally enclosed in double quotes, but if you're using paths with `raRef:CResource`, you'll need to double-up the `\`, like this:

```yaml
      curvesPath:
          type: raRef:CResource
          value: "base\\gameplay\\vehicles\\curves\\muscle_car.vehcurveset"
```

`raRef:CResource` also accepts integers (ones that you might pull from a tweakdb output) in place of the path, like this:

```yaml
      curvesPath:
          type: raRef:CResource
          value: 5774411407796421038
```

TweakDBID types can be the full path of the flat/group:

```yaml
flats:
  myFlat.reference:
    type: TweakDBID
    value: myOtherFlat.cow
```

Or the shorthand that uses the hash & length, both in hexadecimal:

```yaml
flats:
  myFlat.reference:
    type: TweakDBID
    value: TDBID:12345678:12
```

`Vector3` are declared like this, using a capital `XYZ`:

```yaml
flats:
  whereIam.position:
    type: Vector3
    value: 
      X: 0
      Y: 0
      Z: 0 
```
