---
description: Information about installing PowerShell on Red Hat Enterprise Linux (RHEL)
ms.date: 07/03/2025
title: Installing PowerShell on Red Hat Enterprise Linux (RHEL)
---
# Installing PowerShell on Red Hat Enterprise Linux (RHEL)

All packages are available on our GitHub [releases][02] page. Before installing, check the list of
[Supported versions][01] below. After the package is installed, run `pwsh` from a terminal. Run
`pwsh-preview` if you installed a preview release.

> [!NOTE]
> PowerShell 7.4 is an in-place upgrade that removes previous versions of PowerShell 7. Preview
> versions of PowerShell can be installed side-by-side with other versions of PowerShell. If you
> need to run PowerShell 7.4 side-by-side with a previous version, reinstall the previous version
> using the [binary archive][05] method.

RHEL 7 uses `yum` and RHEL 8 and higher uses the `dnf` package manager.

[!INCLUDE [Latest version](../../includes/latest-install.md)]

## Installation via the Package Repository

Microsoft builds and supports a variety of software products for Linux systems and makes them
available via Linux packaging clients (apt, dnf, yum, etc). These Linux software packages are hosted
on the _Linux package repository for Microsoft products_, [https://packages.microsoft.com][03], also
known as _PMC_.

Installing PowerShell from PMC is the preferred method of installation.

> [!NOTE]
> This script only works for supported versions of RHEL.

```sh
###################################
# Prerequisites

# Get version of RHEL
source /etc/os-release
if [ ${VERSION_ID%.*} -lt 8 ]
then majorver=7
elif [ ${VERSION_ID%.*} -lt 9 ]
then majorver=8
else majorver=9
fi

# Download the Microsoft RedHat repository package
curl -sSL -O https://packages.microsoft.com/config/rhel/$majorver/packages-microsoft-prod.rpm

# Register the Microsoft RedHat repository
sudo rpm -i packages-microsoft-prod.rpm

# Delete the downloaded package after installing
rm packages-microsoft-prod.rpm

# Update package index files
sudo dnf update
# Install PowerShell
sudo dnf install powershell -y
```

## Installation via direct download

PowerShell 7.2 introduced a universal package that makes installation easier. Download the universal
package from the [releases][02] page onto your RHEL machine.

The link to the current version is:

- PowerShell 7.4.11 universal package for supported versions of RHEL
  - `https://github.com/PowerShell/PowerShell/releases/download/v7.4.11/powershell-7.4.11-1.rh.x86_64.rpm`
- PowerShell 7.5.2 universal package for supported versions of RHEL
  - `https://github.com/PowerShell/PowerShell/releases/download/v7.5.2/powershell-7.5.2-1.rh.x86_64.rpm`

The following shell script downloads and installs the current preview release of PowerShell. You can
change the URL to download the version of PowerShell that you want to install.

On RHEL 8 or 9:

```sh
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v7.5.2/powershell-7.5.2-1.rh.x86_64.rpm
```

## Uninstall PowerShell

On RHEL 8 or 9:

```sh
sudo dnf remove powershell
```

## Support for Arm processors

PowerShell 7.2 and newer supports running on RHEL using a 64-bit Arm processor. Use the binary
archive installation method of installing PowerShell that's described in
[Alternate ways to install PowerShell on Linux][05].

## PowerShell paths

- `$PSHOME` is `/opt/microsoft/powershell/7/`
- The profiles scripts are stored in the following locations:
  - AllUsersAllHosts - `$PSHOME/profile.ps1`
  - AllUsersCurrentHost - `$PSHOME/Microsoft.PowerShell_profile.ps1`
  - CurrentUserAllHosts - `~/.config/powershell/profile.ps1`
  - CurrentUserCurrentHost - `~/.config/powershell/Microsoft.PowerShell_profile.ps1`
- Modules are stored in the following locations:
  - User modules - `~/.local/share/powershell/Modules`
  - Shared modules - `/usr/local/share/powershell/Modules`
  - Default modules - `$PSHOME/Modules`
- PSReadLine history is recorded in `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

PowerShell respects the [XDG Base Directory Specification][04] on Linux.

## Supported versions

[!INCLUDE [RHEL support](../../includes/rhel-support.md)]

## Installation support

Microsoft supports the installation methods in this document. There may be other methods of
installation available from other third-party sources. While those tools and methods may work,
Microsoft can't support those methods.

<!-- link references -->
[01]: #supported-versions
[02]: https://aka.ms/PowerShell-Release?tag=stable
[03]: https://packages.microsoft.com
[04]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
[05]: install-other-linux.md#binary-archives
