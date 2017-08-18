---
title: "Windows 上 .NET Core 的先决条件"
description: "了解在 Windows 计算机上开发和运行 .NET Core 应用程序所需的依赖项。"
keywords: ".NET Core、Windows、先决条件、依赖项、Visual Studio"
author: mairaw
ms.author: mairaw
ms.date: 06/26/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0e414af0edbafed5b7f540eda6de2e5078eac789
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="prerequisites-for-net-core-on-windows"></a>Windows 上 .NET Core 的先决条件

本文展示了在 Windows 计算机上部署和运行 .NET Core 应用程序并使用 Visual Studio 进行开发时所需的依赖项。

## <a name="supported-windows-versions"></a>受支持的 Windows 版本

以下 Windows 版本均支持 .NET Core：

* Windows 7 SP1
* Windows 8.1
* Windows 10
* Windows Server 2008 R2 SP1（完全服务器或服务器核心）
* Windows Server 2012 SP1（完全服务器或服务器核心）
* Windows Server 2012 R2（完全服务器或服务器核心）
* Windows Server 2016（完全服务器、服务器核心或 Nano Server）

在 [.NET Core 发行说明](https://github.com/dotnet/core/blob/master/release-notes/1.1/1.1.md)中查看一系列完整的受支持的操作系统。

## <a name="net-core-dependencies"></a>.NET Core 依赖项

在早于 Windows 10 和 Windows Server 2016 的 Windows 版本上运行 .NET Core 时，需要 Visual C++ Redistributable。 若使用 .NET Core 安装程序，将自动安装此依赖项。 但是，如果通过[安装程序脚本](./tools/dotnet-install-script.md)安装 .NET Core 或部署独立的 .NET Core 应用程序，则需要手动安装 [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=52685)。

> [!NOTE]
> <em>仅适用于 Windows 7 和 Windows Server 2008 计算机：</em><br>
> 确保 Windows 安装是最新版本，并且包括通过 Windows 更新安装的修补程序 [KB2533623](https://support.microsoft.com/help/2533623)。

## <a name="prerequisites-with-visual-studio-2017"></a>Visual Studio 2017 的先决条件

可以使用所选择的任何编辑器，使用 .NET Core SDK 开发 .NET Core 应用程序。 但是，若要在集成的开发环境中的 Windows 上开发 .NET Core 应用程序，可以使用 [Visual Studio 2017](#visual-studio-2017)。

> [!IMPORTANT]
> 尽管可以在 .NET Core 工具的预览版中使用 Visual Studio 2015，但这些项目基于 *project.json* 的，现在已弃用。 Visual Studio 2017 使用基于 MSBuild 的项目文件。 有关格式更改的详细信息，请参阅[有关更改的高级别概述](./tools/cli-msbuild-architecture.md)。

若要使用 Visual Studio 2017 开发 .NET Core 应用，必须选择将 **.NET Core 跨平台开发**工具集（在“其他工具集”部分中）与最新版本的 Visual Studio 一并安装。
![选中“.NET Core 跨平台开发”工作负荷的 Visual Studio 2017 安装的屏幕截图](./media/windows-prerequisites/vs_workloads.jpg)

Visual Studio 2017 有不同的版本。 可以免费下载 [Visual Studio Community 2017](https://www.visualstudio.com/downloads/) 并开始使用。  若要了解有关 Visual Studio 安装过程的详细信息，请参阅[安装 Visual Studo 2017](/visualstudio/install/install-visual-studio)。

若要验证运行的是否是最新版本的 Visual Studio 2017，请执行以下操作：

 * 在“帮助”菜单上，选择“关于 Microsoft Visual Studio”。
 * 在“关于 Microsoft Visual Studio”对话框中，版本号应该是 15.0.26228.4 或更高版本。

在[发行说明](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)中可以详细了解 Visual Studio 2017 中的更改。

