---
title: ".NET Core 工具遥测"
description: "了解可收集使用情况信息以供分析使用的 .NET Core 工具遥测功能。"
keywords: .NET, .NET Core
author: richlander
ms.author: mairaw
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 480df976-7568-4df4-9d26-9911357b5a31
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 1816b9fbad1f671820c9f970674c8af2147a230e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="net-core-tools-telemetry"></a>.NET Core 工具遥测

.NET Core 工具包括可收集使用情况信息的[遥测功能](https://github.com/dotnet/cli/pull/2145)。 让 .NET 团队了解工具的使用情况非常重要，我们可由此对其做出改进。

收集的数据是匿名的，并以聚合形式发布，供 Microsoft 和社区工程师在 [Creative Commons Attribution 许可证](https://creativecommons.org/licenses/by/4.0/)下使用。

## <a name="scope"></a>范围

`dotnet` 命令用于启动应用和 .NET Core 工具。 `dotnet` 命令本身不会收集遥测数据。 而是通过 `dotnet` 命令运行的 .NET Core 工具收集遥测数据。

.NET Core 命令（未启用遥测）：

- `dotnet`
- `dotnet [path-to-app]`

.NET Core 工具[命令](index.md)（已启用遥测），如：

- `dotnet build`
- `dotnet pack`
- `dotnet restore`
- `dotnet run`

## <a name="behavior"></a>行为

默认启用 .NET Core 工具遥测功能。 可通过将环境变量 DOTNET_CLI_TELEMETRY_OPTOUT（例如，macOS/Linux 上的 `export`，Windows 上的 `set`）设置为 true（例如“true”, 1），选择退出遥测功能。

## <a name="data-points"></a>数据点

该功能收集以下数据块：

- 正在使用的命令（例如，“生成”、“还原”）
- 命令的 ExitCode
- 对于测试项目，正在使用的测试运行程序
- 调用的时间戳
- 使用的框架
- “运行时”节点中是否存在运行时 ID
- 正在使用的 CLI 版本

该功能不会收集任何个人数据，如用户名或电子邮件。 它不会扫描代码，也不会提取被视为敏感信息的项目级别数据，例如名称、存储库或作者（如果在 project.json 中进行了这些设置）。 我们想知道这些工具的使用方式，而不是用户通过这些工具构建的内容。 如果发现正在收集敏感数据，则那是一个 bug。 请[提出问题](https://github.com/dotnet/cli/issues)，此问题将会得到解决。

## <a name="license"></a>许可证

.NET Core 的 Microsoft 分发由 [MICROSOFT .NET LIBRARY EULA](https://aka.ms/dotnet-core-eula) 授权。 这包括以下重新打印的“DATA”部分，用于启用遥测。

[.NET NuGet 包](https://www.nuget.org/profiles/dotnetframework)使用此相同的许可证，但不启用遥测（请参阅上方的[范围](#scope)）。

> 2. DATA。 此软件可能会收集并向 Microsoft 发送你的信息和软件使用信息。 Microsoft 可能会使用此类信息来改进我们的产品和服务。 可以参阅帮助文档和隐私声明 (http://go.microsoft.com/fwlink/?LinkId=528096)，详细了解数据收集和使用。 使用此软件即表示同意接受这些做法。

## <a name="disclosure"></a>公开

首次运行其中一个命令（例如 `dotnet restore`）时，.NET Core 工具显示以下文本。 此“首次运行”体验是 Microsoft 通知用户有关数据收集信息的方式。 此相同体验最初也使用 .NET Core SDK 中的库填充 NuGet 缓存，从而避免针对这些库的对 NuGet.org（或其他 NuGet 源）的请求。

```console
Welcome to .NET Core!
---------------------
Learn more about .NET Core @ https://aka.ms/dotnet-docs. Use dotnet --help to see available commands or go to https://aka.ms/dotnet-cli-docs.

Telemetry
--------------
The .NET Core tools collect usage data in order to improve your experience.
The data is anonymous and does not include command-line arguments. The data is collected by Microsoft and shared with the community.
You can opt out of telemetry by setting a DOTNET_CLI_TELEMETRY_OPTOUT environment variable to 1 using your favorite shell.
You can read more about .NET Core tools telemetry @ https://aka.ms/dotnet-cli-telemetry.

Configuring...
-------------------
A command is running to initially populate your local package cache, to improve restore speed and enable offline access. This command will take up to a minute to complete and will only happen once.
```

