# WScript API Documentation

All methods listed on this page are accessible via `wkit.functionName()` without any additional imports.

{% hint style="info" %} The following method list is auto-generated from WolvenKit Source. {% endhint %}

<!-- AUTOGEN_MARKER_START -->
> Turn on/off updates to the project tree, useful for when making lots of changes to the project structure.

| Parameter | Description |
|-----------|-------------|
| `suspend` | bool for if updates are suspended |
```csharp
SuspendFileWatcher(suspend: bool) → void
```

---

> Add the specified CR2WFile or IGameFile file to the project.

| Parameter | Description |
|-----------|-------------|
| `path` | The file to write to |
| `file` | CR2WFile or IGameFile to be saved |
```csharp
SaveToProject(path: string, file: object) → void
```

---

> Save the specified text to the specified path in the raw folder.

| Parameter | Description |
|-----------|-------------|
| `path` | The file to write to |
| `content` | The string to write to the file |
```csharp
SaveToRaw(path: string, content: string) → void
```

---

> Save the specified text to the specified path in the resources folder.

| Parameter | Description |
|-----------|-------------|
| `path` | The file to write to |
| `content` | The string to write to the file |
```csharp
SaveToResources(path: string, content: string) → void
```

---

> Loads the content of a text file from resources.

| Parameter | Description |
|-----------|-------------|
| `path` | The relative path of the text file |

**Returns:** The content or null
```csharp
LoadFromResources(path: string) → ? string
```

---

> Loads the specified game file from the project files rather than game archives.

| Parameter | Description |
|-----------|-------------|
| `path` | The file to open for reading |
| `type` | The type of the object which is returned. Can be "cr2w" or "json" |
```csharp
LoadGameFileFromProject(path: string, type: string) → ? object
```

---

> Loads the specified json file from the project raw files rather than game archives.

| Parameter | Description |
|-----------|-------------|
| `path` | The file to open for reading |
| `type` | The type of the object which is returned. Can be "cr2w" or "json" |
```csharp
LoadRawJsonFromProject(path: string, type: string) → ? object
```

---

> Retrieves a list of files from the project.

| Parameter | Description |
|-----------|-------------|
| `folderType` | string parameter folderType = "archive" or "raw" |
```csharp
GetProjectFiles(folderType: string) → List< string >
```

---

> Clears the lookup for exported depot files.
```csharp
ClearExportFileLookup() → void
```

---

> Exports a list of files as you would with the export tool.

| Parameter | Description |
|-----------|-------------|
| `fileList` | — |
| `defaultSettings` | — |
| `blocking` | — |
```csharp
ExportFiles(fileList: IList, defaultSettings: ScriptObject? = null) → void
```

---

> Loads a file from the project using either a file path or hash.

| Parameter | Description |
|-----------|-------------|
| `path` | The path of the file to retrieve |
| `openAs` | The output format (OpenAs.GameFile, OpenAs.CR2W or OpenAs.Json) |
```csharp
GetFileFromProject(path: string, openAs: OpenAs) → ? object
```

---

> Loads a file from the project using either a file path or hash.

| Parameter | Description |
|-----------|-------------|
| `hash` | The hash of the file to retrieve |
| `openAs` | The output format (OpenAs.GameFile, OpenAs.CR2W or OpenAs.Json) |
```csharp
GetFileFromProject(hash: ulong, openAs: OpenAs) → ? object
```

---

> Loads a file from the project or archive (in this order) using either a file path or hash.

| Parameter | Description |
|-----------|-------------|
| `path` | The path of the file to retrieve |
| `openAs` | The output format (OpenAs.GameFile, OpenAs.CR2W or OpenAs.Json) |
```csharp
GetFile(path: string, openAs: OpenAs) → ? object
```

---

> Loads a file from the project or archive (in this order) using either a file path or hash.

| Parameter | Description |
|-----------|-------------|
| `hash` | The hash of the file to retrieve |
| `openAs` | The output format (OpenAs.GameFile, OpenAs.CR2W or OpenAs.Json) |
```csharp
GetFile(hash: ulong, openAs: OpenAs) → ? object
```

---

> Check if file exists in the project.

| Parameter | Description |
|-----------|-------------|
| `path` | file path to check |
```csharp
FileExistsInProject(path: string) → bool
```

---

> Check if file exists in the project.

| Parameter | Description |
|-----------|-------------|
| `hash` | hash value to be checked |
```csharp
FileExistsInProject(hash: ulong) → bool
```

---

> Check if file exists in either the game archives or the project.

| Parameter | Description |
|-----------|-------------|
| `path` | file path to check |
```csharp
FileExists(path: string) → bool
```

---

> Check if file exists in either the game archives or the project.

| Parameter | Description |
|-----------|-------------|
| `hash` | hash value to be checked |
```csharp
FileExists(hash: ulong) → bool
```

---

> Check if file exists in the project Raw folder.

| Parameter | Description |
|-----------|-------------|
| `filepath` | relative filepath to be checked |
```csharp
FileExistsInRaw(filepath: string) → bool
```

