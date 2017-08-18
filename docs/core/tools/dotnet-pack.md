---
title: "dotnet-pack 命令 - .NET Core CLI"
description: "dotnet-pack 命令可为 .NET Core 项目创建 NuGet 包。"
keywords: "dotnet-pack, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 8dbbb3f7-b817-4161-a6c8-a3489d05e051
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 04b967fdf6578098caae8c21604c5d6160eb6775
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="dotnet-pack"></a>dotnet-pack

## <a name="name"></a>名称

`dotnet-pack` - 将代码打包到 NuGet 包。

## <a name="synopsis"></a>摘要

`dotnet pack [<PROJECT>] [-o|--output] [--no-build] [--include-symbols] [--include-source] [-c|--configuration] [--version-suffix <VERSION_SUFFIX>] [-s|--serviceable] [-v|--verbosity] [-h|--help]`

## <a name="description"></a>描述

`dotnet pack` 命令生成项目并创建 NuGet 包。 该命令的结果是一个 NuGet 包。 如果 `--include-symbols` 选项存在，则创建包含调试符号的另一个包。 

将被打包项目的 NuGet 依赖项添加到 *.nuspec* 文件，以便在安装包时可以进行正确解析。 项目到项目的引用不会打包到项目内。 目前，如果具有项目到项目的依赖项，则每个项目均必须包含一个包。

默认情况下，`dotnet pack` 先构建项目。 如果希望避免此行为，则传递 `--no-build` 选项。 这通常在持续集成 (CI) 生成方案中非常有用，在其中你可以知道代码是之前生成的。

可向 `dotnet pack` 命令提供 MSBuild 属性，用于打包进程。 有关详细信息，请参阅 [NuGet 元数据属性](csproj.md#nuget-metadata-properties)和 [MSBuild 命令行引用](/visualstudio/msbuild/msbuild-command-line-reference)。

## <a name="arguments"></a>参数

`PROJECT` 
    
要打包的项目。 它可能是 [csproj 文件](csproj.md)或目录的路径。 如果省略，则默认为当前目录。 

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。  

`-o|--output <OUTPUT_DIRECTORY>`

将生成的包放置在指定目录。 

`--no-build`

打包前不生成项目。 

`--include-symbols`

生成符号 `nupkg`。 

`--include-source`

将源文件包括在 NuGet 包中。 源文件包括在 `nupkg` 内的 `src` 文件夹中。 

`-c|--configuration <CONFIGURATION>`

生成项目时要使用的配置。 如果未指定，则配置默认为 `Debug`。

`--version-suffix <VERSION_SUFFIX>`

定义项目中 `$(VersionSuffix)` MSBuild 属性的值。

`-s|--serviceable`

设置包中可用的标志。 有关详细信息，请参阅 [.NET 博客：.NET 4.5.1 支持 .NET NuGet 库的 Microsoft 安全更新](https://aka.ms/nupkgservicing)。

`--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

## <a name="examples"></a>示例

打包当前目录中的项目：

`dotnet pack`

打包 `app1` 项目：

`dotnet pack ~/projects/app1/project.csproj`
    
打包当前目录中的项目并将生成的包放置到 `nupkgs` 文件夹：

`dotnet pack --output nupkgs`

将当前目录中的项目打包到 `nupkgs` 文件夹并跳过生成步骤：

`dotnet pack --no-build --output nupkgs`

将项目的版本后缀配置为 *.csproj* 文件中的 `<VersionSuffix>$(VersionSuffix)</VersionSuffix>`，使用给定的后缀打包当前项目，并更新生成的程序包版本：

`dotnet pack --version-suffix "ci-1234"`

使用 `PackageVersion` MSBuild 属性将包版本设置为 `2.1.0`：

`dotnet pack /p:PackageVersion=2.1.0`

