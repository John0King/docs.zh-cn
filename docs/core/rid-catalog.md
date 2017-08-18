---
title: ".NET Core 运行时标识符 (RID) 目录"
description: "了解运行时标识符 (RID) 及如何在 .NET Core 中使用 RID。"
keywords: .NET, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 08/22/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: b2032f5d-771f-48d9-917c-587d9509035c
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 3490fb639efd223dc36190324bdf3a06bc23c10e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="net-core-runtime-identifier-rid-catalog"></a>.NET Core 运行时标识符 (RID) 目录

## <a name="what-are-rids"></a>RID 是什么？
RID 是运行时标识符的缩写。 RID 用于标识其中将运行应用程序或资产（即程序集）的目标操作系统。 其外观类似如下：“ubuntu.14.04-x64”、“win7-x64”、“osx.10.11-x64”。 对于具有本机依赖项的包，它将指定在其中可以还原包的平台。 

请务必注意 RID 实际上是不透明字符串。 这意味着它们需要与使用它们的操作完全匹配。 例如，让我们设想这样的情况，[Elementary OS](https://elementary.io/) 是 Ubuntu 14.04 的简单克隆。 虽然 .NET Core 和 CLI 基于该版本的 Ubuntu 工作，但如果尝试不进行任何修改就在 Elementary OS 上使用它们，则任何包的还原操作都将失败。 这是因为当前不具有将 Elementary OS 指定为一种平台的 RID。 

表示具体操作系统的 RID 通常遵循以下模式：`[os].[version]-[arch]`，其中：
- `[os]` 是系统名字对象，例如 `ubuntu`。
- `[version]` 是用圆点 (`.`) 分隔的版本号形式表示的操作系统版本（例如 `15.10`），准确性足以合理启用资产来使用该版本代表的操作系统平台 API。
  - 这**不应**为营销版本，因为它们通常代表该操作系统的多个离散版本，且具有不同的平台 API 外围应用。
- `[arch]` 是处理器体系结构，例如 `x86`、`x64`、`arm`、`arm64` 等。

RID 图形是在名为 `runtime.json` 的文件中名为 `Microsoft.NETCore.Platforms` 的包中定义的，请参见 [CoreFX repo](https://github.com/dotnet/corefx/blob/master/pkg/Microsoft.NETCore.Platforms/runtime.json)。 如果使用此文件，你将注意到，某些 RID 中具有 `"#import"` 语句。 这些语句是兼容性语句。 这意味着其中已导入 RID 的 RID 可以作为该 RID 还原包的目标。 看上去有点混乱，让我们看一个示例。 我们来看一看 macOS：

```json
"osx.10.11-x64": {
    "#import": [ "osx.10.11", "osx.10.10-x64" ]
}
```
上述 RID 指定 `osx.10.11-x64` 导入 `osx.10.10-x64`。 这意味着，当还原包时，NuGet 将能够还原指定在 `osx.10.11-x64` 上需要 `osx.10.10-x64` 的所有包。

一个稍微大点的示例 RID 关系图：  

- `win10-arm`
  - `win10`
  - `win81-arm`
    - `win81`
    - `win8-arm`
      - `win8`
        - `win7`
          - `win`
            - `any`

所有 RID 最终都会映射回根 `any` RID。

虽然看起来使用相当容易，但仍有几件关于 RID 的特殊事项，在你使用它们的时候需要牢记：

* 它们是**不透明字符串**并且应将其视为黑框
    * 不应以编程方式构造 RID
* 需要使用已针对平台定义的 RID，并且此文档表明
* RID 需要具体化，因此不用假定来自实际 RID 值的任何内容；请参阅此文档以确定给定平台需要哪个 RID

## <a name="using-rids"></a>使用 RID
若要使用 RID，必须知道有哪些 RID。 新的 RID 将定期添加到该平台。 有关最新版本，请查看 CoreFX 存储库上的 [runtime.json](https://github.com/dotnet/corefx/blob/master/pkg/Microsoft.NETCore.Platforms/runtime.json) 文件。

> [!NOTE]
> 我们正致力于以更具交互性的形式提供此信息。 届时，此页面将更新为指向该工具和/或其使用情况文档。 

## <a name="windows-rids"></a>Windows RID

* Windows 7 / Windows Server 2008 R2
    * `win7-x64`
    * `win7-x86`
* Windows 8 / Windows Server 2012
    * `win8-x64`
    * `win8-x86`
    * `win8-arm`
* Windows 8.1 / Windows Server 2012 R2
    * `win81-x64`
    * `win81-x86`
    * `win81-arm`
* Windows 10 / Windows Server 2016
    * `win10-x64`
    * `win10-x86`
    * `win10-arm`
    * `win10-arm64`

## <a name="linux-rids"></a>Linux RID

* Red Hat Enterprise Linux
    * `rhel.7-x64`
* Ubuntu
    * `ubuntu.14.04-x64`
    * `ubuntu.14.10-x64`
    * `ubuntu.15.04-x64`
    * `ubuntu.15.10-x64`
    * `ubuntu.16.04-x64`
    * `ubuntu.16.10-x64`
* CentOS
    * `centos.7-x64`
* Debian
    * `debian.8-x64`
* Fedora
    * `fedora.23-x64`
    * `fedora.24-x64`
* OpenSUSE
    * `opensuse.13.2-x64`
    * `opensuse.42.1-x64`
* Oracle Linux
    * `ol.7-x64`
    * `ol.7.0-x64`
    * `ol.7.1-x64`
    * `ol.7.2-x64`
* 当前支持的 Ubuntu 派生类 
    * `linuxmint.17-x64`
    * `linuxmint.17.1-x64`
    * `linuxmint.17.2-x64`
    * `linuxmint.17.3-x64`
    * `linuxmint.18-x64`

## <a name="os-x-rids"></a>OS X RID

* `osx.10.10-x64`
* `osx.10.11-x64`
* `osx.10.12-x64`

