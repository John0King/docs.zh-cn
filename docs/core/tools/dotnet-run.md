---
title: "dotnet-run 命令 - .NET Core CLI"
description: "dotnet-run 命令为从源代码运行应用程序提供了一个方便的选项。"
keywords: "dotnet-run, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/22/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 40d4e60f-9900-4a48-b03c-0bae06792d91
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: f0a6fce4f83808076b7cbcabdaa948badde2cf80
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="dotnet-run"></a>dotnet-run

## <a name="name"></a>名称 

`dotnet-run` - 无需任何显式编译或启动命令即可运行源代码。

## <a name="synopsis"></a>摘要

`dotnet run [-c|--configuration] [-f|--framework] [-p|--project] [[--] [application arguments]] [-h|--help]`

## <a name="description"></a>描述

`dotnet run` 命令为从源代码使用一个命令运行应用程序提供了一个方便的选项。 这对从命令行中进行快速迭代开发很有帮助。 命令取决于生成代码的 [`dotnet build`](dotnet-build.md) 命令。 对于此生成的任何要求，例如项目必须首先还原，同样适用于 `dotnet run`。 

输出文件会写入到默认位置，即 `bin/<configuration>/<target>`。 例如，如果具有 `netcoreapp1.0` 应用程序并且运行 `dotnet run`，则输出置于 `bin/Debug/netcoreapp1.0`。 将根据需要覆盖文件。 临时文件将置于 `obj` 目录。 

如果该项目指定多个框架，在不使用 `-f|--framework <FRAMEWORK>` 选项指定框架时，执行 `dotnet run` 将导致错误。

在项目上下文，而不是生成程序集中使用 `dotnet run` 命令。 如果尝试改为运行依赖于框架的应用程序 DLL，则必须在不使用命令的情况下使用 [dotnet](dotnet.md)。 例如，若要运行 `myapp.dll`，请使用：
 
```
dotnet myapp.dll
```

有关 `dotnet` 驱动程序的详细信息，请参阅 [.NET Core 命令行工具 (CLI)](index.md) 主题。

若要运行应用程序，`dotnet run` 命令需从 NuGet 缓存解析共享运行时之外的应用程序依赖项。 因为它使用缓存的依赖项，因此，不推荐在生产中使用 `dotnet run` 来运行应用程序。 相反，使用 [`dotnet publish`](dotnet-publish.md)[ 命令创建部署](../deploying/index.md)，并部署已发布的输出。 

## <a name="options"></a>选项

`--`

将参数分隔到正在运行的应用程序的参数的 `dotnet run`。 在此参数后的所有参数均传递给已运行的应用程序。 

`-h|--help`

打印出有关命令的简短帮助。

`-c|--configuration <CONFIGURATION>`

用于生成项目的配置。 默认值为 `Debug`。

`-f|--framework <FRAMEWORK>`

使用指定[框架](../../standard/frameworks.md)生成并运行应用。 框架必须在项目文件中进行指定。

`-p|--project <PATH/PROJECT.csproj>`

指定项目文件的路径和名称。 （请参阅备注。）如果未指定，则默认为当前目录。

> [!NOTE]
> 通过 `-p|--project` 选项使用项目文件的路径和名称。 CLI 中的回归可阻止当前提供文件夹路径。 若要了解详细信息并跟踪此问题，请参阅 [dotnet run -p，无法启动项目 (dotnet/cli #5992)](https://github.com/dotnet/cli/issues/5992)。

## <a name="examples"></a>示例

运行当前目录中的项目：

`dotnet run` 

运行指定的项目：

`dotnet run --project /projects/proj1/proj1.csproj`

运行当前目录中的项目（在本例中，`--help` 参数被传递到应用程序，因为使用了 `--` 参数）：

`dotnet run --configuration Release -- --help`