---

> Deletes a file from the project, if it exists.

| Parameter | Description |
|-----------|-------------|
| `filepath` | relative filepath to be deleted |
| `folderType` | project subfolder type (archive\|raw\|resources) |

**Returns:** true if the file was deleted
```csharp
DeleteFile(filepath: string, folderType: string) → bool
```

---

> Loads all records as TweakDBID paths.
```csharp
GetRecords() → IEnumerable
```

---

> Loads all flats as TweakDBID paths.
```csharp
GetFlats() → IEnumerable
```

---

> Loads all queries as TweakDBID paths.
```csharp
GetQueries() → IEnumerable
```

---

> Loads all group tags as TweakDBID paths.
```csharp
GetGroupTags() → IEnumerable
```

---

> Loads a record by its TweakDBID path.

| Parameter | Description |
|-----------|-------------|
| `path` | — |

**Returns:** record as a JSON string, null when not found
```csharp
GetRecord(path: string) → ? string
```

---

> Loads a flat by its TweakDBID path.

**Returns:** flat as a JSON string, null when not found
```csharp
GetFlat(path: string) → ? string
```

---

> Loads flats of a query by its TweakDBID path.

**Returns:** a list of flats as TweakDBID paths, empty when not found
```csharp
GetQuery(path: string) → IEnumerable
```

---

> Loads a group tag by its TweakDBID path.

**Returns:** flat as a JSON string, null when not found
```csharp
GetGroupTag(path: string) → ? byte
```

---

> Whether TweakDBID path exists as a flat or a record?

| Parameter | Description |
|-----------|-------------|
| `path` | — |
```csharp
HasTDBID(path: string) → bool
```

---

> Tries to get TweakDBID path from its hash.

| Parameter | Description |
|-----------|-------------|
| `key` | — |

**Returns:** path of the hash, null when undefined
```csharp
GetTDBIDPath(key: ulong) → ? string
```

---

> Displays a message box.

| Parameter | Description |
|-----------|-------------|
| `text` | A string that specifies the text to display. |
| `caption` | A string that specifies the title bar caption to display. |
| `image` | A WMessageBoxImage value that specifies the icon to display. |
| `buttons` | A WMessageBoxButtons value that specifies which buttons to display. |

**Returns:** A WMessageBoxResult value that specifies the result the message box button that was clicked by the user returned.
```csharp
ShowMessageBox(text: string, caption: string, image: WMessageBoxImage, buttons: WMessageBoxButtons) → WMessageBoxResult
```

---

> Extracts a file from the base archive and adds it to the project.

| Parameter | Description |
|-----------|-------------|
| `path` | Path of the game file |
```csharp
Extract(path: string) → void
```

---

> Gets the current active document from the docking manager.
```csharp
GetActiveDocument() → ?  ScriptDocumentWrapper
```

---

> Gets all documents from the docking manager.
```csharp
GetDocuments() → ? IList<  ScriptDocumentWrapper  >
```

---

> Opens a file in  WolvenKit .

| Parameter | Description |
|-----------|-------------|
| `path` | Path to the file |

**Returns:** Returns true if the file was opened, otherwise it returns false
```csharp
OpenDocument(path: string) → bool
```

---

> Opens an archive game file.

| Parameter | Description |
|-----------|-------------|
| `gameFile` | The game file to open |
```csharp
OpenDocument(gameFile: IGameFile) → void
```

---

> Exports an geometry_cache entry.

| Parameter | Description |
|-----------|-------------|
| `sectorHashStr` | Sector hash as string |
| `entryHashStr` | Entry hash as string |
```csharp
ExportGeometryCacheEntry(sectorHashStr: string, entryHashStr: string) → ? string
```

---

> Creates a new instance of the given class, and returns it converted to a JSON string.

| Parameter | Description |
|-----------|-------------|
| `className` | Name of the class |
```csharp
CreateInstanceAsJSON(className: string) → ? object
```

---

> Returns the hashcode for a given string.

| Parameter | Description |
|-----------|-------------|
| `data` | String to be hashed |
| `method` | Hash method to use. Can be "fnv1a64" or "default" (Uses the String objects built in hash function) |
```csharp
HashString(data: string, method: string) → ? ulong
```

---

> Pauses the execution of the script for the specified amount of milliseconds.

| Parameter | Description |
|-----------|-------------|
| `milliseconds` | The number of milliseconds to sleep. |
```csharp
Sleep(milliseconds: int) → void
```

---

> Returns the current wolvenkit version.
```csharp
ProgramVersion() → string
```

---

> Shows the settings dialog for the supplied data.

| Parameter | Description |
|-----------|-------------|
| `data` | A JavaScript object containing data |

**Returns:** Returns true when the user changed the settings, otherwise it returns false
```csharp
ShowSettings(data: ScriptObject) → bool
```

---

```csharp
SaveAs(path: string, action: Action< string >) → void
```

---

```csharp
GetBaseFolder(folderType: string) → string?
```

---

