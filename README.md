# SSMSPlus
SSMS Plus is a productivity extension for SQL Server Management Studio **22** (also targets SSMS 21 via the VSIX InstallationTarget range).

It extends SSMS with a handful set of features:

    Query Execution History
    Schema Object Search
    Document Export for binary columns


### Table Of Contents

- [Getting started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Download](#download)
  * [Install](#install)
  * [Update](#update)
  * [Launch](#launch)
- [Features](#features)
  * [Query History](#query-history)
  * [Schema Object Search](#schema-object-search)
  * [Documents Export](#documents-export)
- [Contributing](#contributing)
  * [How can I contribute ?](#how-can-i-contribute--)
  * [Project Goals](#project-goals)
    + [Goals](#goals)
    + [Non Goals](#non-goals)
  * [Debugging](#debugging)
    + [Debug the SSMS instance](#debug-the-ssms-instance)
    + [The Demo project](#the-demo-project)
    + [Troubleshooting](#troubleshooting)


# Getting started
## Prerequisites
SQL Server Management Studio 22 (SSMS 21 should also accept the same VSIX).

Build requires Visual Studio 2022 with the **Visual Studio extension development** workload (.NET Framework 4.8 targeting pack).

## Download
### For SSMS 22 / 21

Build from this repository (see [PublishRelease.md](PublishRelease.md)), or get a release package from the [Releases](https://github.com/austinkwilliams/SSMSPlus/releases) page when available.

### For SSMS 20

Get this release from upstream:
https://github.com/akarzazi/SSMSPlus/releases (v6 / SSMS 20)

### For SSMS 19

Get this release: 
https://github.com/akarzazi/SSMSPlus/releases/tag/5.0

### For SSMS 18

Get this release: 
https://github.com/akarzazi/SSMSPlus/releases/tag/4.0

## Install

### Preferred: VSIX (SSMS 21 / 22)

SSMS 21+ is based on the Visual Studio 2022 shell and installs extensions via VSIX again. Use the **SSMS-bundled** `VSIXInstaller.exe` (double-clicking a `.vsix` may not bind to SSMS):

```powershell
$ssmsRoot = "C:\Program Files\Microsoft SQL Server Management Studio 22\Release\Common7\IDE"
$vsix = "C:\path\to\SSMSPlus.vsix"
$ssmsVersion = (Get-Item "$ssmsRoot\Ssms.exe").VersionInfo.ProductVersion
& "$ssmsRoot\VSIXInstaller.exe" /skuName:ssms /skuVersion:$ssmsVersion $vsix
```

The packaged manifest targets `Microsoft.VisualStudio.Ssms` version `[21.0,23.0)` for both `amd64` and `arm64`.

### Fallback: copy to Extensions folder

Close SSMS. Copy the built extension folder to:

`C:\Program Files\Microsoft SQL Server Management Studio 22\Release\Common7\IDE\Extensions\SSMSPlus`

Administrator rights are typically required. The folder should contain the SSMSPlus assemblies (do **not** place copies of SSMS host DLLs such as `SqlPackageBase.dll` there).

Older SSMS 18–20 installs still used the SFX extract into `C:\Program Files (x86)\Microsoft SQL Server Management Studio <N>\Common7\IDE\Extensions` — see upstream docs for those versions.

## Update

Close SQL Server Management Studio.

**VSIX:** uninstall/reinstall with `VSIXInstaller.exe`, or replace via Extensions management if available.

**Manual copy:** delete:

`C:\Program Files\Microsoft SQL Server Management Studio 22\Release\Common7\IDE\Extensions\SSMSPlus`

Then follow the install steps again.

## Launch
A new top menu "SSMS Plus" will be available.

![SSMS Plus Menu](docs/illustrations/menu-screen.png?raw=true "SSMS Plus Menu")

# Features

## Query History

Every time you execute a query through the editor, SSMS Plus will save that query.

You'll find your query history through the main menu

![SSMS Plus Query History](docs/illustrations/history-screen.png?raw=true "Query History")

## Schema Object Search

Use this tool to find quickly any user object in the database.

![SSMS Plus Schema Object Search](docs/illustrations/schema-search-screen.png?raw=true "Schema Object Search")

## Documents Export

This tool is handy when you want to preview or export files from the database.

The query is expecting two columns corresponding respectively to file name and file content.

![SSMS Plus Documents Export](docs/illustrations/document-export-screen.png?raw=true "Documents Export")

# Contributing

We're glad to know you're interested in the project.

Your contributions are welcome !

## How can I contribute ?

You can contribute in the following ways : 

* Report an issue / Suggest a feature.
* Create a pull request.

## Project Goals
### Goals
* Performance: Provide a **lightweight** plugin to bring to SSMS those missing features.
* Performance: React to events in an async and **non blocking** way.
* Minimal:  Focus on **handy** features that matter for the community.
* Stable: Do not implement features using **`Reflection`** heavy stuff.
* Ever Green: Focus on the latest SSMS Major Editions.

### Non Goals
* Implement domain specific features. (ex: integrate with FTP, Azure Services)
* Implement heavy features like intellisense.
* Seek for compatibility with an old edition of SQL Server or SSMS.


## Debugging

### Debug the SSMS instance

This section explains how to setup Visual Studio to debug the plugin within an SSMS Instance. 

1.  In the Debug section of the main project "SSMSPlus", setup your SSMS path as the startup program.

`C:\Program Files\Microsoft SQL Server Management Studio 22\Release\Common7\IDE\Ssms.exe`

![SSMS Plus Debug Startup](docs/illustrations/debug-vs-startup.png?raw=true "Documents Export")

2.  In the VSIX section of the main project "SSMSPlus", configure the deployment path for the plugin. 

`C:\Program Files\Microsoft SQL Server Management Studio 22\Release\Common7\IDE\Extensions\SSMSPlus`
![SSMS Plus Documents Export](docs/illustrations/debug-vs-copy-vsix.png?raw=true "Documents Export")

3. That's All ! You may start your the debugging session.

### The Demo project

A [Demo project](src/Demo) is available in the sources.

It is handy for faster UI prototyping, since it does not require to launch SSMS. 

### Troubleshooting

A log record in the folder corresponding to `Environment.SpecialFolder.LocalApplicationData + "\SSMS Plus"` which corresponds generally to `C:\Users\<USER>\AppData\Local\SSMS Plus`.

Theses logs are very useful for diagnostics.
