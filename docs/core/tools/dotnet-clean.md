---
title: "dotnet-clean 命令 - .NET Core CLI"
description: "dotnet-clean 命令可清除当前目录。"
keywords: "dotnet-clean, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: eff65fa1-bab4-4421-8260-d0a284b690b2
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 10222781d5bff596d1b7883bc73097758e878235
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="dotnet-clean"></a>dotnet-clean

## <a name="name"></a>名称

`dotnet-clean` - 清除项目输出。 

## <a name="synopsis"></a>摘要

`dotnet clean [<PROJECT>] [-o|--output] [-f|--framework] [-c|--configuration] [-v|--verbosity] [-h|--help]`

## <a name="description"></a>描述

`dotnet clean` 命令可清除上一个生成的输出。 它以 [MSBuild 目标](/visualstudio/msbuild/msbuild-targets) 的形式实现，以便在运行命令时对项目进行评估。 只会清除在生成过程中创建的输出。 中间 (*obj*) 和最终输出 (*bin*) 文件夹都会被清除。

## <a name="arguments"></a>参数

`PROJECT`

要清除的 MSBuild 项目。 如果未指定项目文件，MSBuild 会在当前工作目录中搜索以 *proj* 结尾的文件扩展名并使用该文件。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

`-o|--output <OUTPUT_DIRECTORY>`

包含已生成的输出的目录。 如果在生成项目时指定了框架，则使用输出目录开关指定 `-f|--framework <FRAMEWORK>` 开关。

`-f|--framework <FRAMEWORK>`

在生成时指定的[框架](../../standard/frameworks.md)。 必须在[项目文件](csproj.md)中定义该框架。 如果在生成时指定了框架，则必须在清除时指定框架。

`-c|--configuration <CONFIGURATION>`

定义配置。 如果省略，则默认为 `Debug`。 如果在生成时指定了属性，则仅在清除时需要该属性。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许的级别为 q[uiet]、m[inimal]、n[ormal]、d[etailed] 和 diag[nostic]。

## <a name="examples"></a>示例

清除项目的默认生成：

`dotnet clean`

清除使用版本配置生成的项目：

`dotnet clean --configuration Release`

