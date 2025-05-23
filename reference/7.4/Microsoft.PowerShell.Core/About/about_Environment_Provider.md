---
description: Environment
Locale: en-US
ms.date: 10/18/2018
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_environment_provider?view=powershell-7.4&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Environment_Provider
---
# about_Environment_Provider

## Provider name

Environment

## Drives

`Env:`

## Capabilities

**ShouldProcess**

## Short description

Provides access to the Windows environment variables.

## Detailed description

The PowerShell **Environment** provider lets you get, add, change, clear, and
delete environment variables and values in PowerShell.

**Environment** variables are dynamically named variables that describe the
environment in which your programs run. Windows and PowerShell use environment
variables to store persistent information that affect system and process
execution. Unlike PowerShell variables, environment variables are not subject
to scope constraints.

The **Environment** drive is a flat namespace containing the environment
variables specific to the current user's session. The environment variables
have no child items.

The **Environment** provider supports the following cmdlets, which are covered
in this article.

- [Get-Location][01]
- [Set-Location][02]
- [Get-Item][03]
- [New-Item][04]
- [Remove-Item][05]
- [Clear-Item][06]

## Types exposed by this provider

Each environment variable is an instance of the
[System.Collections.DictionaryEntry][07] class. The name of the variable is the
dictionary key. The value of the environment variable is the dictionary value.

## Navigating the Environment drive

The **Environment** provider exposes its data store in the `Env:` drive. To
work with environment variables, change your location to the `Env:` drive
(`Set-Location Env:`), or work from another PowerShell drive. To reference an
environment variable from another location, use the `Env:` drive name in the
path.

```powershell
Set-Location Env:
```

To return to a file system drive, type the drive name. For example, type:

```powershell
Set-Location C:
```

You can also work with the **Environment** provider from any other PowerShell
drive. To reference an environment variable from another location, use the
drive name `Env:` in the path.

The **Environment** provider also exposes environment variables using a
variable prefix of `$Env:`.  The following command views the contents of the
**ProgramFiles** environment variable. The `$Env:` variable prefix can
be used from any PowerShell drive.

```
PS C:\> $Env:ProgramFiles
C:\Program Files
```

You can also change the value of an environment variable using the `$Env:`
variable prefix.  Any changes made only pertain to the current PowerShell
session for as long as it is active.

> [!NOTE]
> PowerShell uses aliases to allow you a familiar way to work with provider
> paths. Commands such as `dir` and `ls` are now aliases for
> [Get-ChildItem][08], `cd` is an alias for [Set-Location][02] and `pwd` is
> an alias for [Get-Location][01].

## Getting environment variables

This command lists all the environment variables in the current session.

```powershell
Get-Item -Path Env:
```

You can use this command from any PowerShell drive.

The Environment provider has no containers, so the above command has the
same effect when used with `Get-ChildItem`.

```powershell
Get-ChildItem -Path Env:
```

### Get a selected environment variable

This command gets the `windir` environment Variable.

```powershell
Get-ChildItem -Path Env:windir
```

You can also use the variable prefix format as well.

```powershell
$Env:windir
```

## Create an environment variable

This command creates the `USERMODE` environment variable with a value of
"Non-Admin". The `-Path` parameter value creates the new item in the `Env:`
drive. The new environment variable is only usable in the current PowerShell
session for as long as it is active.

```powershell
PS C:\> New-Item -Path Env: -Name USERMODE -Value Non-Admin
```

## Changing an environment variable

### Rename an environment variable

This command uses the `Rename-Item` cmdlet to change the name of the `USERMODE`
environment variable that you created to `USERROLE`. Do not change the name of
an environment variable that the system uses. Although these changes affect
only the current session, they might cause the system or a program to operate
incorrectly.

```powershell
Rename-Item -Path Env:USERMODE -NewName USERROLE
```

### Change an environment variable

This command uses the `Set-Item` cmdlet to change the value of the `USERROLE`
environment variable to "Administrator".

```powershell
Set-Item -Path Env:USERROLE -Value Administrator
```

## Copy an environment variable

This command copies the value of the `USERROLE` environment variable to the
`USERROLE2` environment Variable.

```powershell
Copy-Item -Path Env:USERROLE -Destination Env:USERROLE2
```

## Remove an environment variable

This command deletes the `USERROLE2` environment variable from the current
session.

```powershell
Remove-Item -Path Env:USERROLE2
```

## Remove an environment variable with Clear-Item

This command deletes the `USERROLE` environment variable by clearing its
value.

```powershell
Clear-Item -Path Env:USERROLE
```

## Using the pipeline

Provider cmdlets accept pipeline input. You can use the pipeline to simplify
task by sending provider data from one cmdlet to another provider cmdlet.
To read more about how to use the pipeline with provider cmdlets, see the
cmdlet references provided throughout this article.

## Getting help

Beginning in Windows PowerShell 3.0, you can get customized help topics for
provider cmdlets that explain how those cmdlets behave in a file system drive.

To get the help topics that are customized for the file system drive, run a
[Get-Help][09] command in a file system drive or use the `-Path` parameter of
[Get-Help][09] to specify a file system drive.

```powershell
Get-Help Get-ChildItem
```

```powershell
Get-Help Get-ChildItem -Path Env:
```

## See also

- [about_Providers][10]

<!-- link references -->
[01]: xref:Microsoft.PowerShell.Management.Get-Location
[02]: xref:Microsoft.PowerShell.Management.Set-Location
[03]: xref:Microsoft.PowerShell.Management.Get-Item
[04]: xref:Microsoft.PowerShell.Management.New-Item
[05]: xref:Microsoft.PowerShell.Management.Remove-Item
[06]: xref:Microsoft.PowerShell.Management.Clear-Item
[07]: /dotnet/api/system.collections.dictionaryentry
[08]: xref:Microsoft.PowerShell.Management.Get-ChildItem
[09]: xref:Microsoft.PowerShell.Core.Get-Help
[10]: about_Providers.md
