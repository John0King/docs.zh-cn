---
title: "dotnet-publish 命令 - .NET Core CLI"
description: "dotnet-publish 命令可将 .NET Core 项目发布到目录。"
keywords: "dotnet-publish, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: f2ef275a-7c5e-430a-8c30-65f52af62771
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a8a37b1eacab13682d4f4a2bea2f9ea248cdd9eb
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="dotnet-publish"></a>dotnet-publish

## <a name="name"></a>名称

`dotnet-publish` - 将应用程序及其依赖项打包到文件夹以部署到托管系统。

## <a name="synopsis"></a>摘要

`dotnet publish [<PROJECT>] [-f|--framework] [-r|--runtime] [-o|--output] [-c|--configuration] [--version-suffix] [-v|--verbosity] [-h|--help]`

## <a name="description"></a>说明

`dotnet publish` 编译应用程序、读取 project 文件中指定的所有依赖项并将生成的文件集发布到目录。 输出将包含以下信息：

* 扩展名为 `*.dll` 的程序集中的中间语言 (IL) 代码。
* *\*.deps.json* 文件，包含项目的所有依赖项。
* *\*.runtime.config.json* 文件，指定应用程序所要求的共享运行时以及该运行时的其他配置选项（例如，垃圾回收类型）。
* 应用程序的依赖项。 将这些依赖项从 NuGet 缓存复制到输出文件夹。

`dotnet publish` 命令的输出已准备好部署到托管系统（例如，服务器、电脑、Mac 和笔记本电脑）以供执行，它还是准备应用程序以供部署的唯一受官方支持的方法。 根据项目指定的部署的类型，托管系统不一定已在其上安装 .NET Core 共享运行时。 有关详细信息，请参阅 [.NET Core 应用程序部署](../deploying/index.md)。 有关已发布应用程序的目录结构，请参阅[目录结构](/aspnet/core/hosting/directory-structure)。

## <a name="arguments"></a>参数

`PROJECT` 

要发布的项目，如果未指定，则默认为当前目录。 

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。  

`-f|--framework <FRAMEWORK>`

为指定的[目标框架](../../standard/frameworks.md)发布应用程序。 必须在项目文件中指定目标框架。

`-r|--runtime <RUNTIME_IDENTIFIER>`

发布针对给定运行时的应用程序。 这将在创建[独立部署 (SCD)](../deploying/index.md#self-contained-deployments-scd) 时使用。 有关运行时标识符 (RID) 的列表，请参阅 [RID 目录](../rid-catalog.md)。 默认为发布[依赖于框架的部署 (FDD)](../deploying/index.md#framework-dependent-deployments-fdd)。

`-o|--output <OUTPUT_DIRECTORY>`

指定输出目录的路径。 如未指定，对于依赖于框架的部署，将默认为 *./bin/[configuration]/[framework]/* 或对于独立部署，将默认为 *./bin/[configuration]/[framework]/[runtime]*。

`-c|--configuration <CONFIGURATION>`

生成项目时要使用的配置。 默认值为 `Debug`。

`--version-suffix <VERSION_SUFFIX>`

定义版本后缀来替换项目文件的版本字段中的星号 (`*`)。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

## <a name="examples"></a>示例

在当前目录中发布项目：

`dotnet publish`

使用指定的项目文件发布应用程序：

`dotnet publish ~/projects/app1/app1.csproj`
    
使用 `netcoreapp1.1` 框架发布当前目录中的项目：

`dotnet publish --framework netcoreapp1.1`
    
使用 `netcoreapp1.1` 框架和 `OS X 10.10` 的运行时发布当前应用程序（必须在项目文件中列出此 RID）。

`dotnet publish --framework netcoreapp1.1 --runtime osx.10.11-x64`

## <a name="see-also"></a>请参阅

* [目标框架](../../standard/frameworks.md)
* [运行时标识符 (RID) 目录](../rid-catalog.md)