```csharp
ParseExportSettings< T >(scriptSettingsObject: ScriptObject) → T
```

---

```csharp
GetGlobalExportArgs(settings: ScriptObject) → GlobalExportArgs
```

---

```csharp
ConvertTDBToPath(ids: List< TweakDBID >?) → List< string >
```

---

```csharp
ConvertTDBToJson(tdb: object?) → string?
```

---

> Gets the game file.

| Parameter | Description |
|-----------|-------------|
| `type` | The output type of the game file ("cr2w" or "json") |
```csharp
GetGameFile(type: string) → object?
```

---

> Saves the document.
```csharp
Save() → void
```

---

> Reloads the document.

| Parameter | Description |
|-----------|-------------|
| `force` | If force is true, any unsaved changes will be discarded |
```csharp
Reload(force: bool) → bool
```

---

> Closes the document without saving.
```csharp
Close() → void
```

---


| Parameter | Description |
|-----------|-------------|
| `target` | — |
| `name` | — |
```csharp
AddMenuItem(target: string, name: string) → ScriptFunctionWrapper
```

---


| Parameter | Description |
|-----------|-------------|
| `target` | — |
| `name` | — |
| `onClick` | — |
```csharp
AddMenuItem(target: string, name: string, onClick: ScriptObject) → ScriptFunctionWrapper
```

---


| Parameter | Description |
|-----------|-------------|
| `target` | — |
| `name` | — |
| `onClick` | — |
| `args` | — |
```csharp
AddMenuItem(target: string, name: string, onClick: ScriptObject?, args: params object??[]) → ScriptFunctionWrapper
```

---


| Parameter | Description |
|-----------|-------------|
| `target` | — |
| `name` | — |
| `onClick` | — |
| `args` | — |
```csharp
AddMenuItem(target: ScriptFunctionWrapper, name: string, onClick: ScriptObject? = null, args: params object??[]) → ScriptFunctionWrapper
```

---

> Gets a list of the files available in the game archives Note to myself: Don't use IEnumerable<T>
```csharp
GetArchiveFiles() → IEnumerable
```

---

> DEPRECATED: Please use GetFileFromArchive(path, OpenAs.GameFile) Loads a file from the base archives using either a file path or hash.

| Parameter | Description |
|-----------|-------------|
| `path` | The path of the file to retrieve |
```csharp
GetFileFromBase(path: string) → ? IGameFile
```

---

> DEPRECATED: Please use GetFileFromArchive(hash, OpenAs.GameFile) Loads a file from the base archives using either a file path or hash.

| Parameter | Description |
|-----------|-------------|
| `hash` | The hash of the file to retrieve |
```csharp
GetFileFromBase(hash: ulong) → ? IGameFile
```

---

> Creates a json representation of the specifed game file.

| Parameter | Description |
|-----------|-------------|
| `gameFile` | The gameFile which should be converted |
```csharp
GameFileToJson(gameFile: IGameFile) → ? string
```

---

> Creates a CR2W game file from a json.

| Parameter | Description |
|-----------|-------------|
| `json` | — |
```csharp
JsonToCR2W(json: string) → ? CR2WFile
```

---

> Changes the extension of the provided string path.

| Parameter | Description |
|-----------|-------------|
| `path` | The path of the file to change |
| `extension` | — |
```csharp
ChangeExtension(path: string, extension: string) → string
```

---

> Loads a file from the base archives using either a file path or hash.

| Parameter | Description |
|-----------|-------------|
| `path` | The path of the file to retrieve |
| `openAs` | The output format (OpenAs.GameFile, OpenAs.CR2W or OpenAs.Json) |
```csharp
GetFileFromArchive(path: string, openAs: OpenAs) → ? object
```

---

> Loads a file from the base archives using either a file path or hash.

| Parameter | Description |
|-----------|-------------|
| `hash` | The hash of the file to retrieve |
| `openAs` | The output format (OpenAs.GameFile, OpenAs.CR2W or OpenAs.Json) |
```csharp
GetFileFromArchive(hash: ulong, openAs: OpenAs) → ? object
```

---

> Check if file exists in the game archives.

| Parameter | Description |
|-----------|-------------|
| `path` | file path to check |
```csharp
FileExistsInArchive(path: string) → bool
```

---

> Check if file exists in the game archives.

| Parameter | Description |
|-----------|-------------|
| `hash` | hash value to be checked |
```csharp
FileExistsInArchive(hash: ulong) → bool
```

---

> Converts a YAML string to a JSON string.

| Parameter | Description |
|-----------|-------------|
| `yamlText` | The YAML string to convert |

**Returns:** The converted JSON string
```csharp
YamlToJson(yamlText: string) → string
```

---

> Converts a JSON string to a YAML string.

| Parameter | Description |
|-----------|-------------|
| `jsonText` | The JSON string to convert |

**Returns:** The converted YAML string
```csharp
JsonToYaml(jsonText: string) → string
```

---

```csharp
ConvertGameFile(gameFile: IGameFile, openAs: OpenAs) → ? object
```

---