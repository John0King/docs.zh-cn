---
title: "dotnet-remove reference 命令 - .NET Core CLI"
description: "使用 dotnet-remove reference 命令可方便地删除“项目到项目”引用。"
keywords: "dotnet-remove, CLI, CLI 命令, .NET Core"
author: spboyer
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 889c6b7e-a313-40b1-9fd3-6a6f4c52f1d0
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: e22f64370be4b56597a303d79d3aabe1ff22a78a
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="dotnet-remove-reference"></a>dotnet-remove reference

## <a name="name"></a>名称

`dotnet-remove reference` - 删除“项目到项目”引用。

## <a name="synopsis"></a>摘要

`dotnet remove [<PROJECT>] reference [-f|--framework] <PROJECT_REFERENCES> [-h|--help]`

## <a name="description"></a>描述

使用 `dotnet remove reference` 命令可方便地从项目删除项目引用。

## <a name="arguments"></a>参数

`PROJECT`

目标项目文件。 如果未指定，此命令会搜索当前目录来获取一个项目文件。

`PROJECT_REFERENCES`

要删除的项目到项目 (P2P) 引用。 可指定一个或多个项目。 基于 Unix/Linux 的终端支持 [Glob 模式](https://en.wikipedia.org/wiki/Glob_(programming))。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

`-f|--framework <FRAMEWORK>`

仅在以特定[框架](../../standard/frameworks.md)为目标时删除引用。

## <a name="examples"></a>示例

从指定项目删除项目引用：

`dotnet remove app/app.csproj reference lib/lib.csproj`

从当前目录中的项目删除多个项目引用：

`dotnet remove reference lib1/lib1.csproj lib2/lib2.csproj`

使用 Unix/Linux 的 glob 模式删除多个项目引用：

`dotnet remove app/app.csproj reference **/*.csproj`

