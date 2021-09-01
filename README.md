BileEx.FileExplorer
===================
A file explorer for Blazor Server projects.

[Nuget](https://www.nuget.org/packages/BileEx.FileExplorer/)

## Why is this repository empty
Project development is done [elsewhere](https://git.tomkarho.com/bile/file-explorer). This repository is more for archival purposes.

## How to use

### Blazor components
Add `@using BileEx.FileExplorer.Components` to your _Imports.razor.

After this you can use the components provided by this library.

### Startup.cs
Add a line `services.AddFileExplorer();` or `services.AddFileExplorer(Configuration.GetSection("[appsettings section]"));` in ConfigureServices.

This exposes `IFileExplorerService` and/or `FileExplorerOptions` instances via dependency injection.

## Components
There are three separate components that can be used together or separately.

### SelectFilesButton
Provides a button that can be used to open SelectFilesDialog. Can be given content like a normal html element.

`<SelectFilesButton>Select file</SelectFilesButton>`

#### Additional parameters
SelectFilesButton takes two additional parameters: Id and ClassName which can be used to edit id and class attributes.
Use these if you need custom css selectors added for styling purposes.

`<SelectFilesButton Id="custom-id" ClassName="custom-class">Select file</SelectFilesButton>`

Generates html:

`<button id="custom-id" class="bile-button custom-class">Custom id only</button>`

Notice that id field is replaced by any given parameter while class is only appended.

### SelectFilesDialog
Provides a dialog for interacting with file system. Use in conjunction with SelectFilesButton.

Default css puts this component above other elements, in the center with dark background using position absolute etc.
Plan your layout and css accordingly.

Takes two additional parameters: Id and ClassName which can be used to edit id and class attributes.
Use these if you need custom css selectors added for styling purposes.

### SelectedFiles
Provides a list of selected files. More a debugging tool than any real use unless your use case really is to just display files and do nothing else with them.

## Configuration
You can provide in startup.cs appsettings.json configuration section.

Examples:

```json
{
  "BileEx": {
    "FileExplorer": {
      "AllowedFileTypes": ["video"],
      "ComparisonLevel": 0
    }
  } 
}
```

```json
{
  "BileEx": {
    "FileExplorer": {
      "AllowedFileTypes": [],
      "ComparisonLevel": 0
    }
  } 
}
```

```json
{
  "BileEx": {
    "FileExplorer": {
      "AllowedFileTypes": ["video/x-matroska"],
      "ComparisonLevel": 1
    }
  } 
}
```
### AllowedFileTypes
Provides an array of files types that file dialog can be filtered by.
Array must match either strictly or laxly valid mimetypes.

### ComparisonLevel
Determine whether AllowedFileTypes is used strictly or laxly.

#### Strict (1)
Requires full mimetype to be provided for file to be recognized.
Let's say you have four files in a folder:

- testvid.mp4
- testvid.mkv
- testvid.mpeg
- test.txt

And set AllowedFileTypes: ["video/mp4"].

Only **testvid.mp4** will be displayed due to strict interpretation.


#### Lax (0)
Only requires the first part of a mimetype to be provided.
Let's say you have four files in a folder:

- testvid.mp4
- testvid.mkv
- testvid.mpeg
- test.txt

And set AllowedFileTypes: ["video"].

- testvid.mp4
- testvid.mkv
- testvid.mpeg

Would be displayed.

### How to contribute
Get in touch with the author at [tomkarho.com](https://tomkarho.com/contact)
