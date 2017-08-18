---
title: "dotnet-install 脚本"
description: "了解用于安装 .NET Core CLI 工具和共享运行时的 dotnet-install 脚本。"
keywords: "dotnet-install, dotnet-install 脚本, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 07/10/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: b64e7e6f-ffb4-4fc8-b43b-5731c89479c2
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 8af168e96f8f5b57626b126135d8b5e509fbb059
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="dotnet-install-scripts-reference"></a>dotnet-install 脚本引用

## <a name="name"></a>名称

`dotnet-install.ps1` | `dotnet-install.sh` - 用于安装 .NET Core 命令行接口 (CLI) 工具和共享运行时的脚本。

## <a name="synopsis"></a>摘要

Windows：

`dotnet-install.ps1 [-Channel] [-Version] [-InstallDir] [-Architecture] [-SharedRuntime] [-DebugSymbols] [-DryRun] [-NoPath] [-AzureFeed] [-ProxyAddress]`

macOS/Linux：

`dotnet-install.sh [--channel] [--version] [--install-dir] [--architecture] [--shared-runtime] [--debug-symbols] [--dry-run] [--no-path] [--verbose] [--azure-feed] [--help]`

## <a name="description"></a>描述

`dotnet-install` 脚本用于执行 CLI 工具链和共享运行时的非管理员安装。 可以从 [CLI GitHub 存储库](https://github.com/dotnet/cli/tree/rel/1.0.0/scripts/obtain)下载脚本。 

这些脚本主要用于自动化方案和非管理员安装。 共有两个脚本，一个是在 Windows 上运行的 PowerShell 脚本。 另一个脚本是在 Linux/OS X 上运行的 Bash 脚本。两个脚本均具有相同的行为。 Bash 脚本也读取 PowerShell 开关，因此，可以在 Linux/OS X 系统上将 PowerShell 开关与脚本结合使用。 

安装脚本从 CLI 生成放置下载 ZIP/tarball 文件，并将其安装在默认位置或 `-InstallDir|--install-dir` 所指定的位置。 默认情况下，安装脚本下载 SDK 并安装它。 如果只想获取共享的运行时，请指定 `--shared-runtime` 参数。 

默认情况下，该脚本会将安装位置添加到当前会话的 $PATH。 通过指定 `--no-path` 参数覆盖此默认行为。 

运行脚本前，请安装所需的[依赖项](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md)。

可以使用 `--version` 参数安装特定版本。 必须将该版本指定为一个 3 部分构成的版本（例如，1.0.0-13232）。 如果省略，则将默认为层次结构中找到的第一个 [global.json](global-json.md) 文件（内附 `version` 属性），且该结构位于调用脚本的文件夹上方。 如果该版本不存在，则使用最新的版本。

还可以使用 `--debug` 参数运行此脚本，以获取 SDK 或含有调试符号的共享运行时调试二进制文件。 如果在首次安装时无法执行此操作，并在以后意识到需要调试符号，可以使用 `--debug` 参数和已安装的 SDK 版本重新运行该脚本，以获取调试符号。 

## <a name="options"></a>选项

请注意：脚本实现之间的选项有所不同。 

### <a name="powershell-windows"></a>PowerShell (Windows)

`-Channel <CHANNEL>`

指定安装的源通道。 可能的值为：

- `Current` - 当前版本
- `LTS` - 长期支持频道（当前支持版本）
- 表示特定版本的由两部分构成的 X.Y 格式的版本（例如 `2.0` 或 `1.0`）
- 分支名称 [例如 `release/2.0.0`、`release/2.0.0-preview2` 或 `master` 分支中的最新版 `master`（“最前沿”的每日构建）]

默认值为 `LTS`。 有关 .NET 支持频道的详细信息，请参阅 [.NET Core 支持生命周期](https://www.microsoft.com/net/core/support)主题。

`-Version <VERSION>`

表示源频道上的内部版本（请参阅“`-Channel`”选项）。 可能的值为：

- `latest` - 频道上的最新内部版本
- `coherent` - 频道上最新的连贯内部版本；使用最新的稳定包组合
- 表示特定版本的由三部分构成的 X.Y.Z 格式的版本（例如 `1.0.x`，其中 `x` 表示修补程序版本；或特定内部版本，例如 `2.0.0-preview2-006120`）

如果省略，则 `-Version` 默认为是包含 `version` 成员的第一个 [global.json](global-json.md)。 如果它不存在，则 `-Version` 默认为是 `latest`。

`-InstallDir <DIRECTORY>`

指定安装路径。 如果不存在，则会创建该目录。 默认值为 *%LocalAppData%\.dotnet*。 请注意，会将二进制文件直接放入目录中。

`-Architecture <ARCHITECTURE>`

要安装的 .NET Core 二进制文件的体系结构。 可能的值包括 `auto`、`x64` 和 `x86`。 默认值为 `auto`，它表示当前正在运行的操作系统体系结构。

`-SharedRuntime`

如果设置，则此开关限制到共享运行时的安装。 不会安装整个 SDK。

`-DebugSymbols`（请参阅备注）

如果设置，则安装程序在安装中包括调试符号。

> [!NOTE]
> `-DebugSymbols` 开关当前不可用，但计划在将来的版本中提供此功能。

`-DryRun`

如果设置，该脚本不会执行安装，而会显示要使用哪个命令行来持续安装当前请求的 .NET Core CLI 版本。 例如，如果指定版本 `latest`，它将显示特定版本的链接，以便可在生成脚本中明确地使用此命令。 如果想要自行安装或下载，它还会显示二进制文件位置。

`-NoPath`

如果设定，不会将 prefix/installdir 导出到当前会话的路径。 默认情况下，该脚本将修改 PATH，这会使 CLI 工具在安装后立即可用。

`-AzureFeed`

指定此安装程序的 Azure 源的 URL。 不建议更改该值。 默认值为 `https://dotnetcli.azureedge.net/dotnet`。

`-ProxyAddress`

如果设置，安装程序发出 Web 请求时将使用该代理。

### <a name="bash-macoslinux"></a>Bash (macOS/Linux)

`dotnet-install.sh [--channel] [--version] [--install-dir] [--architecture] [--shared-runtime] [--debug-symbols] [--dry-run] [--no-path] [--verbose] [--azure-feed] [--help]`

`-Channel <CHANNEL>`

指定安装的源通道。 可能的值为：

- `Current` - 当前版本
- `LTS` - 长期支持频道（当前支持版本）
- 表示特定版本的由两部分构成的 X.Y 格式的版本（例如 `2.0` 或 `1.0`）
- 分支名称 [例如 `release/2.0.0`、`release/2.0.0-preview2` 或 `master` 分支中的最新版 `master`（“最前沿”的每日构建）]

默认值为 `LTS`。 有关 .NET 支持频道的详细信息，请参阅 [.NET Core 支持生命周期](https://www.microsoft.com/net/core/support)主题。

`-Version <VERSION>`

表示源频道上的内部版本（请参阅“`-Channel`”选项）。 可能的值为：

- `latest` - 频道上的最新内部版本
- `coherent` - 频道上最新的连贯内部版本；使用最新的稳定包组合
- 表示特定版本的由三部分构成的 X.Y.Z 格式的版本（例如 `1.0.x`，其中 `x` 表示修补程序版本；或特定内部版本，例如 `2.0.0-preview2-006120`）

如果省略，则 `-Version` 默认为是包含 `version` 成员的第一个 [global.json](global-json.md)。 如果它不存在，则 `-Version` 默认为是 `latest`。

`--install-dir <DIRECTORY>`

指定安装路径。 如果不存在，则会创建该目录。 默认值为 `$HOME/.dotnet`。

`--architecture <ARCHITECTURE>`

要安装的 .NET Core 二进制文件的体系结构。 可能值为 `auto`、`x64` 和 `amd64`。 默认值为 `auto`，它表示当前正在运行的操作系统体系结构。

`--shared-runtime`

如果设置，则此开关限制到共享运行时的安装。 不会安装整个 SDK。

`--debug-symbols`

如果设置，则安装程序在安装中包括调试符号。

> [!NOTE]
> 此开关当前不可用，但计划在将来的版本中提供此功能。

`--dry-run`

如果设置，该脚本不会执行安装，而会显示要使用哪个命令行来持续安装当前请求的 .NET Core CLI 版本。 例如，如果指定版本 `latest`，它将显示特定版本的链接，以便可在生成脚本中明确地使用此命令。 如果想要自行安装或下载，它还会显示二进制文件位置。

`--no-path`

如果设定，不会将 prefix/installdir 导出到当前会话的路径。 默认情况下，该脚本将修改 PATH，这会使 CLI 工具在安装后立即可用。

`--verbose`

显示诊断信息。

`--azure-feed`

指定此安装程序的 Azure 源的 URL。 不建议更改该值。 默认值为 `https://dotnetcli.azureedge.net/dotnet`。

`--help`

打印脚本帮助。

## <a name="examples"></a>示例

将最新的开发版本安装到默认位置：

Windows：

`./dotnet-install.ps1 -Channel Future`

macOS/Linux：

`./dotnet-install.sh --channel Future`

将最新预览版安装到指定位置：

Windows：

`./dotnet-install.ps1 -Channel preview -InstallDir C:\cli`

macOS/Linux：

`./dotnet-install.sh --channel preview --install-dir ~/cli`

## <a name="see-also"></a>请参阅

[.NET Core 版本](https://github.com/dotnet/core/releases)   
[.NET Core 运行时和 SDK 下载存档](https://github.com/dotnet/core/blob/master/release-notes/download-archive.md)

