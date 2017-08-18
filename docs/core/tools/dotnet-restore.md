---
title: "dotnet-restore 命令 - .NET Core CLI"
description: "了解如何使用 dotnet-restore 命令还原依赖项和特定于项目的工具。"
keywords: "dotnet-restore, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/24/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fd7a5769-afbe-4838-bbaf-3ae0cfcbb914
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a9e471bd1d66d68703b025cd3eaa009cb296a9fb
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="dotnet-restore"></a>dotnet-restore

## <a name="name"></a>名称

`dotnet-restore` - 恢复项目的依赖项和工具。

## <a name="synopsis"></a>摘要

`dotnet restore [<ROOT>] [-s|--source] [-r|--runtime] [--packages] [--disable-parallel] [--configfile] [--no-cache] [--ignore-failed-sources] [--no-dependencies] [-v|--verbosity] [-h|--help]`

## <a name="description"></a>描述

`dotnet restore` 命令使用 NuGet 还原依赖项以及在 project 文件中指定的特定于项目的工具。 默认情况下，并行执行对依赖项和工具的还原。

为了还原依赖项，NuGet 需要包所在的源。 通常通过 *NuGet.config* 配置文件提供源。 安装 CLI 工具时提供一个默认的配置文件。 可以通过在项目目录中创建自己的 *NuGet.config* 文件来指定其他源。 也可以在命令提示符处指定每次调用的其他源。 

对于依赖项，使用 `--packages` 参数指定还原操作期间放置还原包的位置。 如未指定，将使用默认的 NuGet 包缓存，可在所有操作系统上的用户主目录（例如，Linux 上的 */home/user1* 或 Windows 上的 *C:\Users\user1*）中的 `.nuget/packages` 目录找到它。

对于特定于项目的工具，`dotnet restore` 首先还原打包工具所在的包，然后继续还原 project 文件中指定的工具依赖项。

`dotnet restore` 命令的行为会受 Nuget.Config 文件（如果有）中某些设置的影响。 例如，在 NuGet.Config 中设置 `globalPackagesFolder` 会将还原的 NuGet 包置于指定的文件夹中。 这是在 `dotnet restore` 命令中指定 `--packages` 选项的替代方法。 有关详细信息，请参阅 [NuGet.Config reference](/nuget/schema/nuget-config-file)（NuGet.Config 引用）。

## <a name="arguments"></a>参数

`ROOT` 
    
要还原的项目文件的可选路径。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

`-s|--source <SOURCE>`

指定要在还原操作期间使用的 NuGet 包源。 这会替代 *NuGet.config* 文件中指定的所有源。 多次指定此选项可以提供多个源。

`-r|--runtime <RUNTIME_IDENTIFIER>`

指定程序包还原的运行时。 这用于还原 *.csproj* 文件中的 `<RuntimeIdentifiers>` 标记中未显式列出的运行时的程序包。 有关运行时标识符 (RID) 的列表，请参阅 [RID 目录](../rid-catalog.md)。 通过多次指定此选项提供多个 RID。

`--packages <PACKAGES_DIRECTORY>`

指定还原包的目录。 

`--disable-parallel`

禁用并行还原多个项目。 

`--configfile <FILE>`

供还原操作使用的 NuGet 配置文件 (*NuGet.config*)。

`--no-cache`

指定不缓存包和 HTTP 请求。

`--ignore-failed-sources`

如果存在符合版本要求的包，则源失败时警告。

`--no-dependencies`

当使用项目到项目 (P2P) 引用还原项目时，还原根项目，不还原引用。

`--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

## <a name="examples"></a>示例

还原当前目录中项目的依赖项和工具：

`dotnet restore` 

还原在给定路径中找到的 `app1` 项目的依赖项和工具：

`dotnet restore ~/projects/app1/app1.csproj`
    
通过将提供的文件路径用作源，在当前目录中还原项目的依赖项和工具：

`dotnet restore -s c:\packages\mypackages` 

通过将提供的两个文件路径用作源，在当前目录中还原项目的依赖项和工具：

`dotnet restore -s c:\packages\mypackages -s c:\packages\myotherpackages` 

还原当前目录中项目的依赖项和工具，并仅显示最少的输出：

`dotnet restore --verbosity minimal`

