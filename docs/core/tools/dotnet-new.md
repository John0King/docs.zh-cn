---
title: "dotnet-new 命令 - .NET Core CLI"
description: "dotnet-new 命令可在当前目录中创建新的 .NET Core 项目。"
keywords: "dotnet-new, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fcc3ed2e-9265-4d50-b59e-dc2e5c190b34
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 56033295b2448b045d5a51dbd84d5429aed77451
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="dotnet-new"></a>dotnet-new

## <a name="name"></a>名称

`dotnet-new` - 根据指定的模板，创建新的项目、配置文件或解决方案。

## <a name="synopsis"></a>摘要

```
dotnet new <TEMPLATE> [-lang|--language] [-n|--name] [-o|--output] [-all|--show-all] [-h|--help] [Template options]
dotnet new <TEMPLATE> [-l|--list]
dotnet new [-all|--show-all]
dotnet new [-h|--help]
```

## <a name="description"></a>说明

`dotnet new` 命令为初始化有效的 .NET Core 项目提供了便捷方法。 

命令调用[模板引擎](https://github.com/dotnet/templating)，以根据指定的模板和选项在磁盘上创建项目。

## <a name="arguments"></a>参数

`TEMPLATE`

调用命令时要实例化的模板。 每个模板可能具有可传递的特定选项。 有关详细信息，请参阅[模板选项](#template-options)。

此命令包含默认的模板列表。 使用 `dotnet new -all` 获取可用模板的列表。 下表显示随 SDK 一起预安装的模板。 模板的默认语言显示在括号内。

|模板描述  | 模板名称  | 语言 |
|----------------------|----------------|-----------|
| 控制台应用程序  | 控制台        | [C#]，F#  |
| 类库        | classlib       | [C#]，F#  |
| 单元测试项目    | mstest         | [C#]，F#  |
| xUnit 测试项目   | xunit          | [C#]，F#  |
| ASP.NET Core 空   | Web            | [C#]      |
| ASP.NET Core Web 应用 | mvc            | [C#]，F#  |
| ASP.NET Core Web API | webapi         | [C#]      |
| Nuget 配置         | nugetconfig    |           |
| Web 配置           | webconfig      |           |
| 解决方案文件        | sln            |           |

## <a name="options"></a>选项

`-h|--help`

打印命令帮助。 可针对 `dotnet new` 命令本身或任何模板（如 `dotnet new mvc --help`）调用它。

`-l|--list`

列出包含指定名称的模板。 如果针对 `dotnet new` 命令调用，则它列出可能对给定的目录可用的模板。 例如，如果该目录已包含一个项目，则它不会列出所有项目模板。

`-lang|--language {C#|F#}`

要创建的模板的语言。 接受的语言因模板而异（请参阅[参数](#arguments)部分中的默认值）。 对于某些模板无效。

`-n|--name <OUTPUT_NAME>`

所创建的输出的名称。 如果未指定名称，使用的是当前目录的名称。

`-o|--output <OUTPUT_DIRECTORY>`

用于放置生成的输出的位置。 默认为当前目录。

`-all|--show-all`

单独在 `dotnet new` 命令的上下文中运行时，显示特定类型的项目的所有模板。 在特定模板（如 `dotnet new web -all`）的上下文中运行时，`-all` 解释为一个强制创建标记。 输出目录已包含一个项目时，可能需要此操作。

## <a name="template-options"></a>模板选项

每个项目模板都可能有附加选项。 核心模板有以下选项：

**console、xunit、mstest、web、webapi**

`-f|--framework` - 指定目标[框架](../../standard/frameworks.md)。 值：`netcoreapp1.0` 或 `netcoreapp1.1`（默认：`netcoreapp1.0`）

**mvc**

`-f|--framework` - 指定目标[框架](../../standard/frameworks.md)。 值：`netcoreapp1.0` 或 `netcoreapp1.1`（`Default: netcoreapp1.0`）

`-au|--auth` - 要使用的身份验证类型。 值：`None` 或 `Individual`（默认：`None`）

`-uld|--use-local-db` - 指定是否使用 LocalDB，而不是 SQLite。 值：`true` 或 `false`（默认：`false`）

**classlib**

`-f|--framework` - 指定目标[框架](../../standard/frameworks.md)。 值：`netcoreapp1.0`、`netcoreapp1.1` 或 `netstandard1.0` 到 `netstandard1.6`（默认：`netstandard1.4`）

## <a name="examples"></a>示例

在当前目录中创建 F# 控制台应用程序项目：

`dotnet new console -lang f#` 
   
在当前目录中新建定位 .NET Core 1.0 且没有设置身份验证的 ASP.NET Core C# MVC 应用程序项目：  

`dotnet new mvc -au None -f netcoreapp1.0`
 
新建定位 .NET Core 1.1 的 xUnit 应用程序：

`dotnet new xunit --framework netcoreapp1.1`

列出适用于 MVC 的所有模板：

`dotnet new mvc -l`

